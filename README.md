#include <stdio.h>

#define MAX_SUBJECTS 5

void calculateResult(const int marks[], int count, int *total, float *average);
char getGrade(float average);
void displayMarks(const int marks[], int count);

int main(void) {
    int marks[MAX_SUBJECTS];
    int total = 0;
    float average = 0.0f;
    char grade;

    printf("=== Student Marks Calculator ===\n");
    printf("Enter marks for %d subjects (0-100):\n", MAX_SUBJECTS);

    for (int i = 0; i < MAX_SUBJECTS; i++) {
        printf("Subject %d: ", i + 1);

        if (scanf("%d", &marks[i]) != 1 || marks[i] < 0 || marks[i] > 100) {
            printf("Invalid input. Enter marks between 0 and 100.\n");
            return 1;
        }
    }

    calculateResult(marks, MAX_SUBJECTS, &total, &average);
    grade = getGrade(average);

    printf("\n--- Result ---\n");
    displayMarks(marks, MAX_SUBJECTS);
    printf("Total   : %d/%d\n", total, MAX_SUBJECTS * 100);
    printf("Average : %.2f\n", average);
    printf("Grade   : %c\n", grade);

    if (average >= 50.0f)
        printf("Status  : Pass\n");
    else
        printf("Status  : Fail\n");

    return 0;
}

void calculateResult(const int marks[], int count, int *total, float *average) {
    *total = 0;

    for (int i = 0; i < count; i++)
        *total += marks[i];

    *average = (float)(*total) / count;
}

char getGrade(float average) {
    if (average >= 90) return 'A';
    else if (average >= 75) return 'B';
    else if (average >= 60) return 'C';
    else if (average >= 50) return 'D';
    else return 'F';
}

void displayMarks(const int marks[], int count) {
    printf("Marks   : ");

    for (int i = 0; i < count; i++) {
        printf("%d", marks[i]);
        if (i < count - 1)
            printf(", ");
    }

    printf("\n");
}
