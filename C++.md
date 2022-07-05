## 이름 공간(namespace) 
* 라이브러리가 많아지면서 이름이 중복되는 변수나 함수가 나타나 이름이 충돌되는 현상이 발생하므로 이름 공간을 통해 소속을 지정해주어 이름 충돌을 방지한다 
```cpp
// header1.h 의 내용
namespace header1 
{
int foo();
void bar();
}
```
```cpp
// header2.h 의 내용
namespace header2 
{
int foo();
void bar();
}
```
```cpp
#include "header1.h"
#include "header2.h"

namespace header1 
{
int func() 
{
  foo();           // 알아서 header1::foo() 가 실행된다.
  header2::foo();  // header2::foo() 가 실행된다.
}
}  // namespace header1
```
* 자기 자신이 포함되어 있는 이름 공간 안에서는 굳이 앞에 이름 공간을 명시하지 않고 자유롭게 부를 수 있다
```cpp
#include "header1.h"
#include "header2.h"

using header1::foo;
int main() {
  foo();  // header1 에 있는 함수를 호출
}
```
* header1 의 foo 함수를 이름 공간을 명시하지 않고 사용할 때 using 키워드를 통해 선언할 수 있다 
```cpp
#include "header1.h"
#include "header2.h"

using namespace header1;
int main() {
  foo();  // header1 에 있는 함수를 호출
  bar();  // header1 에 있는 함수를 호출
}
```
* header1의 정의된 모든 함수를 이름 공간을 명시하지 않고 사용하고 싶을때는 using 키워드로 using namespace header1;  

## 이름 없는 이름 공간 
```cpp
#include <iostream>

namespace 
{
// 이 함수는 이 파일 안에서만 사용할 수 있습니다.
// 이는 마치 static int OnlyInThisFile() 과 동일합니다.
int OnlyInThisFile() {}

// 이 변수 역시 static int x 와 동일합니다.
int only_in_this_file = 0;
}  // namespace

int main() 
{
  OnlyInThisFile();
  only_in_this_file = 3;
}
```
