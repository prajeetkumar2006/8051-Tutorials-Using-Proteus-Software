#include <reg51.h>


#define LCD P3
sbit RS = P2^0;
sbit EN = P2^1;


#define ROW P0    
#define COL P1  


void delay(unsigned int d)
{
    unsigned int i,j;
    for(i=0;i<d;i++)
        for(j=0;j<120;j++);
}


void lcd_cmd(unsigned char cmd)
{
    LCD = cmd;
    RS = 0;
    EN = 1;
    delay(2);
    EN = 0;
}

void lcd_data(unsigned char dat)
{
    LCD = dat;
    RS = 1;
    EN = 1;
    delay(2);
    EN = 0;
}

void lcd_init()
{
    lcd_cmd(0x38); 
    lcd_cmd(0x0C); 
    lcd_cmd(0x06); 
    lcd_cmd(0x01); 
    delay(5);
}


char keypad_scan()
{
    char col;

    while(1)
    {
       
        ROW = 0xFE; 
        col = COL & 0x78; 
        if(!(col & 0x08)) return '1';
        if(!(col & 0x10)) return '4';
        if(!(col & 0x20)) return '7';
        if(!(col & 0x40)) return '*';
        
       
        ROW = 0xFD; 
        col = COL & 0x78;
        if(!(col & 0x08)) return '2';
        if(!(col & 0x10)) return '5';
        if(!(col & 0x20)) return '8';
        if(!(col & 0x40)) return '0';
        

        ROW = 0xFB; 
        col = COL & 0x78;
        if(!(col & 0x08)) return '3';
        if(!(col & 0x10)) return '6';
        if(!(col & 0x20)) return '9';
        if(!(col & 0x40)) return '#';
        
        delay(10); 
    }
}


void main()
{
    char key;
    lcd_init();

    while(1)
    {
        key = keypad_scan();
        lcd_cmd(0x01); 
        lcd_cmd(0x80); 
        lcd_data(key); 
        delay(300);
    }
}
