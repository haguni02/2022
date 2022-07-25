## std::ios::sync_with_stdio(false);
* 기본적으로, 모든 표준 stream들은 동기화 되어있어 C와 C++의 입출력방식을 자유롭게 혼용할 수 있는데 C 표준 stream과 C++ 표준 stream의 동기화를 끊는다 
* 동기화를 끊는다면, C++ stream들은 독립적인 버퍼를 갖게되며, 버퍼의 수가 줄어들기 때문에 실행속도 자체는 향상 된다 
* C와 C++의 입출력방식을 혼용해서 사용할 경우 의도한대로 입출력이 되지 않을 수 있다 

## cin.tie(NULL);
* 기본적으로 cin 과 cout 은 서로 묶여있는데 이 묶음을 untie 해준다 
* tie 일 때 stream 을 사용하고 다른 stream 을 사용할 경우 버퍼 내용을 비워주는데 untie 일 경우 이 과정을 생략하므로 입/출력 실행속도가 빨라진다 
* 출력하고 싶을 때 stream을 수동으로 flush 해줘야한다
