# 1.  큐
## { 1-1. 큐의 정의 }
> 정의 
- 삽입과 삭제의 위치가 제한적인 자료구조이다. 
- 뒤에서는 삽입, 앞에서는 삭제만 이루어지는 선입선출(FIFO)구조이다. (삽입한 순서대로 원소가 저장되어, 가장 먼저 삽입된 원소는 가장 먼저 삭제된다.)
- ex) 캐시,버퍼, 은행줄, 버스 정류장, 인쇄 대기열

> 장단점 
- 장점 
	- **FIFO(First-In-First-Out)** 구조로 데이터가 들어온 순서대로 처리됨 → 순서가 중요한 작업에 적합 (예: 대기열, 요청 처리)
	-  **운영체제에서 다양하게 활용 가능** → 작업 스케줄링, 프로세스 관리, 프린터 대기열 등
	- 삽입(EnQueue)과 삭제(DeQueue) 연산이 **간단하고 직관적**
	-  **데이터 흐름이 자연스럽게 표현됨** → 네트워크 버퍼, 메시지 큐, 이벤트 처리 등에서 유용
- 단점 
	- **배열 기반 큐는 공간 낭비** → `DeQueue` 후 앞쪽 공간을 재사용하지 못함 (해결: 원형 큐)
    - 큐에 들어간 데이터를 **중간에서 접근하거나 수정하기 어려움**
    - **최대 크기 지정이 필요한 경우**, 크기 초과 시 Overflow 발생 가능→ 동적 큐나 리스트 기반 큐로 해결 가능
    - 단순 큐는 **복잡한 우선순위나 조건 처리가 어려움**  → 우선순위 큐(Priority Queue), 이중 큐(Deque) 등이 필요할 수 있음

## { 1-2. 큐의 주요 연산 }
| 연산 이름       | 설명                                         | 사용 메서드/기능              |
| ----------- | ------------------------------------------ | ---------------------- |
| **EnQueue** | 큐의 **뒤쪽**에 원소를 삽입하는 연산                     | `append()`             |
| **DeQueue** | 큐의 **앞쪽**에서 원소를 **삭제하고 반환**하는 연산           | `pop(0)`               |
| **IsEmpty** | 큐가 **비어있는지** 확인하는 연산                       | `len(queue) == 0` 등    |
| **IsFull**  | 큐가 **가득 찼는지** 확인하는 연산 (고정 크기 큐에 해당)        | `len(queue) == size` 등 |
| **peek**    | 큐의 앞쪽 원소를 **삭제하지 않고 반환**하는 연산              | `queue[0]`             |
| **Front**   | 큐에서 **삭제할 위치** 또는 **첫 번째 원소 위치**를 가리키는 포인터 | -                      |
| **Rear**    | 큐에서 **삽입할 위치** 또는 **마지막 원소 위치**를 가리키는 포인터  | -                      |

## {1-3. 큐의 작동 구조 }
![[Pasted image 20251016085652.png]]
![[Pasted image 20251016085708.png]]

## { 1-4. 시간복잡도 }
- 시간복잡도: 특정 원소를 빼기 위한 pop(n)의 시간 복잡도는 O(n)이기 때문에 효율이 낮다. 따라서 pop(숫자로 된 위치)는 하지 않는 것이 좋다.
    - pop(숫자로 된 위치)를 하면 위치에 있는 값이 빠지고 큐에 있는 값이 한칸씩 당겨지기 때문에 for문과 같은 역할을 내부적으로 한다. (내장 함수의 대부분이 그렇다. ex:max())

# 2. 구현 
## { 2-1. 리스트로 구현하기}
1. enqueue (1/2)
    
    - 메소드를 통한 구현
    - append메소드를 통해 리스트의 마지막에 데이터를 삽입(append의 시간 복잡도는 1)
    
    ```python
    queue = []
    #삽입 
    def enqueue(item):
    	queue.append(item)
    #삭제 
    def dequeue():
    	if len(queue) ==0:
    		print("데이터가 없습니다.")
    		return 
    	return queue.pop(0)
    
    ```

## { 2-2. 클래스로 구현하기}
- 클래스를 이용해서 구조체를 정의하고, front, rear 포인터를 활용해서 구현한다.

```python
class Queue:
	# 생성자 메서드 
	#capacity: 크기 설정 값 
	def __init__(self,capacity):
		#capacity에 크기를 설정하면 self.capacity변수에 값을 넣는다.
		self.capacity = capacity
		# self.items변수에 capacity 크기값만큼 큐를 생성한다. [None,None...*10] 
		# [] 와 * 이 만나면 곱해진 값만큼 리스트를 생성한다. 
		self.items = [None] * capacity
		# 포인터 
		self.front = -1
		self.rear = -1
	# 가득차 있을 경우 
	# rear+1이 큐의 길이와 같다면 더이상 집어넣을 수 없다. 
	def is_full(self):
		return self.rear ==self.capacity - 1
	#삽입 메서드 
	def enqueue(self,item):
		# 만약 가득 차있다면 
		is self.is_full():
			raise IndexError("Queue is full")
		#가득차지 않았다면 위치를 옮기고 데이터를 집어넣는다. 
		self.rear +=1
		self.items[self.rear] = item
	
	# 큐가 비었다 == rear와 front 값이 같다. (관리하는 데이터가 같다. ) 
	def is_empty(self):
		return self.front == self.rear
	#큐의 값 삭제 
	def dequeue(self):
		if self.is_empty():
			raise IndexError("Queue is empty")
		# front 값을 1 더해준다. 
		self.front +=1
		# item 변수에 해당 위치의 데이터 값을 넣어준다. 
		item = self.item[self.front]
		# None으로 바꿔 해당 위치의 데이터를 큐에서 삭제해준다. 
		self.items[self,front] = None
		# item변수를 반환해준다. 
		return item
	# 값만 리턴해준다. 
	def peek(self):
		if self.is_empty():
			raise IndexError("Queue is empty")
		return self.items[self.front+1]
		
```
