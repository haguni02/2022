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
* new 로 배열 할당하기
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

## 객체와 클래스 
* 클래스의 변수와 함수를 멤버 변수, 멤버 함수 라고 부른다 
* 클래스를 이용해 객체를 생성해야 프로그램 상에서 사용 가능하다 
* 객체의 변수와 함수를 인스턴스 변수, 인스턴스 메서드 라고 부른다 
* 컴퓨터 상에서 현실 세계를 100% 나타낼 수 없는 것이기 때문에, 적절하게 컴퓨터에서 처리할 수 있도록 바꾸는 추상화(abstraction) 과정이 필요하다 
* 객체의 상태를 나타내는 것을 변수로 추상화 하고, 객체의 행위를 함수로 추상화 할 수 있다  
* 외부에서 직접 인스턴스 변수의 값을 바꿀 수 없고 항상 인스턴스 메소드를 통해서 간접적으로 조절하는 것을 캡슐화(Encapsulation) 라고 부른다 
```cpp
#include <iostream>

class Animal {
 private:
  int food;
  int weight;

 public:
  void set_animal(int _food, int _weight) {
    food = _food;
    weight = _weight;
  }
  void increase_food(int inc) {
    food += inc;
    weight += (inc / 3);
  }
  void view_stat() {
    std::cout << "이 동물의 food   : " << food << std::endl;
    std::cout << "이 동물의 weight : " << weight << std::endl;
  }
};  // 세미콜론 잊지 말자!

int main() {
  Animal animal; // 클래스를 이용한 객체 생성 
  animal.set_animal(100, 50);
  animal.increase_food(30);

  animal.view_stat();
  return 0;
}
```
```
이 동물의 food   : 130
이 동물의 weight : 60
```

## 함수의 오버로딩 (Overloading)
* 함수 이름이 같아도 인자의 개수나 타입이 다르다면 다른 함수로 취급한다 
```cpp
/* 함수의 오버로딩 */
#include <iostream>

void print(int x) { std::cout << "int : " << x << std::endl; }
void print(double x) { std::cout << "double : " << x << std::endl; }

int main() {
  int a = 1;
  char b = 'c';
  double c = 3.2f;

  print(a);
  print(b);
  print(c);

  return 0;
}
```
```
int : 1
int : 99
double : 3.2
```
* print(b) 가 되는 이유는 함수의 오버로딩은 몇가지 규칙을 가지고 있기 때문이다 
> * 1단계 : 자신과 타입이 정확히 일치하는 함수를 찾는다
> * 2단계 : 정확히 일치하는 타입이 없는 경우 아래와 같은 형변환을 통해서 일치하는 함수를 찾아본다
>> * char, unsigned char, short 는 int 로 변환된다
>> * unsigned short 는 int 의 크기에 따라 int 혹은 unsigned int 로 변환된다
>> * float 은 double 로 변환된다
>> * enum 은 int 로 변환된다
> * 3단계 : 위와 같이 변환해도 일치하는 것이 없다면 아래의 좀더 포괄적인 형변환을 통해 일치하는 함수를 찾는다
>> * 임의의 숫자(numeric) 타입은 다른 숫자 타입으로 변환된다 (예를 들어 float -> int)
>> * enum 도 임의의 숫자 타입으로 변환된다 (예를 들어 enum -> double)
>> * 0 은 포인터 타입이나 숫자 타입으로 변환된 0 은 포인터 타입이나 숫자 타입으로 변환된다
>> * 포인터는 void 포인터로 변환된다
> * 4단계 : 유저 정의된 타입 변환으로 일치하는 것을 찾는다
> * 만약에 컴파일러가 위 과정을 통하더라도 일치하는 함수를 찾을 수 없거나 같은 단계에서 두 개 이상이 일치하는 경우에 모호하다 (ambiguous) 라고 판단해서 오류를 발생하게 된다
