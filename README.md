#include <stdio.h>
int a[9][9];
 
int place(int x, int y) //二者分别是数组对应的行地址和列地址，取值为0-8
{
int up, down, left, right;
int i,j;
 
up=x/3*3;
down=up+3;
 
left=y/3*3;
right=left+3;
 
//以下分三种情况判断是否在x,y对应的位置放这个数，如果不可以放，返回0，如果可以放，返回1，会进一步迭代

for(i=0;i<9;i++){
if(a[x][y]==a[i][y] && i!=x && a[i][y]!=0)
return 0;
}
 
for(i=0;i<9;i++){
if (a[x][y]==a[x][i] && i!=y && a[x][i]!=0)
return 0;
}
 
for(i=up;i<down;i++)
{
for(j=left;j<right;j++)
if(i!=x || j!=y)
{
if(a[i][j]==a[x][y] && a[i][j]!=0)
return 0;
}
}
 
return 1;
}
 
 
void backtrack(int t)
{
int i,j;
int x,y;
 
if(t==81)
{
printf("\n=============================\n");
for(i=0;i<9;i++)
{
for(j=0;j<9;j++)
printf("%d",a[i][j]);
 
putchar('\n');
}
}
else
{
x=t/9;
y=t%9; //将这个转换为相应的数组行坐标和列坐标
 
if(a[x][y]!=0)
{
backtrack(t+1);
}
else
{
for(i=1;i<10;i++)
{
a[x][y]=i;
if(place(x,y)==1)
backtrack(t+1);
a[x][y]=0;
}
}
}
}
 
int main()
{
char str[9][9];
int i,j;
 
for(i=0;i<9;i++)
gets(str[i]);
 
for(i=0;i<9;i++)
for(j=0;j<9;j++)
a[i][j]=str[i][j]-'0';

backtrack(0);
 
return 0;
 
}
