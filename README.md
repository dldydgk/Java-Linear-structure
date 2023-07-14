# Java-Linear-structure
자바 자료구조 선형구조

## 연결 리스트(Liked List)
- 연결 리스트는 자료들을 반드시 연속적으로 배열시키지는 않는다.
- 연결 리스트는 동적 메모리에 할당된 링크에 의해 연결된 유한 개수의 데이터 원소들이다.

### 연결 리스트의 특징
- 링크 값을 변화시키는 것 만으로도 노드의 삽입 삭제가 용이하다.
- 기억공간이 연속적으로 놓여 있지 않아도 저장이 가능하되, 중간 노드 연결이 끊어지면 그 다음 노드를 찾지 못한다.
- 연결을 위한 포인터를 찾는 시간이 필요하기 때문에 접근 속도가 느리다.
- 트리를 표현하기에 가장 적합한 자료이다.

## 노드(node)
- 자료와 포인터를 갖고 있는 것을 노드(node)라고 한다

## 연결 리스트의 종류
###  단순 연결 리스트(Singly Liked List)
  
![image](https://github.com/dldydgk/Java-Linear-structure/assets/126844590/80669ec5-da74-4b7e-a167-0926ba13d2da)


### - 단순 원형 연결 리스트(Singly Circlar Liked List)

![image](https://github.com/dldydgk/Java-Linear-structure/assets/126844590/1ced1165-e1b6-40b9-9a38-d60a3ad53680)

### - 이중 연결 리스트(Doubly Liked List)

![image](https://github.com/dldydgk/Java-Linear-structure/assets/126844590/1fa9a142-3f9f-4d29-bb0c-5081f10fb7c6)


- 이중 원형 연결 리스트(Doubly Circual Liked List)

  ![image](https://github.com/dldydgk/Java-Linear-structure/assets/126844590/58acb352-7aa8-4b14-a8c1-eaa6a06b1d71)



### 기초 자바 코드 ▼
``` java
package sungil_2022_03;

public class LinkedList {
	//첫번째 노드를 가리키는 필드
	private Node head;
	private Node tail;
	private int size = 0;
	private class Node {
		//데이터가 저장될 필드
		public Object date;
		//다음 노드를 가리키는 필드
		public Node next;
		public Node(Object input) {
			this.date = input;
			this.next = null;
		}
		// 노드의 내용을 쉽게 출력해서 확인해볼 수 있는 기능
		public String toString() {
			return String.valueOf(this.date);
		}
	}
	public void addFirst(Object input) {
		//노드를 생성합니다.
		Node temp = new Node(input);
		//새로운 노드의 다음 노드로 헤드를 지정합니다.
		temp.next = head;
		//헤드로 새로운 노드를 지정합니다
		head = temp;
		size++;
		if(head.next==null) {
			tail = head;
		}
	}
		public void addLast(Object input) {
			//노드를 생성합니다
			Node temp = new Node(input);
			if(size == 0) {
				addFirst(input);
			} else {
				tail.next = temp;
				tail = temp;
				size++;
		}
	}
}
```

## 스택(Stack )– LIFO(Last In First Out)
- 스택은 리스트의 한쪽 끝으로만 자료의 삽입 및 삭제가 이루어지는 구조로
  먼저 삽입된 자료가 맨 나중에 삭제가 되는 후입 선출로 Lsart In First Out
  방식이다.

![image](https://github.com/dldydgk/Java-Linear-structure/assets/126844590/6d07c164-3671-4c57-8b86-a18dbe11b148)

![image](https://github.com/dldydgk/Java-Linear-structure/assets/126844590/856bd7c6-269e-4ecf-978b-d9278938786c)


### 스택(Stack)의 응용 분야
- 부 프로그램 호출 시 복귀 주소를 저장할 때
- 함수 호출의 순서 제어
- 인터럽트(Interrupt) 발생하여 복귀 주소를 저장할 때
- 컴파일러를 이용한 언어 번역 시
- 표현된 수식은
① 전위 표기법(Prefix Notation) : 연산자를 피연산자의 앞에 표기 +ab
② 중위 표기법(Infix Notation) : 연산자를 피연산자 사이에 표기 a+b
③ 후위 표기법(Postfix Notation) : 연산자를 피연산자이 뒤에 표기 ab+



### 기초 자바 코드▼
``` java
package sungil_2022_03;

public class InStack {
	private int[] stk;	//스택용 배열
	private int capacity;	// 스택용 크기
	private int ptr;	// 스택 포인터
	
	// 실행시 예외: 스택이 비어있음
	public class EmptyIntStackException extends RuntimeException {
		public EmptyIntStackException()	{}
	}
	// 실행시 예외 스택이 가득 참
	public class OverflowIntStackException extends RuntimeException {
		public OverflowIntStackException() {}
	}
	// 생성자(constructor)
	public InStack(int maxlen) {
		ptr = 0;
		capacity = maxlen;
		try {
			stk = new int [capacity];	//스택용 본체용 배열을 생성
		} catch (OutOfMemoryError e) {	//생성할 수 없음
			capacity = 0;
		}
	}
	// 스택에 x를 푸시
	public int push(int x) throws OverflowIntStackException {
		if (ptr >= capacity)	//스택이 가득 참
			throw new OverflowIntStackException();
		return stk[ptr++] = x;
	}
	//스택에서 데이터를 팝(정상에 있는 데이터를 꺼냄)
	public int pop() throws EmptyIntStackException {
		if(ptr == 0)	//스택이 빔
			throw new EmptyIntStackException();
		return stk[--ptr];
	}
}
```


## 큐(queue) – FIFO(First In First Out)
큐(queue)는 한쪽 방향으로 데이터가 삽입되고 반대 방향으로 데이터가 삭제되는 먼저
들어온 데이터가 먼저 나가는 선입 선출(First In First Out) 구조이다.

  

### 큐의 예시
- 컴퓨터 시스템의 작업 스케줄에서 특별한 우선 순위가 없는 경우 먼저 들어온 프로세스가
먼저 처리된다.
- 계산대에서 계산대에 먼저 도착한 고객이 먼저 계산하고 나간다.
- 버스 승강장에서 앞에 선 사람이 먼저 승차한다.

![image](https://github.com/dldydgk/Java-Linear-structure/assets/126844590/5a9905f7-0427-444d-996e-c64a7a4fcc71)


### 프런트(F, Front)
- 가장 먼저 삽입된 자료의 기억 공간을 가리키는 포인터이다.
- 삭제 작업을 할 때 사용

### 리어(R, Rear)
- 가장 마지막에 삽입된 자료가 위치한 기억 장소를 가리키는 포인터이다.
- 삽입 작업을 할 때 사용

### Queue의 응용 분야
- 창구 업무나 택시 정거장처럼 서비스순서를 기다리는 등의 대기 행열의 처리에 사용한다.
- 운영 체제의 작업 스케줄링에 사용


### 기초 자바 코드▼
``` java
package sungil_2022_03;

public class IntQueue {
	private int[] que;
	private int capacity;
	private int front;
	private int rear;
	private int num;

	public class EmptyIntQueueException extends RuntimeException {
		public EmptyIntQueueException() {}
	}
	public class OverflowIntQueueException extends RuntimeException {
		public OverflowIntQueueException() {}
	}
	public IntQueue(int maxlen) {
		num = front = rear = 0;
		capacity = maxlen;
		try {
			que = new int[capacity];
		} catch (Error e) {
			if(num >= capacity)
				throw new OverflowIntQueueException();
		}
	}
	public int enque(int x) throws OverflowIntQueueException {
		if (num>=capacity)
			throw new OverflowIntQueueException();
		que[rear++] = x;
		num++;
		if(rear == capacity)
			rear = 0;
		return x;
	}
	public int deque() throws EmptyIntQueueException {
		if(num <= 0)
			throw new EmptyIntQueueException();
		int x = que[front++];
		num--;
		if(front == capacity)
			front = 0;
		return x;
	}
}
```
