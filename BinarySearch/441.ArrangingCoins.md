# 441. Arranging Coins 安排硬币

### 解法1

```java
    /*
    每次加一整行（每递增一行，行中的个数都+1），一旦求和超出了给定的n，则返回上一行的行数
     */
    public static int arrangeCoins(int n) {
        int i = 1;
        int sum = 0;
        while (sum <= n) {
            sum = sum + i++;
        }
        return i - 2;
    }
```



### 解法2

```java
    /*
    主体思想：对行数进行二分查找，判断条件为求和公式

    求和公式
    (x * ( x + 1)) / 2 = n
    (x^2 + x) /2  = n
    */
    public static int arrangeCoins2(int n) {
        int start = 0;
        int end = n;
        int mid = 0;

        while (start <= end) {
            mid = (start + end) >>> 1;
            if ((0.5 * mid * mid + 0.5 * mid) <= n) { //这里没有溢出问题，再计算时，自动装箱为double
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }
        return start - 1;
        /*
        返回值为start-1，当n值处于两个公式值（行数计算）中间时，要确保返回较小的那个行数
        代码中，无论是<还是= ，都将start+1了
         */
    }
```

### 解法3

```java
    /*
    (x * ( x + 1)) / 2 <= n
    求根公式得出
    x = 1 / 2 * (-sqrt(8 * n + 1)-1) (负数，抛弃) or  x = 1 / 2 * (sqrt(8 * n + 1)-1)

    注意代码为8.0*n隐式自动装箱为double,不会出现溢出现象
    8*n 当n=Integer.MAX_VALUE，则会不正确了
     */
    public static int arrangeCoins3(int n) {
        return (int) ((Math.sqrt(1 + 8.0 * n) - 1) / 2);
    }
```



![](/assets/576949164908537716.jpg)







