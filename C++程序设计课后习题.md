# 程序设计初步

## 1.最大公约数和最大公倍数

```
#include<stdio.h>
#include<iostream>
using namespace std;

int gcd(int a,int b){
     if(b == 0)  return a;
     return gcd(b,a % b);
}

int main()
{
     int a,b;
     scanf("%d%d",&a,&b);
     printf("%d\n",gcd(a,b));
     printf("%d\n",a * b / gcd(a,b));
     return 0;
}
```
## 2.求 a + aa + aaa + ... 的值，a 是一个数字

```
#include<stdio.h>
#include<iostream>
using namespace std;

int main()
{
     int n;
     scanf("%d",&n);
     int ans = 0;
     int a = 0;
     for(int i = 0;i < n;i++){
          a = a * 10 + 2;
          ans += a;
    }
    printf("%d\n",ans);
    return 0;
```
## 3.阶乘求和

```
#include<stdio.h>
#include<iostream>
using namespace std;
​
int main()
{
      int a[20] = {0};
      a[0] = 1;
      int ans = 0;
      for(int i = 1;i < 20;i++){
            a[i] = a[i - 1] * (i + 1);
      }
      for(int i = 0; i < 20;i++){
            ans += a[i];
      }
      printf("%d\n",ans);
      return 0;
}
```
## 4.水仙花数

```
#include<stdio.h>
#include<iostream>
using namespace std;
​
int main()
{
      int n;
      scanf("%d",&n);
      int a = n % 10;
      int b = n / 10 % 10;
      int c = n / 100;
      if(a * a * a + b * b * b + c * c* c == n)
            printf("yes\n");
      else
            printf("no\n");
      return 0;
}
```
## 5.分数序列之和。2 / 1 + 2 / 3 + 5 / 3 + 8 / 5 + 13 / 8 + 21 / 13 + ...

```
#include<stdio.h>
#include<math.h>
#include<iostream>
#include<vector>
using namespace std;
int main()
{
      double a = 1,b = 2;
      double ans = 0;
      for(int i = 0;i < 20;i++){
            ans += b / a;
            int temp = a;
            a = b;
            b = a + temp;
      }
      printf("%.2f\n",ans);
      return 0;
}
```
## 6.猴子吃桃

```
#include<stdio.h>
#include<math.h>
#include<iostream>
#include<vector>
using namespace std;
int main()
{
      int ans = 1;
      int n;
      scanf("%d",&n);
      for(int i = 0;i < n - 1;i++){
            ans = (ans + 1) * 2;
      }
      printf("%d\n",ans);
      return 0;
}
```
## 7.用迭代法求平方根

```
#include<stdio.h>
#include<math.h>
#include<iostream>
#include<vector>
using namespace std;
​
int main()
{
      double a;
      scanf("%lf",&a);
      double x1,x2;
      x2 = 1.0; // x 的初值为 1
      while(true){
            x1 = x2;
            x2 = (x1 + a / x1) / 2;
            if(fabs(x1 - x2) < 0.00001){
                  printf("%lf\n",x2);
                  break;
            }
      }
      return 0;
}
```
# 函数

## 1.用牛顿迭代法求根

```
#include<stdio.h>
#include<math.h>
#include<iostream>
#include<vector>
using namespace std;
​
/*
牛顿迭代法原理
*/
int main()
{
      double x,f,a,b,c,d;
      scanf("%lf%lf%lf%lf",&a,&b,&c,&d);
​
      x = 1;
      while(true){
            f = (a * x * x * x + b * x * x + c * x + d) / (3 * a * x * x + 2 * b * x + c);
            if(fabs(f) < 1e-5)
                  break;
            x -= f;
      }
      printf("%lf\n",x);
      return 0;
}
```
## 2.汉诺塔问题

```
#include<stdio.h>
#include<math.h>
#include<iostream>
#include<vector>
using namespace std;
/*
递归求解汉诺塔问题
*/
int c = 0; //全局变量，对搬动计数
void hanoi(int n,char x,char y,char z);
int main()
{
      int a;
      scanf("%d\n",&a);
      hanoi(a,'A','B','C');
      return 0;
}
void hanoi(int n,char x,char y,char z){
      if(n == 1)
            printf("%d. Move Disk %d from %c to %c\n",++c,n,x,z);
      else{
            hanoi(n - 1,x,z,y); //将 x 上编号为 1 至 n-1 的圆盘移到 y,z 作辅助塔
            printf("%d. Move Disk %d from %c to %c\n",++c,n,x,z); //将编号为 n 的圆盘从 x 移到 z;
            hanoi(n - 1,y,x,z);
      }
}
```
## 3.用递归法将一个整数转换成字符串

```
#include<stdio.h>
#include<math.h>
#include<string.h>
#include<iostream>
#include<vector>
using namespace std;
/*
递归数字变字符串
*/
void change(int n);
char str[100];
int index = 0;
int main()
{
      int a;
      scanf("%d",&a);
      change(a);
      for(int i = strlen(str) - 1;i >= 0;i--){
            printf("%c",str[i]);
      }
      printf("\n");
      return 0;
}
void change(int n){
      if(n == 0){
            return;
      }
      char c = (n % 10) + '0';
      str[index++] = c;
      change(n / 10);
}
```
## 4.用递归方法求 1 ^ 2 + 2 ^ 2 + ... + n ^ 2;

```
#include<stdio.h>
#include<math.h>
#include<string.h>
#include<iostream>
using namespace std;
int f(int i);
int main()
{
      int n;
      scanf("%d",&n);
      printf("%d",f(n));
      return 0;
}
int f(int i){
      if(i == 1){
            return 1;
      }
      return f(i - 1) + (i * i);
}
```
# 数组

## 1.素数筛法求 100 内的素数

```
#include<stdio.h>
#include<math.h>
#include<string.h>
#include<iostream>
using namespace std;
const int maxn = 100;
bool mark[maxn] = {0};
int prime[maxn];
int primeSize = 0;
void find_prime(){
      //素数筛法
      for(int i = 2;i < maxn;i++){
            if(!mark[i]){
                  prime[primeSize++] = i;
                  //把素数的整数倍标记
                  for(int j = i * i;j < maxn;j += i){
                        mark[j] = true;
                  }
            }
      }
}
int main()
{
      find_prime();
      for(int i = 0;i < primeSize;i++){
            printf("%d ",prime[i]);
      }
      printf("\n");
}
```
## 2.杨辉三角

```
#include <stdio.h>
int n;
int GetYHTriangle(int i,int j){
    if(j==0 || i==j)
        return 1;
    else
        return GetYHTriangle(i-1,j-1)+GetYHTriangle(i-1,j);
}
int main(){
    int i,j;
    while(scanf("%d",&n)!=EOF){
        for(i=0;i<n;i++){
            for(j=0;j<i;j++)
                printf("%d ",GetYHTriangle(i,j));
            printf("%d\n",GetYHTriangle(i,i));
        }
    }
    return 0;
}
```
## 3.鞍点

```
#include <stdio.h>
int main(){
      int row = 3;
      int column = 3;
      int a[row][column] = {
            {2,3,4},
            {1,7,5},
            {8,9,6}
      };
      bool flag = true;
      for(int i = 0;i < row;i++){
            //先找出每行的最大值，再验证该数是否在列上最小
            int max = a[i][0], max_j = 0;
            for(int j = 0; j < column;j++){
                  if(a[i][j] > max){
                        max = a[i][j];
                        max_j = j;
                  }
            }
            for(int k = 0;k < row;k++){
                  if(max > a[k][max_j])
                        flag = false;
            }
            if(flag)
                  printf("鞍点的坐标为（%d,%d），鞍点的值为 %d\n",i,max_j
                         ,a[i][max_j]);
      }
      return 0;
}
```
## 4.今年的第几天

```
#include <stdio.h>
bool isRunNian(int year){
      return (year % 4 == 0 && year % 100 != 0) || (year % 400 == 0);
}
int main(){
      int month[13] = {0,31,28,31,30,31,30,31,31,30,31,30,31};
      int y,m,d;
      while(scanf("%d%d%d",&y,&m,&d) != EOF){
            if(isRunNian(y))
                  month[2]  = 29;
            int ans = 0;
            for(int i = 1; i < m;i++){
                  ans += month[i];
            }
            ans += d;
            printf("%d\n",ans);
      }
}
```

