# 链表
## 题目
判断一个单链表中是否有环

解题语言不限(其实本身JAVA和C++方便理解这种类型的，因为涉及到指针)：  

解题思路：

链表中有没有环就是使用指针去遍历，是永远走不到头的。因此我们可以想象成2个人一起跑步，如果一个人跑的慢，一个人跑的快，如果是有环，那么终究在一个时刻跑的快的会追上  
慢的，指针也是类似，一个走两步，一个走一步，判断是否可以相遇，时间复杂度为O(n)

定义节点：

```php
class ListNode {
      private $val;
      private $next = NULL;
      
      function __construct($x) {
          $this->val = $x;
      }
}
```

### 利用快慢指针 
```php
public function EntryNodeOfLoop($phead){  
    if($pHead == NULL || $pHead->next == NULL) {
        return false;
    }
    $pFast = $pHead->next->next;//快指针每次前进两步
    $pSlow = $pHead->next;//慢指针每次前进一步
    while(pFast != NULL && $pSlow != NULL) {
        if ($pFast === $pSlow) {
            return true;
        }
        $pFast = $pHead->next->next;
        $pSlow = $pHead->next;
    }
    return false;
}  
```

## 延伸题目
我们已经判断了链表中有没有环，那如果有环，是不是可能有延伸找出入口？

解题思路：

确实有环的情况下，关于找到找到环的入口点的问题，当fast若与slow相遇时，slow肯定没有走遍历完链表，而fast已经在环内循环了n圈(1<=n)。  
假设slow走了s步，则fast走了2s步（fast步数还等于s 加上在环上多转的n圈），设环长为r，则：

2s = s + nr  
s= nr  

设整个链表长L，入口环与相遇点距离为x，起点到环入口点的距离为a  

a + x = nr  
a + x = (n – 1)r +r = (n-1)r + L - a  
a = (n-1)r + (L – a – x)  

(L – a – x)为相遇点到环入口点的距离，由此可知，从链表头到环入口点等于(n-1)循环内环+相遇点到环入口点，  
于是我们从链表头、与相遇点分别设一个指针，每次各走一步，两个指针必定相遇，且相遇第一点为环入口点。程序描述如下  


```php
public function FindLoopPort($phead){  
    if($pHead == NULL || $pHead->next == NULL) {
        return false;
    }
    $pFast = $pHead->next->next;//快指针每次前进两步
    $pSlow = $pHead->next;//慢指针每次前进一步
    while(pFast != NULL && $pSlow != NULL) {
        if ($pFast === $pSlow) {
            break;
        }
        $pFast = $pHead->next->next;
        $pSlow = $pHead->next;
    }
    $pSlow = $pFast;
    while($pSlow != $pFast) {
        $pFast = $pHead->next;
        $pSlow = $pHead->next;
    }
    return $pSlow;
}  
```

## 做题总结
这种类型的需要我们灵活使用指针去思考和解决问题

## 需要思考的知道点
* 判断两个单链表是否相交
* 因为常规情况下感觉和环有类似的地方，其实如果2个单链表相交，那就肯定一个事情，两个链表都不存在环。

