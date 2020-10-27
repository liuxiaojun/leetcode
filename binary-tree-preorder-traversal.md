遍历二叉树的方法合集

## 递归解法
* 前序遍历
```
public static void preOrderRecur(TreeNode head) {
    if (head == null) {
        return;
    }
    System.out.print(head.value + " ");
    preOrderRecur(head.left);
    preOrderRecur(head.right);
}
```
* 中序遍历
```
public static void preOrderRecur(TreeNode head) {
    if (head == null) {
        return;
    }
    preOrderRecur(head.left);
    System.out.print(head.value + " ");
    preOrderRecur(head.right);
}
```
* 后序遍历
```
public static void postOrderRecur(TreeNode head) {
    if (head == null) {
        return;
    }
    postOrderRecur(head.left);
    postOrderRecur(head.right);
    System.out.print(head.value + " ");
}
```

## 迭代解法
本质上是模拟递归，因为在递归的过程中使用了系统栈，所以在迭代的解法中常用Stack来模拟系统栈。
* 前序遍历
TODO
