#include<reg51.h>

sbit led = P2^4;

void delay(){
	TMOD = 0x01;
	TH0 = 0xF4;
	TL0 = 0xDC;
	TR0 = 1;
	while(TF0 == 0);
	TR0 = 0;
	TF0 = 0; 
}

void main(){
	led = 1;
	while(1){
		led =~ led;
		delay();
	}
}

