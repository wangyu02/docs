# 链表

- 什么是单链表？

  1. 链表不像数组那样将数组存储在一个连续的存储空间地址里面，它可以不是连续的因为他的每个节点保存着下一个节点的引用(地址)。

     ````java
     public class Node {
         int value;
         Node next;
         public void Node(int value) {
             this.value = value;
         }
     }
     ````

  2. 链表的特点

     ````wi
     链表删除一个元素的时间复杂度是：o(1),查找一个元素的时间复杂度是o(n)
     单链表无需像数组那样预先分配存储空间的大小，避免了空间浪费
     当链表不能进行回溯操作，如：只知道链表的头节点的时候无法快读快速链表的倒数第几个节点的值。
     ````

     ----

     

- 链表的建单操作

  1. 获取链表的长度：

     ````java
     public int getLength(Node head) {
         if(head == null) {
             return 0;
         }
         int len = 0;
         while(head != null){
             len++;
             head = head.next;
         }
         return len;
     }
     ````

  2. 查询指定索引的节点或制定值得节点值的索引

     根据链表的特性，我们是无法通过索引值获取索引的位置元素，所以链表的查询时间的复杂度是o(n)级别的。

     ````java
     // 获取指定角标的节点值
     public int getValueOfIndex(Node head, int index) {
         if(index < 0 || index >= getLength(head)) {
             throws new Exception("角标越界")；
         }
         if(head == null){
             throw new Exception("当前链表为null");
         }
         Node dummyHead = head;
         while(dummy.next != null && index > 0){
             dummyHead = dummyHead.next;
             index--;
         }
         return dummyHead.value;
     }
     ````

     ````java
     // 获取节点值等于value的第一个元素角标
     public int getNodeIndex(Node head, int value) {
         int index = -1;
         Node dummyHead = head;
         while(dummyHead != null){
             index++;
             if(dummyHead.value == value){
                 return value;
             }
             dummyHead = dummyHead.next;
         }
         return -1;
     }
     ````

  3. 链表添加一个元素

     如果我们只知道一个链表的头节点的情况下去插入一个元素，就不是很简单就能解决问题了，对于头插入法我们只需要构造一个新的节点，让后将这个节点的next 指针执行已知链表的头结点就可以了

     ````java
     // 在已有链表头部插入一个节点
     public Node addAtHead(Node head, int value) {
         Node newHead = new Head(value);
         newHead.next = head;
         return newHead;
     }
     ````

     ````java
     //在已有链表的尾部插入一个节点
     public Node addAtTail(Node head， int value){
         Node node = new Node(value);
         Node dummyHead = head;
         // 找到链表尾巴
         while(dummyHead.next != null){
             dummyHead = dummyHead.next;
         }
         dummyHead.next = node;
     }
     ````

     ````java
     // 在给定位置添加一个节点
     // 找到这个索引所在的节点前一个以及该节点，分别记录这两个节点，然后将索引所在节点的前一个节点的next指针指向新节点，将新节点的next指针执行插入节点既可。
     public Node insertElement(Node node, int value, int index) {
         int len = getLength(head);
         if(index < 0 || index >= length){
             throw new Exception("角标越界");
         }
         if(index == 0){
             return addAtHead(head, value);
         } else if(index == length -1){
             return addAtTail(head, value);
         } else {
             Node pro = head;
             Node current = head.next;
             while(pre != null && index > 1){
                 pre = pre.next;
                 cur = cur.next;
                 index--;
             }
             // pre保存的是索引的上一个节点，cur保存的是索引值当前的节点
             Node node = new Node(value);
             pre.next = node;
             node.next = cur;
         }
         return head;
     }
     ````

  4. 链表删除一个元素

     ````java
     // 在链表头部删除一个元素
     public Node deleteHead(Node head){
         if(head == null) {
             throw new Exception("当前链表为空")；
         }
         return head.next;
     }
     ````

     ````java
     // 删除链表尾节点的元素
     public Node deleteTail(Node node) {
         if(head == null) {
             throw new Exception("当前链表为null");
         }
         Node dummyNode = node;
         while(dummyNode.next != null && dummyNode.next.next != null) {
             dummyNode = dummyNode.next;
         }
         dummyNode.next = null;
     }
     ````

     ````java
     // 在表单中删除一个元素
     public Node deleteElement(Node head, int index) {
         int size = getLength(head);
         if(index < 0 || index > size){
             throw new Exception("角标越界线");
         }
         if(index == 0) {
             return deleteHead(head);
         } else if(index == size - 1){
             return deleteTail(head);
         } else {
             Node pre = head;
             while(pre.next != null && index > 1){
                 pre = pre.next;
                 index--;
             }
             if(pre.next != null) {
                 pre.next = pre.next.next;
             }
         }
         return head;
     }
     ````
     
     链表想要对指定索引进行操作(增加和删除)的时候，必须获取该索引的前一个元素。

- 单链表操作中常见的面试题：

  1. 寻找链表的中间元素 -- 快慢指针的方式

     设置两个slow、fast 起始都指向单链表的头节点，其中fast的移动速度是slow的2倍，当fast指向为尾节点的时候，slow刚好在中间了。

     ````java
     public Node getMid(Node head) {
         if(head == null){
             return null;
         }
         Node slow = head;
         Node fast = head;
         
         while(fast != null && fast.next != null){
             fast = fast.next.next;
             slow = slow.next;
         }
         return slow;
     }
     ````

  2. 判断一个链表是否是循环链表

     什么是循环链表：单链表的尾部指针指向了头指针，构成了一个环形的链表

     A的速度快，B的速度慢，经过一定时间后，A总是回合B相遇的，且相遇时A跑过的总距离减去B跑过的总距离一定是圈长的n倍，这样的方法就是Floyd判环算法。

     ````java
     public static boolean isLoopList(Node node) {
         if(head == null){
             return false;
         }
         Node slow = head;
         Node fast = head.next;
         
         while(slow != null && fast != null && fast.next != null){
             if(fast == slow || fast.next == slow){
                 return true;
             }
             fast = fast.next.next;
             slow = slow.next;
         }
         return false;
     }
     ````

  3. 删除单链表求倒数第N个节点

     操作链表的某个节点就必须知道他的前一个节点，所以删除倒数第n个元素就要找到倒数第n+1个元素，然后将倒数第n+1个元素P的next指针p.next指向p.next.next.

     找到倒数第n个节点的时候，先让fast先走了n-1步，那么我们删除倒数第n个节点的时候就需要让fast先走n步，构建一个n+1大小的窗口，然后fast和slow整体平移到链表尾部，slow指向的节点就是倒数第n+1个节点。

     ````java
      public Node deleteLastNNode(Node head, int n){
          if(head == null || n < 1){
              return head;
          }
          // head 走到第n-1个节点
          Node fast = head;
          for(int i=0; i < n;i++){
              if(fast == null){
                  return head;
              } else {
                  fast = fast.next;
              }
          }
          if(fast == null){
              return head.next;
          }
          // fast先走了n步骤
          Node pre = head;
          while(fast.next != null){
              fast = fast.next;
              pre = pre.next;
          }
          // 经过上面的循环，fast走到了尾节点，pre走到了第k个节点，之后完成删除的操作。
          pre.next = pre.next.next;
          return head;
      }
     ````

  4. 旋转单链表

     该题目的本质就是将其变成尾节点，然后原来链表的尾节点指向原来的头结点

     ````java
     public Node rotateList(Node head, int n){
         int start = 1;
         Node fast = head;
         while(start < n && fast.next != null){
             fast = fast.next;
             start++;
         }
         if(fast.next == null || start < n){
             return head;
         }
         Node pre = fast;
         Node newHead = fast.next;
         while(fast.next != null){
             fast = fast.null;
         }
         fast.next = head;
         pre.next = null;
         return newHead;
     }
     ````

     

     

  