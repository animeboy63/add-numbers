# add-numbers
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Linked List Node
struct Node {
    int data;
    struct Node* next;
};

// Function to create a new node
struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->next = NULL;
    return newNode;
}

// Function to add a digit at the beginning of the linked list
void addToFront(struct Node** head, int digit) {
    struct Node* newNode = createNode(digit);
    newNode->next = *head;
    *head = newNode;
}

// Function to add two large numbers represented by linked lists
struct Node* addLargeNumbers(struct Node* num1, struct Node* num2) {
    struct Node* result = NULL;
    int carry = 0;

    while (num1 || num2 || carry) {
        int sum = carry;

        if (num1) {
            sum += num1->data;
            num1 = num1->next;
        }
        if (num2) {
            sum += num2->data;
            num2 = num2->next;
        }

        carry = sum / 10;
        sum %= 10;

        addToFront(&result, sum);
    }

    return result;
}

// Function to display a linked list
void display(struct Node* head) {
    struct Node* current = head;
    while (current) {
        printf("%d", current->data);
        current = current->next;
    }
    printf("\n");
}

int main() {
    char num1_str[1000];
    char num2_str[1000];

    printf("Enter the first large number: ");
    scanf("%s", num1_str);

    printf("Enter the second large number: ");
    scanf("%s", num2_str);

    struct Node* number1 = NULL;
    struct Node* number2 = NULL;

    int num1_len = strlen(num1_str);
    int num2_len = strlen(num2_str);

    for (int i = num1_len - 1; i >= 0; i--) {
        addToFront(&number1, num1_str[i] - '0');
    }

    for (int i = num2_len - 1; i >= 0; i--) {
        addToFront(&number2, num2_str[i] - '0');
    }

    printf("Number 1: ");
    display(number1);

    printf("Number 2: ");
    display(number2);

    struct Node* sum = addLargeNumbers(number1, number2);
    printf("Sum: ");
    display(sum);

    return 0;
}
