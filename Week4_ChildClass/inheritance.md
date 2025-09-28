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
---
---
# 다중 상속
## 7. 다음과 같은 코드에서 두 부모를 상속받을 때, 부모의 오버라이딩된 함수를 어떻게 구분하는지 해결하기
```c++
#include <iostream>
using namespace std;

class Teacher {
public:
    void teach() { cout << "강의를 하고 있습니다." << endl; }
    void introduce() { cout << "저는 선생님입니다." << endl; }
};

class Researcher {
public:
    void research() { cout << "연구를 하고 있습니다." << endl; }
    void introduce() { cout << "저는 연구원입니다." << endl; }
};

// 다중 상속
class Professor : public Teacher, public Researcher {
public:
    void introduce() { cout << "저는 교수입니다." << endl; }
};

int main() {
    Professor p;
    p.introduce();
    p.teach();
    p.research();

    return 0;
}
```
```
실행결과

저는 교수입니다.
강의를 하고 있습니다.
연구를 하고 있습니다.
```
이 코드에서 main() 함수 내에서 다음과 같이 사용하면 구분해서 호출할 수 있다.


```c++
int main() {
    Professor p;
    p.introduce();
    p.teach();
    p.research();

    p.Teacher::introduce();     //상속 받은 Teacher 클래스의 introduce() 호출
    p.Researcher::introduce();  //상속 받은 Researcher 클래스의 introduce() 호출
    return 0;
}
```
```
실행결과

저는 교수입니다.
강의를 하고 있습니다.
연구를 하고 있습니다.
저는 선생님입니다.
저는 연구원입니다.

```
네임스페이스 접근 지정자로 구분하여 따로 호출할 수 있다.


---
## 8. 7번 코드는 오버라이딩에서 다형성과 관련된 것으로, 자식은 함수가 총 1개를 가지고 있다. 문제가 발생하는 부분을 수정해봐라.
```c++
#include <iostream>
using namespace std;

class Animal {
public:
    // 가상 함수
    void speak() { cout << "동물이 소리를 냅니다." << endl; }
};

class Dog : public Animal {
public:
    void speak() override { cout << "멍멍!" << endl; }
};

class Cat : public Animal {
public:
    void speak() override { cout << "야옹!" << endl; }
};

int main() {
    Animal a1;
    Dog a2;
    Cat a3;

    a1.speak();
    a2.speak();
    a3.speak();  

    return 0;
}
```
- 다형성이란, 하나의 형태에서 여러 형태로 가지게 되는 것이다.
  - 예시로 우리가 알고 있는 함수 오버로딩, 오버라이딩이 있다.
- 해당 문제에선 12, 17줄처럼 speak 함수가 override 키워드가 사용된 것을 확인할 수 있는데,이 키워드는 가상 함수(virtual)과 함께 사용되는 키워드다.
  - 가상 함수는 부모 클래스에서 virtual 키워드를 사용한 멤버 함수를 말하며,     자식 클래스가 해당 함수를 재정의해 실제 호출하는 함수는 재정의한 함수가 호출하도록 만든다.
    - 즉, 함수 오버라이딩에서 활용하는 기능으로, 인스턴스의 자료형에 맞는 함수를 호출하게 된다.\n

\
