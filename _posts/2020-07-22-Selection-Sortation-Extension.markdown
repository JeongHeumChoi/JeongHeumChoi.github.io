---
layout: post
title:  "Selection Sortation Extension"
date:   2020-07-22 16:42:15 +0900
categories: C Algorithm
---

### Selection Sortation Extension (선택 정렬 활용)

선택 정렬에 대해서 배웠으니, 이를 구조체 포인터와 함께 활용을 하는 코드를 짜보았다.

어떠한 상황을 예시로 코드를 짜볼지 고민을 하다가.. 간단하게 학생들의 성적을 이용해서 짜보기로 했다.

학생들의 정보를 구조체로 만들 때, 하나의 성적만 넣으려고 했지만 조금은 심심해보여서 여러 과목들을 추가해줬다.

``` c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

typedef struct {
    int id;
    int korean;
    int mathmatics;
    int english;
} student;

void getRandomScore(student *profile, int size);
void printProfile(student *profile, int size);
void selectionSortation(student *profile, int size);

int main(void) {
    
    student *profile;
    int num;
    
    printf("Enter your number : ");
    scanf("%d", &num);
    
    profile = (student*) malloc(num * sizeof(student));
    
    if (!profile) {
        printf("ERROR : Memory allocation failed!");
        exit(1);
    }
    
    getRandomScore(profile, num);
    
    printf("\n\nRandom profile generated!\n\n");
    printProfile(profile, num);
    
    selectionSortation(profile, num);
    
    printf("\n\nprofile has sorted by selection sortation!\n\n");
    printProfile(profile, num);

    free(profile);

    return 0;
}

void selectionSortation(student *profile, int size) {
    
    student temp;
    int maxIndex;
    int i, j;
    
    for (i = 0; i < size - 1; i++) {

        // 최솟값을 미리 정해두고 간다.
        maxIndex = 0;
        
        // 고정시킨 부분을 제외한 배열 내에서 최댓값의 index를 찾아낸다.
        for (j = 0; j < size - i; j++)
            if ((profile + maxIndex)->korean < (profile + j)->korean)
                maxIndex = j;

        // 배열의 끝 부분부터 차례대로 고정 시켜나간다.
        // profile + j - 1이 가리키고 있는 부분이 이번 턴에 고정시킬 자리다.
        // 학생의 정보 자체를 바꿔야하기 때문에 멤버변수 korean만 swap하는 것이 아니라, 구조체를 통째로 swap해야한다.
        temp = *(profile + j - 1); 
        *(profile + j - 1) = *(profile + maxIndex);
        *(profile + maxIndex) = temp;
    }
    
    return;
}

void getRandomScore(student *profile, int size) {
    
    srand((unsigned int)time(NULL));
    
    for (int i = 0; i < size; i++) {
        (profile + i)->id = i + 1;
        (profile + i)->korean = rand() % 101;
        (profile + i)->mathmatics = rand() % 101;
        (profile + i)->english = rand() % 101;
    }
    
    return;
}

void printProfile(student *profile, int size) {
    
    printf("Student ID\tKorean\tMathmatics\tEnglish\n");
    for (int i = 0; i < size; i++) {
        printf("--------------------------------------------\n");
        printf("%10d\t%6d\t%10d\t%7d\n", (profile + i)->id, \
                (profile + i)->korean, (profile + i)->mathmatics, (profile + i)->english);
    }
    
    return;
}

```
