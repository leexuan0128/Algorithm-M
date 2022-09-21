## Definition

栈和队列的原理：队列是先进先出，栈是先进后出。

队列可以理解为有两个口的直通道，一边负责入，另一边负责出。而栈是只有入口的封闭通道，所以只能从入口处进行操作。

队列提供push，pop，peek等接口，所有元素必须符合先进先出FIFO规则，队列可以用栈来实现，也就是列表。

栈提供push和pop等接口，所有元素必须符合先进后出FILO规则，所以栈不提供走访功能，也不提供迭代器(iterator)。 不像是set或者map提供迭代器iterator来遍历所有元素。

栈的底层实现可以是vector，deque，list 都是可以的， 主要就是数组和链表的底层实现。

## Implementation
- 用两个栈实现队列
    ```python
    # 栈用列表List实现
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

- 用两个队列实现栈
    ```python
    # 队列用deque实现
    from collections import deque
    class MyStack:
        def __init__(self):
            self.queue_in = deque() # in queue 存所有数据
            self.queue_out = deque() # out queue pop交换数据

        def push(self, x: int) -> None:
            self.queue_in.append(x)

        def pop(self) -> int:
            """
            1. 首先确认不空
            2. 因为队列的特殊性，FIFO，所以我们只有在pop()的时候才会使用queue_out
            3. 先把queue_in中的所有元素（除了最后一个），依次出列放进queue_out
            4. 交换in和out，此时out里只有一个元素
            5. 把out中的pop出来，即是原队列的最后一个
            
            tip：这不能像栈实现队列一样，因为另一个queue也是FIFO，如果执行pop()它不能像stack一样从另一个pop()，所以干脆in只用来存数据，pop()的时候两个进行交换。
            """
            if self.empty():
                return None
            for _ in range(len(self.queue_in) - 1):
                self.queue_out.append(self.queue_in.popleft())
            self.queue_in, self.queue_out = self.queue_out, self.queue_in
            return self.queue_out.popleft()
        
        def top(self) -> int:
            if self.empty():
                return None
            return self.queue_in[-1]

        def empty(self) -> bool:
            return len(self.queue_in) == 0

    # Your MyStack object will be instantiated and called as such:
    # obj = MyStack()
    # obj.push(x)
    # param_2 = obj.pop()
    # param_3 = obj.top()
    # param_4 = obj.empty()
    ```

- 用一个队列实现栈
    ```python
    # 队列用deque实现
    from collections import deque
    class MyStack:
        def __init__(self):
            self.single_queue = deque()

        def push(self, x: int) -> None:
            self.single_queue.append(x)

        # 一个队列在模拟栈弹出元素的时候只要将队列头部的元素（除了最后一个元素外）重新添加到队列尾部，此时在去弹出头元素就是出栈的顺序了。
        def pop(self) -> int:
            if self.empty():
                return None
            for i in range(len(self.single_queue) - 1):
                self.single_queue.append(self.single_queue.popleft())
            return self.single_queue.popleft()

        def top(self) -> int:
            if self.empty():
                return None
            return self.single_queue[-1]

        def empty(self):
            return not self.single_queue
    ```