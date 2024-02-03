include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_NAME_LENGTH 50

typedef struct {
    char name[MAX_NAME_LENGTH];
    int age;
} Person;

void clearBuffer() {
    int c;
    while ((c = getchar()) != '\n' && c != EOF);
}

void getInput(char *prompt, char *buffer, size_t size) {
    printf("%s", prompt);
    fgets(buffer, size, stdin);
    buffer[strcspn(buffer, "\n")] = '\0';  // Remove trailing newline
    clearBuffer();
}

int main() {
    Person person;

    // Input validation to prevent buffer overflow
    getInput("Enter name: ", person.name, MAX_NAME_LENGTH);

    // Validate age input
    do {
        printf("Enter age: ");
        if (scanf("%d", &person.age) != 1) {
            printf("Invalid input. Please enter a valid age.\n");
            clearBuffer();
        }
    } while (person.age < 0);

    // Display user information
    printf("\nUser Information:\n");
    printf("Name: %s\n", person.name);
    printf("Age: %d\n", person.age);

    return 0;
