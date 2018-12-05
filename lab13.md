# 贪吃蛇C语言实现
```cs
#include<stdio.h>
#include<stdlib.h>
#include<time.h>
#include<math.h>

#define SNAKE_MAX_LENGTH 20
#define SNAKE_HEAD 'H'
#define SNAKE_BODY 'X'
#define BLANK_CELL '' 
#define SNAKE_FOOD '$'
#define WALL_CELL '*'

void snakeMove(int,int);
void put_money(void);
void output(void);
int gameover(void);

char map[13][13]=
     {"************", 
     "*XXXXH     *",
     "*          *",
     "*          *",
     "*          *",
     "*          *",
     "*          *",
     "*          *",
     "*          *",
     "*          *",
     "*          *",
     "************"};
     
int snakeX[SNAKE_MAX_LENGTH]={1,2,3,4,5};
int snakeY[SNAKE_MAX_LENGTH]={1,1,1,1,1};
int snakeLength=5;

int main(){
	put_money();
	output();
	char ch;
	while(1){
		scanf("%c",&ch);
		switch(ch){
			case 'A':snakeMove(-1,0); break;
			case 'D':snakeMove(1,0); break;
			case 'W':snakeMove(0,-1); break;
			case 'S':snakeMove(0,1); break;
		}
		if(gameover()==1){
			output();
		}	
		
		else{
			return 0;
		}
	}
}

int gameover(void){
	int i,j;
	for(i=0;i<snakeLength-1;i++){
		if(snakeX[i]==snakeX[snakeLength-1]&&snakeY[snakeLength-1]==snakeY[i]){
			printf("Game Over.\n");
			return 0;
		}
	}
		
	if(snakeX[snakeLength-1]==0||snakeX[snakeLength-1]==11||snakeY[snakeLength-1]==0||snakeY[snakeLength-1]==11){
		printf("Game Over.\n");
		return 0;
	}
	else return 1;
		
	}


void snakeMove(int x,int y){
	if(map[snakeY[snakeLength-1]+y][snakeX[snakeLength-1]+x]=='$'){
		map[snakeY[snakeLength-1]][snakeX[snakeLength-1]] = 'X';
		snakeY[snakeLength]=snakeY[snakeLength-1]+y;
		snakeX[snakeLength]=snakeX[snakeLength-1]+x;
		map[snakeY[snakeLength]][snakeX[snakeLength]]='H';	
		snakeLength++;
		put_money();
		return;
	}
	map[snakeY[0]][snakeX[0]] = ' ';
	int i;
	
	for(i=0;i<snakeLength-1;i++){
		snakeX[i]=snakeX[i+1];
		snakeY[i]=snakeY[i+1];
		map[snakeY[i]][snakeX[i]] = 'X';
	}
	snakeX[snakeLength-1]+=x;
	snakeY[snakeLength-1]+=y;
	map[snakeY[snakeLength-1]][snakeX[snakeLength-1]] = 'H';
	
}

void output(void){
	int x,y;
	for(y=0;y<12;y++){
		for(x=0;x<12;x++){
			printf("%c",map[y][x]);
		}
		printf("\n");
	}
	
	
}

void put_money(void){
    int x, y; 
    while (1) { 
        x = (int)(15 * rand() / (RAND_MAX + 1.0));  
        y = (int)(15 * rand() / (RAND_MAX + 1.0)); 
        if (map[y][x] == ' ') {  
            map[y][x] = '$'; 
            break; 
        } 
    } 

}
```