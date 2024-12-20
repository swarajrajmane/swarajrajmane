#include <stdio.h>

int main() {
    int a, b, temp;

    // Input two numbers
    printf("Enter the first number (a): ");
    scanf("%d", &a);

    printf("Enter the second number (b): ");
    scanf("%d", &b);

    // Display numbers before swapping
    printf("\nBefore swapping:\n");
    printf("a = %d, b = %d\n", a, b);

    // Swapping logic using a temporary variable
    temp = a;
    a = b;
    b = temp;

    // Display numbers after swapping
    printf("\nAfter swapping:\n");
    printf("a = %d, b = %d\n", a, b);

    return 0;
}
