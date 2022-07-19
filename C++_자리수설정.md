```cpp
#include <iostream>

#include <iostream>

int main()
{
  double a = 3333.333333;
  double b = 1234567.89;
 
  std::cout.precision(6);                   // * 실수 전체 자리수 6개로 설정 
 
  std::cout << a << std::endl;			        // 3333.33 이 출력됨
  std::cout << b << std::endl;              // 1.23457e+06 이 출력됨
 
  std::cout << std::fixed;	                // * 고정 소수점 표기로 전환
  
  std::cout << a << std::endl;			        // 3333.333333 이 출력 됨
  std::cout << b << std::endl;              // 1234567.890000 이 출력됨
  
  std::cout.unsetf(std::ios::fixed);	      // * 고정 소수점 표기 해제
  
  std::cout << a << std::endl;			        // 3333.33 이 출력됨
  std::cout << b << std::endl;              // 1.23457e+06 이 출력됨
  
  return 0;
}
```
* 실행 결과 
```
3333.33
1.23457e+06
3333.333333
1234567.890000
3333.33
1.23457e+06
```
