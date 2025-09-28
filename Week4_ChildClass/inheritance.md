# 단일 상속
## 1. 깃허브의 단일 상속 코드 구동
```c++
#include <iostream>
#include <string>
using namespace std;

// 부모 클래스 (기반 클래스)
class Person {
protected:
    string name;
    int age;

public:
    Person(string n, int a) : name(n), age(a) {}
    void introduce() { cout << "이름: " << name << ", 나이: " << age << endl; }
};

// 자식 클래스 (파생 클래스)
class Student : public Person {
private:
    string major;

public:
    Student(string n, int a, string m) : Person(n, a), major(m) {}
    void study() { cout << name << " 학생이 " << major << " 전공 공부 중입니다." << endl; }
};

int main() {
    Student s("홍길동", 21, "컴퓨터공학");
    s.introduce();   // 부모 클래스 함수 사용
    s.study();       // 자식 클래스 함수 사용

    return 0;
}
```

```
실행결과

이름: 홍길동, 나이: 21
홍길동 학생이 컴퓨터공학 전공 공부 중입니다.
```


--- 
## 2. Student가 상속 받는 부모의 접근 지정자를 private으로 변경하고 구동
```c++
#include <iostream>
#include <string>
using namespace std;

// 부모 클래스 (기반 클래스)
class Person {
protected:
    string name;
    int age;

    void introduce() { cout << "이름: " << name << ", 나이: " << age << endl; }

public:
    Person(string n, int a) : name(n), age(a) {}

};

// 자식 클래스 (파생 클래스)
class Student : private Person {
private:
    string major;

public:
    Student(string n, int a, string m) : Person(n, a), major(m) {}
    void study() { cout << name << " 학생이 " << major << " 전공 공부 중입니다." << endl; }
};

int main() {
    Student s("홍길동", 21, "컴퓨터공학");
    s.introduce();   // 부모 클래스 함수 사용
    s.study();       // 자식 클래스 함수 사용

    return 0;
}
```
이 경우 부모의 멤버에 접근이 불가능하므로 문제가 발생한다.


---
## 3. 2번에 발생하는 오류 해결하기
```c++
#include <iostream>
#include <string>
using namespace std;

// 부모 클래스 (기반 클래스)
class Person {
protected:
    string name;
    int age;

    void introduce() { cout << "이름: " << name << ", 나이: " << age << endl; }

public:
    Person(string n, int a) : name(n), age(a) {}

};

// 자식 클래스 (파생 클래스)
class Student : public Person {
private:
    string major;

public:
    Student(string n, int a, string m) : Person(n, a), major(m) {}
    void study() { cout << name << " 학생이 " << major << " 전공 공부 중입니다." << endl; }
    void introduce() { cout << "이름: " << name << ", 나이: " << age << endl; }
};

int main() {
    Student s("홍길동", 21, "컴퓨터공학");
    s.introduce();   // 부모 클래스 함수 사용
    s.study();       // 자식 클래스 함수 사용

    return 0;
}
```

```
실행결과

이름: 홍길동, 나이: 21
홍길동 학생이 컴퓨터공학 전공 공부 중입니다.
```
부모의 멤버 함수를 오버라이딩함으로써 해결하는 방법이 있다.


---
## 4. 1번의 코드를 Student가 상속받는 부모의 접근 지정자를 private으로 변경하고 구동
```c++
#include <iostream>
#include <string>
using namespace std;

// 부모 클래스 (기반 클래스)
class Person {
protected:
    string name;
    int age;

public:
    Person(string n, int a) : name(n), age(a) {}
    void introduce() { cout << "이름: " << name << ", 나이: " << age << endl; }
};

// 자식 클래스 (파생 클래스)
class Student : private Person {
private:
    string major;

public:
    Student(string n, int a, string m) : Person(n, a), major(m) {}
    void study() { cout << name << " 학생이 " << major << " 전공 공부 중입니다." << endl; }
};

int main() {
    Student s("홍길동", 21, "컴퓨터공학");
    s.introduce();   // 부모 클래스 함수 사용
    s.study();       // 자식 클래스 함수 사용

    return 0;
}
```
이 경우 부모의 멤버에 접근이 불가능하므로 문제가 발생한다.


---
## 5. 4번 코드에서 상속받을 부모의 접근 지정자를 protected로 변경 후 구동
```c++
#include <iostream>
#include <string>
using namespace std;

// 부모 클래스 (기반 클래스)
class Person {
protected:
    string name;
    int age;

public:
    Person(string n, int a) : name(n), age(a) {}
    void introduce() { cout << "이름: " << name << ", 나이: " << age << endl; }
};

// 자식 클래스 (파생 클래스)
class Student : protected Person {
private:
    string major;

public:
    Student(string n, int a, string m) : Person(n, a), major(m) {}
    void study() { cout << name << " 학생이 " << major << " 전공 공부 중입니다." << endl; }
};

int main() {
    Student s("홍길동", 21, "컴퓨터공학");
    s.introduce();   // 부모 클래스 함수 사용
    s.study();       // 자식 클래스 함수 사용

    return 0;
}
```
이 경우도 부모 멤버 변수를 호출하는 과정에서 문제가 발생한다.
protected는 부모에게 상속 받은 자식 내에서만 부모의 멤버에 접근할 수 있게 되는 키워드이기에, 자신을 벗어난 외부에서 부모의 멤버 접근을 불가능하게 된다.


---
## 6. 4번 코드에서 상속받을 부모의 접근 지정자를 public으로 변경 후 구동
이 경우, 자식 내부에서 부모 멤버에 접근하거나, 자식 외부에서 접근하는 경우가 가능해진다.
해당 코드로 수정할 경우, 1번의 코드와 다를 바가 없다.


---
## 7. 
