出错代码
//单调栈（每日温度）
#include <stdio.h>
#include <stdlib.h>

int* dailyTemperatures(int* temperatures, int temperaturesSize, int* returnSize) {
    //创建单调栈，分配动态内存
    int* stack=(int*)malloc(temperaturesSize*sizeof(int));
    if (stack == NULL) {
        printf("fail");
    }

    int stacktop = -1;


    int* result = (int*)malloc(temperaturesSize * sizeof(int));
    if (result == NULL) {
        printf("fail");
    }

    for (int i = 0; i < temperaturesSize; i++) {

        int n = temperatures[i];

        while (stacktop>=0 && n >temperatures[stack[stacktop]]) {
            result[stack[stacktop]] = i - stack[stacktop];

            //移除栈顶元素
            stacktop--;

        }

        stack[stacktop++] = i;

    }

    return result;

}


int main() {

    int temperatures[] = { 73, 74, 75, 71, 69, 72, 76, 73 };
    int temperaturesSize = sizeof(temperatures) / sizeof(temperatures[0]);
    int returnSize;

    int* result = dailyTemperatures(temperatures, temperaturesSize, &returnSize);

    printf("结果数组：");
    for (int i = 0; i < temperaturesSize; i++) {
        printf("%d ", result[i]);
    }
    printf("");

    free(result);
    free(temperatures);

    return 0;
}

