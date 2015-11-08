# Data-Structure-Assignment-2
Linked List

#include<stdio.h>
#include<stdlib.h>


#define NULL_VALUE -99999
#define SUCCESS_VALUE 99999

struct listNode
{
    int item;
    struct listNode * next;
};

struct listNode * list;

void initializeList()
{
    list = 0;  //initially set to NULL
}

int insertItem(int item) //insert at the beginning
{
	struct listNode * newNode ;
	newNode = (struct listNode*) malloc (sizeof(struct listNode)) ;
	newNode->item = item ;
	newNode->next = list ; //point to previous first node
	list = newNode ; //set list to point to newnode as this is now the first node
	return SUCCESS_VALUE ;
}


int deleteItem(int item)
{
	struct listNode *temp, *prev ;
	temp = list ; //start at the beginning
	while (temp != 0)
	{
		if (temp->item == item) break ;
		prev = temp;
		temp = temp->next ; //move to next node
	}
	if (temp == 0) return NULL_VALUE ; //item not found to delete
	if (temp == list) //delete the first node
	{
		list = list->next ;
		free(temp) ;
	}
	else
	{
		prev->next = temp->next ;
		free(temp);
	}
	return SUCCESS_VALUE ;
}


struct listNode * searchItem(int item)
{
	struct listNode * temp ;
	temp = list ; //start at the beginning
	while (temp != 0)
	{
		if (temp->item == item) return temp ;
		temp = temp->next ; //move to next node
	}
	return 0 ; //0 means invalid pointer in C, also called NULL value in C
}

void printList()
{
    struct listNode * temp;
    temp = list;
    while(temp!=0)
    {
        printf("%d->", temp->item);
        temp = temp->next;
    }
    printf("\n");
}

///Task 1 – 4 are to be added in LinkedList.cpp file.
///The file implements a singly linked list using a head
///pointer that points to the first node of the list. Your job is to add following features.



///Task 1: Add insertLast function. Add a new function insertLast(int item)
/// to the list. This function will insert a new item at the end of the list.
int insertLast(int item)
{
    struct listNode * temp;
    temp = list;
    while(temp->next!=0)
    {
        temp = temp->next;
    }
    struct listNode * node;
    node = (struct listNode*) malloc (sizeof(struct listNode)) ;
    node->item=item;
    node->next=0;
    temp->next=node;

}


///Task 2: Add insertAfter function. Add a new function insertAfter(int oldItem,int newItem) to the list. This function will
///insert a new item after an existing item in the list. The function will first search for oldItem in the list. Then it will
///insert the newItem after the oldItem in the list. If the olditem is not present in the list, then insertion should be discarded.

int insertAfter(int oldItem, int newItem)
{
    struct listNode *temp;
    struct listNode *node;
    node = (struct listNode*) malloc (sizeof(struct listNode)) ;
    temp=list;
    node->item=newItem;
    while(temp!=0)
    {
        if(temp->item==oldItem)
        {
            break;
        }
        temp=temp->next;
    }
    node->next=temp->next;
    temp->next=node;

}



///Task 3: Add deleteFirst function. This function will delete the first element of the list. You must ensure that memory of the
///deleted item is released properly. In case the item is not found in the list, return a NULL_VALUE, otherwise return SUCCESS_VALUE.
int deleteLast()
{
    struct listNode *temp;
    struct listNode *prev;
    temp=list;
    while(temp->next!=0)
    {
        prev=temp;
        temp=temp->next;
    }
    prev->next=0;


}


///Task 4: Add deleteLast function. This function will delete the last element of the list. You must ensure that memory of the
///deleted item is correctly released. In case the item is not found in the list, return a NULL_VALUE, otherwise return SUCCESS_VALUE.

int deleteFirst()
{
    if(list!=0)list=list->next;

}


int main(void)
{
    initializeList();
    printf("1. Insert new item. 2. Delete item. 3. Search item. \n");
    printf("4. Print. 5.Insert Last .6.Insert After. 7.Delete Last. 8.Delete First . 9.exit.\n");

    while(1)
    {
        int ch;
        scanf("%d",&ch);
        if(ch==1)
        {
            int item;
            scanf("%d", &item);
            insertItem(item);
        }
        else if(ch==2)
        {
            int item;
            scanf("%d", &item);
            deleteItem(item);
        }
        else if(ch==3)
        {
            int item;
            scanf("%d", &item);
            struct listNode * res = searchItem(item);
            if(res!=0) printf("Found.\n");
            else printf("Not found.\n");
        }
        else if(ch==4)
        {
            printList();
        }
        else if(ch==5)
        {
            int item;
            scanf("%d",&item);
            insertLast(item);
        }
        else if(ch==6)
        {
            int oldItem,newItem;
            scanf("%d %d",&oldItem,&newItem);
            insertAfter(oldItem,newItem);
        }
        else if(ch==7)
        {
            deleteLast();
        }
        else if(ch==8)
        {
            deleteFirst();
        }
        else if(ch==9)
        {
            break;
        }
    }

}

