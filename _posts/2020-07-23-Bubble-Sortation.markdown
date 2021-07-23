---
layout: post
title:  "Bubble Sortation"
date:   2020-07-23 21:34:25 +0900
categories: C Algorithm
---

### Bubble Sortation Extension (버블 정렬 활용)

버블 정렬에 대해서 배웠으니, 이를 구조체 포인터와 함께 활용을 하는 코드를 짜보았다.

전에 Selection Sortation에 적용한 대로 코드를 만들었다.

``` c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

typedef struct {
    int id;
    int korean;
    int english;
    int math;
}student;

void get_score(student *std_p, int n);
void display_list(student *std_p, int n);
void bubble_sortation_descending(student *std_p, int n);
void bubble_sortation_ascending(student *std_p, int n);

int main(void) {
    
    student *std_p;
    int n;
    
    printf("Enter your number : ");
    scanf("%d", &n);
    
    std_p = (student *) malloc(n * sizeof(student));
    
    if(!std_p) {
        printf("ERROR : Memory allocation failed!\n");
        exit(1);
    }
    
    get_score(std_p, n);
    printf("\nRandom profile generated!");
    display_list(std_p, n);
    
    bubble_sortation_descending(std_p, n);
    printf("Bubble sortation descending.");
    display_list(std_p, n);
    
    bubble_sortation_ascending(std_p, n);
    printf("Bubble sortation ascending.");
    display_list(std_p, n);
    
    free(std_p);
    
    return 0;
}

void get_score(student *std_p, int n) {
    
    srand((unsigned int)time(NULL));
    
    int i;
    
    for (i = 0; i < n; i++)
    {
        (std_p + i)->id = i + 1;
        (std_p + i)->korean = rand() % 101;
        (std_p + i)->english = rand() % 101;
        (std_p + i)->math = rand() % 101;
    }
        
    return;
}

void display_list(student *std_p, int n) {
    
    printf("\n\n id\t Korean\tEnglish\t   Math\n");
    for (int i = 0; i < n; i++)
        printf("%3d\t\t%3d\t\t%3d\t\t%3d\n", (std_p + i)->id, (std_p + i)->korean,\
               (std_p + i)->english, (std_p + i)->math);
    printf("\n\n");
    
    return;
}

void bubble_sortation_descending(student *std_p, int n) {
    
    student temp;
    int i, j;
    
    for (i = 0; i < n - 1; i++)
        for (j = 0; j < n - i - 1; j++)
            if ((std_p + j)->korean < (std_p + j + 1)->korean) {
                temp = *(std_p + j);
                *(std_p + j) = *(std_p + j + 1);
                *(std_p + j + 1) = temp;
            }
    
    return;
}

void bubble_sortation_ascending(student *std_p, int n) {
    
    student temp;
    int i, j;
    
    for (i = 0; i < n - 1; i++)
        for (j = 0; j < n - i - 1; j++)
            if ((std_p + j)->korean > (std_p + j + 1)->korean) {
                temp = *(std_p + j);
                *(std_p + j) = *(std_p + j + 1);
                *(std_p + j + 1) = temp;
            }
    
    return;
}

```
