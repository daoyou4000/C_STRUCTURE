## There are two ways to build the Queue.

The Queue is a linear list with two terminals **Front** and **Rear** which follows the rule 
FIFO (Fisrt In First Out). The Front is used to remove element and rear is used to add new element.
It is not allowed to remove or add new elements in between.

### Create the Queue
- use the array with fixed size.
- use the list to build the Queue with flexible size.

两种方法的优缺点，使用数组程序代码比较简单，但在声明队列时已经固定了队列了长度。
使用链表做队列时，代码稍微复杂，但是队列长度灵活。


'''

#include<stdio.h>
#include<stdlib.h>
#include<stdbool.h>

#define MAXSIZE	6
#define ERROR -99

// the struct of the 
typedef struct
{
	int Data[MAXSIZE];
	int front;
	int rear;
	int size;
} Queue;

// create the new Queue, return the Queue pointer
Queue* pCreateQueue()
{
	Queue* p = (Queue*)malloc(sizeof(Queue));
	if (!p)
	{
		printf("no space");
		return NULL;
	}
	// initialize the Queue data;
	p->front = -1;
	p->rear = -1;
	p->size = 0;
	// return the Queue pointer;
	return p;
}

bool bIsFullQ(Queue* pQueue)
{
	bool bFullorNot = (pQueue->size == MAXSIZE)? 1 : 0;
	return bFullorNot;
}

void vAddQueue(Queue* pQueue, int iItem)
{
	if (bIsFullQ(pQueue))
	{
		printf("Full Queue");
		return;
	}
	pQueue->rear++;
	pQueue->rear = pQueue->rear % MAXSIZE;
	pQueue->Data[pQueue->rear] = iItem;
	pQueue->size++;

}

void vPrintQ(Queue* pQueue)
{
	if (pQueue->size == 0)
	{
		printf("the Queue is Empty");
		return;
	}
	printf("the Queue is: \n");
	int index = pQueue->front;

	for (int i = 0; i < pQueue->size; i++)
	{
		index++;
		index %= MAXSIZE;
		printf("%d\n", pQueue->Data[index]);
	}

	printf("\n");
	return;
}

int iRemoveQueue(Queue* pQueue)
{
	if (pQueue->size == 0)
	{
		printf("the Queue is Empty");
		return ERROR;
	}

	pQueue->front++;
	pQueue->front %= MAXSIZE;
	pQueue->size--;
	return pQueue->Data[pQueue->front];
}

int main(void)
{
	Queue* pQue = pCreateQueue();
	vAddQueue(pQue, 1);
	vAddQueue(pQue, 2);
	vAddQueue(pQue, 3);
	vAddQueue(pQue, 5);
	vAddQueue(pQue, 4);
	vAddQueue(pQue, 3);
	iRemoveQueue(pQue);
	vAddQueue(pQue, 1);
	
	vPrintQ(pQue);
	return 1;
}


'''
