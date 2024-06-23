main.c----------
#include "ArrayStack.h"

int main()
{
   ArrayStack* Stack = NULL;
    AS_CreateStack(&Stack, 10);
    AS_Push(Stack, 1);
    AS_Push(Stack, 2);
    AS_Push(Stack, 3);
   
    printf("\n%d", Stack->Nodes[1].Data);
    return 0;
}
-------------
ArrayStack.h------------
#ifndef ARRAYSTACK_H
#define ARRAYSTACK_H

#include <stdio.h>
#include <stdlib.h>

typedef int ElementType;

typedef struct tagNode{
    ElementType Data;
}Node;

typedef struct tagArrayStack{
   
    int Capacity;
    int Top;
    Node* Nodes;
}ArrayStack;


void AS_CreateStack(ArrayStack** Stack, int Capacity);
void AS_DestroyStack(ArrayStack* Stack);
void AS_Push(ArrayStack* Stack, ElementType Data);



#endif
--------------
ArrayStack.c----------------
#include "ArrayStack.h"

//Stack 생성
void AS_CreateStack(ArrayStack** Stack, int Capacity){
   
    //Stack을 자유 저장소에 저장
    (*Stack) = (ArrayStack*)malloc(sizeof(ArrayStack));
   
    //입력된 Capacity만큼 Stack의 Node를 자유 저장소에 저장
    (*Stack)->Nodes = (Node*)malloc(Capacity * sizeof(Node));
   
    //Stack의 Capacity와 Top 초기화
    (*Stack)->Capacity = Capacity;
    (*Stack)->Top = -1;
}

//노드 소멸
void AS_DestroyStack(ArrayStack* Stack){
   
    free(Stack->Nodes);
    free(Stack);
   
}

void AS_Push(ArrayStack* Stack, ElementType Data){
   
    Stack->Nodes[++(Stack->Top)].Data = Data;
   
   
}
===============
