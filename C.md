## 배열과 포인터 
* sizeof 와 주소값 연산자(&)와 함께 사용할 때를 제외하면, 배열의 이름은 첫 번째 원소를 가리키는 포인터로 타입 변환된다.
* arr[i] 와 같은 문장은 사실 컴파일러에 의해 *(arr + i) 로 변환된다.

## 배열 포인터 
* 배열을 가르키는 포인터 
```cpp
#include <stdio.h>

int main() {
  int arr[3] = {1, 2, 3};
  int (*parr)[3] = &arr;

  printf("arr[1] : %d \n", arr[1]);
  printf("parr[1] : %d \n", (*parr)[1]);
}
```
```
arr[1] : 2 
parr[1] : 2  
```
* &arr 은 첫 번째 원소를 가르키는 포인터로 형 변환되지 않고, int 형 3개를 가지는 한 덩어리(4바이트 * 3 = 12바이트) 배열을 가르키는 포인터 그 자체로 사용된다
* int (*parr)[3] 의 의미도 (int 크기 * 3) 배열을 가르키는 포인터로 사용하기 위해 만들었다 
* parr 은 12 바이트 크기의 배열의 첫번째 주소를 가르키고 *parr 은 배열의 이름인 arr 과 같은 의미를 갖는다

## 이차원 배열의 주소값 
* 이차원 배열도 메모리상에서는 일차원 배열과 똑같이 선형으로 나열되어 있는 형태이고, 단지 데이터에 접근할 때 인덱스 두개로 표현하는 것 뿐이다 
* int arr[a][b] 라고 정의된 2 차원 배열이 있다면, int arr[b] 짜리 배열이 메모리에 a 번 나열된 것이라 생각하면 된다 
* 이차원 배열의 x행 y열에 있는 arr[x][y] 의 시작 주소값은 arr + 4bx + 4y 가 되기 때문에 arr[x][y] 의 주소값을 정확히 계산하기 위해서는 x, y 뿐만이 아니라 b 가 뭔지 알아야 한다는 점이다
```cpp
#include <stdio.h>
int main() {
  int arr[2][3] = {{1, 2, 3}, {4, 5, 6}};
  int(*parr)[3];  // 괄호를 꼭 붙이세요

  parr = arr;  // parr 이 arr 을 가리키게 한다.

  printf("parr[1][2] : %d , arr[1][2] : %d \n", parr[1][2], arr[1][2]);

  return 0;
}
```
```
parr[1][2] : 6 , arr[1][2] : 6 
```

## 포인터 배열
```cpp
#include <stdio.h>
int main() {
  int *arr[3];
  int a = 1, b = 2, c = 3;
  arr[0] = &a;
  arr[1] = &b;
  arr[2] = &c;

  printf("a : %d, *arr[0] : %d \n", a, *arr[0]);
  printf("b : %d, *arr[1] : %d \n", b, *arr[1]);
  printf("b : %d, *arr[2] : %d \n", c, *arr[2]);

  return 0;
}
```
```
a : 1, *arr[0] : 1 
b : 2, *arr[1] : 2 
b : 3, *arr[2] : 3 
```
