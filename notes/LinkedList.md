## Definition  
链表是一种常见的数据结构，是通过指针串联在一起的线性非连续数据结构，意味着内存不连续。每一个节点Node由两部分组成，一个是数据域data，一个是指针域存放指向下一个节点的指针next，最后一个节点的指针域指向None（空指针的意思

head定义为链表的入口节点，头节点  
tail定义为链表的尾节点  

## Comparison
数组在定义的时候，长度就是固定的，如果想改动数组的长度，就需要重新定义一个新的数组。  
链表的长度可以是不固定的，并且可以动态增删， 适合数据量不固定，频繁增删，较少查询的场景。

## Type
链表的分类：单链表，双链表，循环链表  

## 单链表  
```python
# Node class
class Node():
    def __init__(self, value, next = None): # 每一个节点都包含值和一个next指针
        self.value = value
        self.next = next
        
# Linkedlist class
class linkedlist():
    def __init__(self): 
        self.__head = None # 初始化链表，头指针指向空
        self.__tail = None # 初始化链表，尾指针指向空
    
    def is_empty(self):
        """判断链表是否为空"""
        return self.__head is None
    
    def length(self):
        """返回链表长度"""
        cur = self.__head  # cur游标，用来移动遍历节点
        count = 0  # count记录节点数量
        while cur is not None:
            count += 1
            cur = cur.next
        return count

    def insert_head(self, value):
        """头插法：在单链表头部插入一个节点"""
        newnode = Node(value)  # 创建一个新节点
        if self.__head is not None:  # 如果初始链表不为空，就将新节点的"next"指针指向head
            newnode.next = self.__head # head指针本来指向原来的第一个节点，现在把他指向新节点
        self.__head = newnode  # 把新节点的地址设置为head指针的地址
        if self.__tail is None:
            self.__tail = newnode
            
    def insert_tail(self, value):
        """尾插法v1：在单链表尾部增加一个节点"""
        # 相当于遍历整个链表，时间复杂度较高 O(n)
        if self.__head is None:
            self.insert_head(value)  # 如果待插入节点是第一个节点，调用insert_head函数
        else:
            cur = self.__head
            while cur.next is not None:  # 遍历到最后一个节点
                cur = cur.next
            cur.next = Node(value)  # 创建新节点并连接到最后
            self.__tail = cur.next
    
    def insert_tail_2(self, value):
        """尾插法v2: 在单链表尾部增加一个tail指针"""
        # 直接利用tail定位尾部节点，添加新节点 O(1)
        if self.__tail is None: # 链表为空 调用头插法
            self.insert_head(value)
        else:
            self.__tail.next = Node(value) # tail的next指针连向新节点
            self.__tail = self.__tail.next # 移动tail到尾部 
    
    def insert_tail_3(self, value):
        """尾插法v3: 引用虚拟头节点dummy node，不需要处理边界空链表的情况了"""


    
    def insert(self, pos, value):
        """指定索引位置插入元素"""
        # 如果位置在0或者之前，调用头插法
        if pos < 0:
            self.insert_head(value)
        # 如果位置在原链表长度之后，调用尾插法
        elif pos > self.length() - 1:
            self.insert_tail(value)
        else:
            cur = self.__head # 定义一个头部临时指针cur
            count = 0
            while count < pos - 1:
                count += 1
                cur = cur.next
            newnode = Node(value) # 待插入到新节点
            newnode.next = cur.next
            cur.next = newnode
            
    def delete_head(self):
        """删除头结点"""
        cur = self.__head
        if self.__head is not None:
            self.__head = self.__head.next
            cur.next = None
        return cur

    def delete_tail(self):
        """删除尾节点"""
        cur = self.__head
        if self.__head is not None:
            if self.__head.next is None:  # 如果头结点是唯一的节点
                self.__head = None
            else:
                while cur.next.next is not None:
                    cur = cur.next
                cur.next, cur = (None, cur.next)
        return cur

    def remove(self, element):
        """删除指定元素"""
        cur, prev = self.__head, None
        while cur is not None:
            if cur.element == element:
                if cur == self.__head:  # 如果该节点是头结点
                    self.__head = cur.next
                else:
                    prev.next = cur.next
                break
            else:
                prev, cur = cur, cur.next
        return cur.element

    def modify(self, pos, element):
        """修改指定位置的元素"""
        cur = self.__head
        if pos < 0 or pos > self.length():
            return False
        for i in range(pos - 1):
            cur = cur.next
        cur.element = element
        return cur

    def search(self, element):
        """查找节点是否存在"""
        cur = self.__head
        while cur:
            if cur.element == element:
                return True
            else:
                cur = cur.next
        return False

    def reverse_list(self):
        """反转整个链表"""
        cur, prev = self.__head, None
        while cur:
            cur.next, prev, cur = prev, cur, cur.next
        self.__head = prev
        
    def traversal(self):
        cur = self.__head # 把head头指针也赋给p，p也指向头部
        while cur is not None:
            print(cur.value, end = " ")
            cur = cur.next
        print("\n")


if __name__ == "__main__":    
    linkedlist1 = linkedlist()
    linkedlist1.insert_head(5)
    
    linkedlist1.insert_tail(3)
    linkedlist1.insert_tail(4)
    
    linkedlist1.insert_tail_2(7)
    
    l = linkedlist1.length()
    print("链表长度为", l)

    linkedlist1.insert(2, 8)
    
    linkedlist1.traversal()
    
    linkedlist1.delete_head()
    linkedlist1.traversal()
    
    linkedlist1.reverse_list()
    linkedlist1.traversal()
