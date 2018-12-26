智能蛇是字符串版贪吃蛇的升级版。在这篇文章中，我将记录我的学习过程，起到同大家分享、交流的目的。    
  本次项目的任务是让蛇有一定的智能，能通过算法具有 “感知 - 决策 - 行动” 的能力。    
## 先是普通字符版贪吃蛇的伪代码。 
```
输出字符矩阵
    WHILE not 游戏结束 DO
        wait(time)
        ch＝whereGoNext(Hx,Hy,Fx,Fy)
        CASE ch DO
        ‘A’:左前进一步，break 
        ‘D’:右前进一步，break    
        ‘W’:上前进一步，break    
        ‘S’:下前进一步，break    
        END CASE
        输出字符矩阵
    END WHILE
    输出 Game Over!!! 
```
## 接下来就是蛇智能行走的算法了
```c
 // Hx,Hy: 头的位置
    // Fx,Fy：食物的位置
    function whereGoNext(Hx,Hy,Fx,Fy) {
    // 用数组movable[3]={“a”,”d”,”w”,”s”} 记录可走的方向
    // 用数组distance[3]={0,0,0,0} 记录离食物的距离
    // 分别计算蛇头周边四个位置到食物的距离。H头的位置，F食物位置
    //     例如：假设输入”a” 则distance[0] = |Fx – (Hx-1)| + |Fy – Hy|
    //           如果 Hx-1，Hy 位置不是Blank，则 distance[0] = 9999
    // 选择distance中存最小距离的下标p，注意最小距离不能是9999
    // 返回 movable[p]
    }
```c
## c语言实现
#include<stdio.h>
#include<stdlib.h>
#include<time.h>
#include<conio.h>
#include<windows.h>
# define SNAKE_MAX_LENGTH 100
#define SNAKE_HEAD 'H'
#define SNAKE_BODY 'X'
#define BLANK_CELL ' '
#define SNAKE_FOOD '$'
#define WALL_CELL '*'
char map[12][13] = {
    "************",
    "*H         *",
    "*          *",
    "*          *",
    "*          *",
    "*          *",
    "*          *",
    "*          *",
    "*          *",
    "*          *",
    "*          *",
    "************",
};

int snakeHeadX = 1, snakeHeadY = 1;
int snakeBodyX[SNAKE_MAX_LENGTH] = { 0 }, snakeBodyY[SNAKE_MAX_LENGTH] = { 0 };
int snakeBodyLen = 1;
int FoodX = 0, FoodY = 0;
int gameRunning = 1;
void gameover(void)
{
    gameRunning = 0;
    printf("Game Over!");
}
void putFood(void)
{
    srand(time(NULL));
    FoodX = rand() % 10 + 1;
    FoodY = rand() % 10 + 1;
    while (map[FoodX][FoodY] != BLANK_CELL)
    {
        FoodX = rand() % 10 + 1;
        FoodY = rand() % 10 + 1;
    }
    map[FoodX][FoodY] = SNAKE_FOOD;
}
char move(int Hx,int Hy,int Fx, int Fy)
{
    char movable[4] = { 'w','a','s','d' };
    int distance[4] = { 0 };
    int i, min = 0;
    if (map[Hx-1][Hy] != WALL_CELL&&map[Hx-1][Hy] != SNAKE_BODY)
        distance[0] = abs(Fx - (Hx-1)) + abs(Fy - Hy);
    else
        distance[0] = 9999;
    if (map[Hx][Hy-1]!=WALL_CELL&&map[Hx][Hy-1] != SNAKE_BODY)
        distance[1] = abs(Fx - Hx) + abs(Fy - (Hy-1));
    else
        distance[1] = 9999;
    if (map[Hx+1][Hy]!=WALL_CELL&&map[Hx+1][Hy] != SNAKE_BODY)
        distance[2] = abs(Fx - (Hx+1)) + abs(Fy - Hy);
    else
        distance[2] = 9999;
    if (map[Hx][Hy+1] !=WALL_CELL&&map[Hx][Hy+1] != SNAKE_BODY)
        distance[3] = abs(Fx - Hx) + abs(Fy - (Hy+1));
    else
        distance[3] = 9999;
    for (i = 0; i < 4; i++)
        if (distance[i] < distance[min]&&distance[i]!=9999)
            min = i;
    return movable[min];
}
void snakeMove()
{
    char control = move(snakeHeadX, snakeHeadY, FoodX, FoodY);
    int preSnakeHeadX = snakeHeadX;
    int preSnakeHeadY = snakeHeadY;
    switch (control)
    {
    case 'w':
        snakeHeadX--;
        break;
    case 'a':
        snakeHeadY--;
        break;
    case 's':
        snakeHeadX++;
        break;
    case 'd':
        snakeHeadY++;
        break;
    default:
        break;
    }
    if (map[snakeHeadX][snakeHeadY] == WALL_CELL || map[snakeHeadX][snakeHeadY] == SNAKE_BODY)
        gameover();
    map[snakeHeadX][snakeHeadY] = SNAKE_HEAD;
    map[preSnakeHeadX][preSnakeHeadY] = BLANK_CELL;
    if (snakeHeadX == FoodX && snakeHeadY == FoodY)
    {
        snakeBodyX[snakeBodyLen] = preSnakeHeadX;
        snakeBodyY[snakeBodyLen] = preSnakeHeadY;
        snakeBodyLen++;
        map[preSnakeHeadX][preSnakeHeadY] = SNAKE_BODY;
        putFood();
        return;
    }
    if (snakeBodyLen <= 0)
        return;
    int i;
    for (i = 0; i < snakeBodyLen - 1; i++)
    {
        snakeBodyX[i] = snakeBodyX[i + 1];
        snakeBodyY[i] = snakeBodyY[i + 1];
    }
    snakeBodyX[snakeBodyLen - 1] = preSnakeHeadX;
    snakeBodyY[snakeBodyLen - 1] = preSnakeHeadY;
    int j;
    for (j = 0; j < snakeBodyLen; j++)
        map[snakeBodyX[j]][snakeBodyY[j]] = SNAKE_BODY;
    map[snakeBodyX[0]][snakeBodyY[0]] = BLANK_CELL;
}
void printMap(void)
{
    system("cls");
    int i = 0;
    for (i = 0; i < 12; i++)
        printf("%s\n", map[i]);
}
int main()
{
    putFood();
    printMap();
    while (gameRunning)
    {
        snakeMove();
        printMap();
        Sleep(100);
    }
    return 0;
}
```