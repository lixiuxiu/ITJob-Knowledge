通过new Scanner(System.in)创建一个Scanner，控制台会一直等待输入，直到敲回车键结束，把所输入的内容传给Scanner，作为扫描对象。

如果要获取输入的内容，获取一行需要调用Scanner的nextLine()方法，

# Scanner常用API

delimiter() 返回此 Scanner 当前正在用于匹配分隔符的 Pattern。

hasNext() 判断扫描器中当前扫描位置后是否还存在下一段，默认以一个或多个连续的空格作为段的分隔符。

hasNextLine() 如果在此扫描器的输入中存在另一行（以回车作为”分行符”），则返回 true。

next() 查找并返回来自此扫描器的下一个完整标记（取得输入段）。

nextLine() 此扫描器执行当前行，并返回跳过的输入信息(取得输入行文本)。

# 实例

## 1.第一行输入一个整数n，后面输入n行

（1）每行3个整数

```java
public static void main(String[] args){
        Scanner in=new Scanner(System.in);
        int n=in.nextInt();
        int[][] games=new int[n][3];
        for (int i=0;i<n;i++){
            games[i][0]=in.nextInt();
            games[i][1]=in.nextInt();
            games[i][2]=in.nextInt();
        }
        System.out.println("A");
}

3
1 2 2
1 2 3
2 3 4
A
```

（2）每行一个字符串

```java
public static void main(String[] args){
        Scanner in=new Scanner(System.in);
        int n=in.nextInt();
        int[] S=new int[n];
        for (int i = 0; i < m; i++) {
            S[i] = sc.nextLine();
        }
}
```

