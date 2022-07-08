## References
```
There shall be no references to references, no arrays of references, and no pointers to references

레퍼런스의 레퍼런스,레퍼런스의 배열, 레퍼런스의 포인터는 존재할 수 없다.
```
* 문법 상 배열의 이름은 (arr) 첫 번째 원소의 주소값으로 변환이 될 수 있어야 arr[1] 과 같은 문장이 *(arr + 1) 로 바뀌어서 처리될 수 있는데, 레퍼런스는 특별한 경우가 아닌 이상 메모리 상에서 공간을 차지 하지않기 때문에 레퍼런스의 배열은 존재할 수 없다 
* 배열의 레퍼런스는 가능하다 
```cpp
#include <iostream>

int main() {
  int arr[3] = {1, 2, 3};
  int(&ref)[3] = arr;

  ref[0] = 100;
  ref[1] = 200;
  ref[2] = 300;

  std::cout << arr[0] << arr[1] << arr[2] << std::endl;
  return 0;
}
```
```
100200300
```

### 메모리 할당 
* 메모리를 할당하기 위해 런타임에 프로그래머가 자유롭게 할당하고 해제할 수 있는 메모리 공간인 heap 이 있다 
* 파일러에 의해 어느정도 안정성이 보장되는 스택(stack) 과는 다르게 힙은 사용자가 스스로 제어해야 하는 부분인 만큼 책임이 따른다 
* C 언어에서는 malloc 과 free 함수를 지원하여 힙 상에서의 메모리 할당을 지원하고, C++ 에서는 new 와 delete 키워드로 메모리 할당을 지원한다 
```
T* pointer = new T;
```
```cpp
/* new 와 delete 의 사용 */
#include <iostream>

int main() {
  int* p = new int;
  *p = 10;

  std::cout << *p << std::endl;

  delete p;
  return 0;
}
```
```
10
```
```
T* pointer = new T[size];
```
```cpp
/* new 로 배열 할당하기 */

#include <iostream>

int main() {
  int arr_size;
  std::cout << "array size : ";
  std::cin >> arr_size;
  int *list = new int[arr_size];
  for (int i = 0; i < arr_size; i++) {
    std::cin >> list[i];
  }
  for (int i = 0; i < arr_size; i++) {
    std::cout << i << "th element of list : " << list[i] << std::endl;
  }
  delete[] list;
  return 0;
}
```
```
array size : 5
1
4
2
6
8
0th element of list : 1
1th element of list : 4
2th element of list : 2
3th element of list : 6
4th element of list : 8
```
