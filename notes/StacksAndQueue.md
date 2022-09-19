## Definition

栈和队列的原理：队列是先进先出，栈是先进后出。

队列可以理解为有两个口的直通道，一边负责入，另一边负责出。而栈是只有入口的封闭通道，所以只能从入口处进行操作。

栈提供push 和 pop 等等接口，所有元素必须符合先进后出规则，所以栈不提供走访功能，也不提供迭代器(iterator)。 不像是set 或者map 提供迭代器iterator来遍历所有元素。

栈提供push 和 pop 等等接口，所有元素必须符合先进后出规则，所以栈不提供走访功能，也不提供迭代器(iterator)。 不像是set 或者map 提供迭代器iterator来遍历所有元素。

栈的底层实现可以是vector，deque，list 都是可以的， 主要就是数组和链表的底层实现。

## Implementation
- 用两个栈实现队列
    ```python
    class MyQueue:
        def __init__(self):
            """
            in stack主要负责push，out stack主要负责pop
            """
            self.stack_in = [] # 入栈
            self.stack_out = [] # 出栈

        def push(self, x: int) -> None:
            """
            有新元素进来，就往in stack 里面push，原理利用列表的append方法
            """
            self.stack_in.append(x)

        def pop(self) -> int:
            """
            Removes the element from the front of queue and returns that element.
            """
            # 先判空
            if self.empty():
                return None
            # 如果输出栈不为空，则直接从出栈弹出数据
            if self.stack_out:
                return self.stack_out.pop()
            # 如果出栈为空，就把入栈所有元素push进出栈，再从出栈弹出数据
            else:
                for i in range(len(self.stack_in)):
                    self.stack_out.append(self.stack_in.pop())
                return self.stack_out.pop()

        def peek(self) -> int:
            """
            Show the front element.
            """
            # 复用pop()方法，先弹出显示，再添加回去
            ans = self.pop()
            self.stack_out.append(ans)
            return ans

        def empty(self) -> bool:
            """
            只要in或者out有元素，说明队列不为空
            """
            return not (self.stack_in or self.stack_out)

    # Your MyQueue object will be instantiated and called as such:
    obj = MyQueue()
    obj.push(1)
    obj.push(2)
    obj.push(3)
    param_2 = obj.pop() # 1, 2
    param_3 = obj.pop() # 1
    param_4 = obj.empty() # F
    ```