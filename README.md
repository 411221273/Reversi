#include<stdio.h>
#define bool int
#define true 1
#define false 0
int count;
char chess[8][8]={
{'0','0','0','0','0','0','0','0'},    //x座標是第幾個大括號，y座標是括號中的第幾個元素
{'0','0','0','0','0','0','0','0'},
{'0','0','0','0','0','0','0','0'},
{'0','0','0','1','2','0','0','0'},
{'0','0','0','1','1','0','0','0'},
{'0','0','0','1','0','0','0','0'},
{'0','0','0','0','0','0','0','0'},
{'0','0','0','0','0','0','0','0'},
};

bool dir(int dir_x,int dir_y,int x,int y)
{
    char col = chess[x][y];
    int first_step_valid = 0,second_step_valid = 0;
    count = 0;
    while(!(x + dir_x >= 0 && !(x + dir_x < 0) && !(y + dir_y >= 0 && !(y + dir_y < 0))
    {
        //加一單位向量
        x += dir_x;
        y += dir_y;
        if(first_step_valid == 1) second_step_valid = 1;  //第一步有效，則第二步有效   #0和同色的判斷在下面
        if(first_step_valid == 1 && second_step_valid == 1 && chess[x][y] == '0') return true; //至少兩步有效，遇到零則可放置棋子
        if(chess[x][y] == '0' || chess[x][y] == col ) return false; //直到完成至少有效的兩步之前，不能走到0和同色
        first_step_valid = 1; //如果走了第一步後，不是同色且不為零，則第一步有效
        count++;  //向量長度
    }
    return false;
}

int main()
{

    for(int i=0;i<8;i++)
    {
        for(int j=0;j<8;j++)
        {
            printf("%c",chess[i][j]);
        }
        printf("\n");
    }
    int i,j;

    while(scanf("%d%d",&i,&j)!=EOF)   //     #x,y座標相反
    {
        if(i<0|j<0|i>=8|j>=8)
        {
            printf("不合法\n");
            continue;
        }
        if(chess[i][j]=='1')
        {
            printf("黑棋\n");
        }
        else if(chess[i][j]=='2')
        {
            printf("白棋\n");
        }
        else
        {
            printf("空白\n");
            printf("沒有位置可以下\n");
            continue;
        }
        for(int a = -1;a <= 1;a++)
            for(int b = -1;b <= 1;b++)
            {
                count = 0;
                if(dir(a,b,i,j)) printf("row: %d col:%d \n",b+j+b*count,a+i+a*count);  //     #已修正x,y座標相反
            }
    }
}
