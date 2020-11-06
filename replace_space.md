## 问题描述
请实现一个函数，把字符串 s 中的每个空格替换成 "%20"
```
输入：s = "We are happy."
输出："We%20are%20happy."
```

## 利用字符串中现有的方法
```
public String replaceSpace(String s) {
    return s.replaceAll(" ", "%20");
}
```
在面试的过程中，面试官不会让你直接使用方法，而是让你造

## StringBuilder
首先，我们肯定要遍历一遍字符串的所有字符，因为每个字符都有可能为空。接下来就是考虑当遇到空字符的时候，我们该怎么处理，最直接的想法当然是将空字符串直接替换为 %20，但是 Java 中的字符串是不变的，
所以直接替换是不行的。Java 中有个 StringBuilder 是表达可变的字符串的。
```
public String replaceSpace(String s) {
   StringBuilder sb = new StringBuilder();
   for (char c : s.toCharArray()) {
       if (c == ' ') sb.append("%20");
       else sb.append(c);
   }
   return sb.toString();
}
```
* 初始化一个 StringBuilder 实例 sb
* 遍历字符串 s 的每个字符. 当遍历到非空字符的时候，直接将字符 append 到 sb 中;如果遍历到的是空字符，那么将 %20 append 到 sb 中;
* 返回 sb.toString
对应的时间和空间复杂度均为O（n）

## 数组
StringBuilder的本质是一个char类型的动态数组
* 当初始化 StringBuilder 的时候，会初始化一个固定长度的 char 类型的数组
* 当往 StringBuilder 中 append 数据的时候，其实就是往 char 类型的数组最后追加数据

当追加的元素大于数组的长度的时候就需要动态扩容了，这时候就损耗性能了。 下面用静态数组来处理下这个问题。
```
public String replaceSpace(String s) {
    int n = s.length();
    char[] newArr = new char[3 * n];
    int j = 0;
    for (int i = 0; i < n; i++) {
        char c = s.charAt(i);
        if (c == ' ') {
            newArr[j++] = '%';
            newArr[j++] = '2';
            newArr[j++] = '0';
        } else {
            newArr[j++] = c;
        }
    }
    return new String(newArr, 0, j);
}
```
