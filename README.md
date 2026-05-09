# Mini-Store-Billing-system-
The objective of this lab assignment is to develop a C program that simulates a basic store  billing system. The program should take input for multiple items, calculate totals, apply  discount and tax, and display a formatted bill.
#include <stdio.h>
#include <conio.h>

int main() {
    int n, i, choice;
    float price[50], total[50];
    int qty[50];

    float grandTotal = 0, discount = 0, tax = 0, net = 0;
    int totalQty = 0;

    printf("Enter number of items: ");
    scanf("%d", &n);

    // Input
    for(i = 0; i < n; i++) {
        printf("Price of item %d: ", i + 1);
        scanf("%f", &price[i]);

        printf("Quantity of item %d: ", i + 1);
        scanf("%d", &qty[i]);
    }

    // AUTOMATIC CALCULATION
    for(i = 0; i < n; i++) {
        total[i] = price[i] * qty[i];
        grandTotal += total[i];
        totalQty += qty[i];
    }

    // Discount logic
    if(grandTotal > 5000)
        discount = grandTotal * 0.10; // 10% discount
    else if(grandTotal > 2000)
        discount = grandTotal * 0.05; // 5% discount

    // Tax and Net calculation
    tax = (grandTotal - discount) * 0.08; // 8% tax
    net = grandTotal - discount + tax;

    // Menu
    do {
        printf("\n1. Display Bill  2. Most Expensive Item  3. Exit");
        printf("\nEnter choice: ");
        scanf("%d", &choice);

        if(choice == 1) {
            printf("\nItem\tPrice\tQty\tTotal\n");
            for(i = 0; i < n; i++) {
                printf("%d\t%.2f\t%d\t%.2f\n", i + 1, price[i], qty[i], total[i]);
            }
            printf("\nTotal Quantity = %d", totalQty);
            printf("\nTotal = %.2f", grandTotal);
            printf("\nDiscount = %.2f", discount);
            printf("\nTax = %.2f", tax);
            printf("\nNet = %.2f\n", net);
        }
        else if(choice == 2) {
            int max = 0;
            for(i = 1; i < n; i++) {
                if(price[i] > price[max])
                    max = i;
            }
            printf("\nMost expensive item: %d (%.2f)\n", max + 1, price[max]);
        }
    } while(choice != 3);

    return 0;
}
