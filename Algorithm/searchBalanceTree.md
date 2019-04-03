# 遍历二叉树
## 题目
用任何语言实现二叉树的遍历(非递归)，注意有前序，中序，和后序三种方式

解题语言为PHP：  

给定一棵树，按照顺序他们依次为：  
* 前序遍历：ABCDEFGHK
* 中序遍历：BDCAEHGKF
* 后序遍历：DCBHKGFEA

解题思路：

利用栈的先进后出的特征，根据不同的遍历方式，对根节点和左右子树进行操作

定义节点：

```php
class Tree {
      public $val;
      public $left;
      public $right
}
```

### 前序遍历:先访问根节点，再遍历左子树，最后遍历右子树；并且在遍历左右子树时，仍需先遍历根节点，然后访问左子树，最后遍历右子树  
```php
public static function preOrder($root){  
    $stack = array();  
    array_push($stack, $root);  
    while(!empty($stack)){  
        $center_node = array_pop($stack);  
        echo $center_node->val . ' ';  

        //先把右子树节点入栈，以确保左子树节点先出栈  
        if($center_node->right != null) {
            array_push($stack, $center_node->right);
        }
        if($center_node->left != null) {
            array_push($stack, $center_node->child_left);
        }
    }  
}  
```
### 中序遍历:先遍历左子树、然后访问根节点，最后遍历右子树；并且在遍历左右子树的时候。仍然是先遍历左子树，然后访问根节点，最后遍历右子树  
```php
public static function midOrder($root){  
    $stack = array();  
    $center_node = $root;  
    while (!empty($stack) || $center_node != null) {  
        while ($center_node != null) {  
            array_push($stack, $center_node);  
            $center_node = $center_node->left;  
        }  

        $center_node = array_pop($stack);  
        echo $center_node->val . ' ';  

        $center_node = $center_node->right;  
    }  
}
```
### 后序遍历:先遍历左子树，然后遍历右子树，最后访问根节点；同样，在遍历左右子树的时候同样要先遍历左子树，然后遍历右子树，最后访问根节点  
```   php 
public static function endOrder($root){  
    $push_stack = array();  
    $visit_stack = array();  
    array_push($push_stack, $root);  

    while (!empty($push_stack)) {  
        $center_node = array_pop($push_stack);  
        array_push($visit_stack, $center_node);  
        //左子树节点先入$pushstack的栈，确保在$visitstack中先出栈  
        if ($center_node->left != null) {
            array_push($push_stack, $center_node->left);  
        }
        if ($center_node->right != null) {
            array_push($push_stack, $center_node->right);  
        }
    }  

    while (!empty($visit_stack)) {  
        $center_node = array_pop($visit_stack);  
        echo $center_node->val . ' ';  
    }  
}  
```

## 做题总结
虽然相对中序稍微难理解，但是我们利用栈内存模拟，相对很多人会对二叉树一些算法有一些好的认识，是不是在也觉得并不是多难对吗

## 需要思考的知道点
* 空间和时间复杂度  
* 有没有更好的优化  
* 待更新...
