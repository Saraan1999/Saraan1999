#include <stdio.h>
#include <stdlib.h>
typedef struct stackk {
    int top;
    unsigned int size;
    int *array;
} stack_type;
stack_type* create(unsigned int size) {
    stack_type *stack_A = (stack_type*) malloc(sizeof(stack_type));
    stack_A->size = size;
    stack_A->top = -1;
    stack_A->array = (int*) malloc(stack_A->size * sizeof(int));
    return stack_A;
}
int isFull(stack_type *stack1) {
    return (stack1->top == (stack1->size - 1));
}
int isEmpty(stack_type *stack1) {
    return (stack1->top == -1);
}
int push(stack_type *stack1, int data) {
    if (isFull(stack1)) {
        printf("Stack is full!\n");
        return 1;
    }
    if (!isEmpty(stack1) && data <= stack1->array[stack1->top]) {
        printf("Cannot push %d: must be greater than the top element %d\n", data, stack1->array[stack1->top]);
        return 1;
    }
    stack1->array[++stack1->top] = data;
    return 0;
}
/// @brief 
/// @param stack1 
/// @return 
int pop(stack_type *stack1) {
    if (isEmpty(stack1)) {
        printf("Stack is empty!\n");
        return 1;
    } else {
        printf("\nPopped element: %d\n", stack1->array[stack1->top--]);
        return 0;
    }
}
int peek(stack_type *stack1) {
    if (isEmpty(stack1)) {
        printf("Stack is empty!\n");
        return -1; // or another indication of an empty stack
    } else {
        return stack1->array[stack1->top];
    }
}
void freeStack(stack_type *stack1) {
    if (stack1) {
        free(stack1->array);
        free(stack1);
    }
}
int main() {
    stack_type *myStack = create(5);
    push(myStack, 5);
    push(myStack, 10);
    push(myStack, 15);
    push(myStack, 12); // This should fail
    pop(myStack);
    push(myStack, 20);
    push(myStack, 18); // This should fail
    pop(myStack);
    pop(myStack);
    pop(myStack);
    pop(myStack); // Empty stack pop
    
    freeStack(myStack);
    return 0;
}
