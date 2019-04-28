编程tips

### 1.TreeSet

```java
import java.util.*;

public class huawei {

    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);
        while(sc.hasNext()){
            //即可以空格分割，也可以换行分割
            int num = sc.nextInt();
          
            //有序无重复的集合，在要求输出不重复且从大到小排列时可以使用
            TreeSet<Integer> set = new TreeSet<Integer>();
            for(int i = 0 ; i < num ;i++){
                int curr = sc.nextInt();
                set.add(curr);
            }
            for(Integer i : set){
                System.out.println(i);
            }
        }
    }
}
```

### 2.substring

按下标切割数组，split按特定字符切割字符串成字符串数组。

```java
s1=s2.substring(0,8);
s2=s2.substring(8); //8到字符串结尾
```

### 3. 字符串类型转化为整形

```java
String str="16";
Integer.parseInt(str);

String str="A";
Integer.parseInt(str,16);//把16进制表示的A转化为10进制，结果为10
```

### 4.替换字符串的某些字符

```java
String newStr=str.replace(" ","%20");//replace可以替换字符，或者其中的部分字符串
//而且替换后的字符串是一个新的字符串，旧字符串的值没有变化
```

### 5.char[] 型转化为string

不能用ch.toString()，显示的不是字符串本身，用下面的

```java
new String(ch)
```

### 6.list.remove();

```java
ArrayList<Integer> temp=new ArrayList<>(list);
res.add(temp); //直接把list加入另一个lists里面，再改变list里面的值，lists里面的值也会改变

//remove()这个方法是一个重载方法，即remove(int position)和remove(object object)，唯一的区别是参数类型。要密切注意自己调用的remove()方法中的，传入的是int类型还是一个对象。
//使用remove(int position)的方法时，要先从大到小的位置移除，否则下标变化之后下面一次移除可能会数组越界。当然如果你知道具体的对象，直接移除remove(对象)更稳妥。
list.remove(new Integer(l));
```

### 7.类作为参数传入方法

java中都是值传递，类传入的时候传入的是这个类的一个地址副本，指向原来的类，使用地址副本改变地址里面的内容的操作会影响原来的类，如果对地址副本赋上new的对象的新地址，则不会对原来的对象造成影响。

```java
private TreeNode ret;
private int cnt = 0;

//第一种可以正常运行
private void inOrder(TreeNode root, int k) {
    if (root == null || cnt >= k)
        return;
    inOrder(root.left, k);
    cnt++;
    if (cnt == k)
        ret = root;  //需要改变类的指向，就不要用参数传进来，而是全局变量
    inOrder(root.right, k);
}
```

### 8.求数字的开根号和次方

```java
int a=(int) Math.sqrt(n);//n开根号
int b=(int) Math.pow(n,m);//n的m次方
```

### 9.比较大小

（1）字符串比较大小

字符串比较长度，长度相等再比较ASCII码，前面小于后面，结果为负值。

```java
//如果str1比str2长度小，或者是长度相等，但是ascii码比较小
if（str1.compareTo(str2) < 0）
```

（2）Java的Arrays类中有一个sort()方法，该方法是Arrays类的静态方法，在需要对数组进行排序时，非常的好用。但是sort()的参数有好几种

```java
Integer[] a = {9, 8, 7, 2, 3, 4, 1, 0, 6, 5};
Arrays.sort(a);//从小到大排序
Arrays.sort(a, 0, 3);//只对数组的0，1，2 三位从小到大排序，其余不变
Comparator cmp = new MyComparator(); //自定义比较类对象
Arrays.sort(a, cmp); //使用这个规则的比较排序
```

```java
class MyComparator implements Comparator<Integer>{
     @Override
     public int compare(Integer o1, Integer o2) {
        //如果o1小于o2，我们就返回正值，如果o1大于o2我们就返回负值，
         //这样颠倒一下，就可以实现反向排序了
         if(o1 < o2) { 
             return 1;
         }else if(o1 > o2) {
             return -1;
         }else {
             return 0;
         }
     }
}
```

字符串s1和s2如何组合使得assic码最小

```java
Arrays.sort(nums, (s1, s2) -> (s1 + s2).compareTo(s2 + s1));
```

```java
//字符串从小到大排序
Arrays.sort(strArray, Collections.reverseOrder()); 
```

