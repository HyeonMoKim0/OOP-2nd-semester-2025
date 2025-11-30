3. 사각형을 표현하는 클래스를 정의하고 클래스를 vector 를 이용하여 저장하고 처리하는 프로그램을 작성하라.

```C++
#include <iostream>
#include <vector>
using namespace std;

class Rectangle {
private:
	double width, height;

public:
	Rectangle(double w, double h) : width(w), height(h) {}
	double getWidth() const { return width; }
	double getHeight() const { return height; }
	double setWidth(double w) { return width = w; }
	double setHeight(double h) { return height = h; }
};

int main() {
	vector<Rectangle> rect;

	rect.push_back(Rectangle(2.0, 4.0));
	cout << rect[0].getWidth() << " " << rect[0].getHeight() << endl;

	//rect[0].setWidth(3.0);
	rect.at(0).setWidth(4.0); // rect[0]와 rect.at(0)는 비슷하나, at() 함수는 범위 검사를 수행한다는 차이가 존재 -> 안전함
	rect.at(0).setHeight(8.0);

	cout << rect[0].getWidth() << " " << rect[0].getHeight() << endl;
	//cout << rect.at(1).getWidth() << " " << rect.at(1).getHeight() << endl; // 실수로 범위를 침범해도 예외 처리가 발생
	return 0;
}
```

---
4. 다음 프로그램의 실행 결과를 분석하라.
```C++
#include <vector>
#include <iostream>
using namespace std;

int main() {
	vector<int> v1(5);
	v1.push_back(3);

	cout << v1.capacity() << endl;
	cout << v1.size() << endl;

	cout << v1.at(5) << endl;

	cout << v1.at(0) << endl; 

	return 0;
}
```

---
6. 4의 프로그램에서 첫 번째 위치에 데이터 10을 저장하는 프로그램을 작성하라.
```C++
#include <vector>
#include <iostream>
using namespace std;

int main() {
	vector<int> v1(5);
	v1.push_back(3);

	cout << v1.capacity() << endl;
	cout << v1.size() << endl;

	cout << v1.at(5) << endl;

	v1.insert(v1.begin(), 10); // 6번 문제 적은 것
	cout << v1.at(0) << endl; 

	return 0;
}
```

---
7. 아래의 링크를 참조하여 vector 클래스의 다른 멤버 함수와 연산자를 활용한 프로그램을 작성하라.
```C++
#include <vector>
#include <iostream>
using namespace std;

int main() {
	vector<int> v1, v2;
	v1.push_back(10); v2.push_back(20);

	// operator!= 연산자 오버로딩, 포함된 요소 수와 값이 같으면 두 벡터가 같은 것, 아니면 다른 것
	if (v1 != v2) cout << "v1 != v2" << endl;
	else cout << "v1 == v2" << endl;

	v1.insert(v1.begin(), 20); // v2의 첫 번째 요소와 같게 만듦
	v1.push_back(30); v2.push_back(40);
	// operator< 연산자 오버로딩, 첫 번째 요소를 먼저 비교해서 같으면, 두 번째 요소도 계속 비교해나감
	if (v1 < v2) cout << "v1 < v2" << endl;
	else cout << "v1 >= v2" << endl;

	// operator<= 연산자 오버로딩, operator<와 비슷하며 첫 번째 요소만 비교
	if (v1 <= v2) cout << "v1 <= v2" << endl;
	else cout << "v1 > v2" << endl;

	// operator> 연산자 오버로딩, operator<와 같은 작동 방식
	if (v1 > v2) cout << "v1 > v2" << endl;
	else cout << "v1 <= v2" << endl;

	// operator>= 연산자 오버로딩, operator<=와 같은 작동 방식
	if (v1 >= v2) cout << "v1 >= v2" << endl;
	else cout << "v1 < v2" << endl;

	vector<int> v3, v4;
	v3.push_back(10);
	v4.push_back(10); v4.push_back(20);
	// operator== 연산자 오버로딩, 모든 요소 개수와 값이 같으면 true
	if (v3 == v4) cout << "v1 == v2" << endl;
	else cout << "v1 != v2" << endl;

	return 0;
}
```

---
8. SampleCodes/STL 디렉토리의 vector_sample.cc 파일을 기반으로 vector 클래스의 멤버 함수를 검증하는 함수를 작성하라.
```C++
#include <iostream>
#include <vector>
using namespace std;

void assignTest() {
    vector <int> v1, v2, v3, v4;

    v1.push_back(10); v1.push_back(20);
    v1.push_back(30); v1.push_back(40);
    v1.push_back(50);

    cout << "the value of elements of v1 " << endl;
    for (auto& e : v1) cout << e << ",";
    cout << endl;
    cout << "the capacity of v1: " << v1.capacity() << endl;
    cout << "the value of elements of v2 after assign" << endl;
    v2.assign(v1.begin(), v1.end());

    cout << "the size of v2: " << v2.size() << endl;
    cout << "the capacity of v2: " << v2.capacity() << endl;

    for (auto& e : v1) cout << e << ",";
    cout << endl;

    v3.assign(10, 3);
    cout << "the result of v3.assign(7 , 3): " << endl;
    cout << "the size of v3: " << v3.size() << endl;
    cout << "the capacity of v3: " << v3.capacity() << endl;

    for (auto& e : v3) cout << e << ", ";
    cout << endl;

    v4.assign({ 5, 6, 7, 8 });
    cout << "the result of v4.assign({5, 6, 7}): " << endl;
    cout << "the size of v4: " << v4.size() << endl;
    cout << "the capacity of v4: " << v4.capacity() << endl;

    for (auto& e : v4) cout << e << ", ";
    cout << endl;

}

void itrTest() {
    vector <int> v1;
    vector <int>::iterator v1_itr;
    vector <int>::const_iterator v1_citer;

    v1.push_back(10); v1.push_back(20);
    v1.push_back(30); v1.push_back(40);
    v1.push_back(50);

    v1_itr = v1.begin();
    cout << "Access the data through the iterator" << endl;
    for (; v1_itr != v1.end(); v1_itr++) cout << *v1_itr << ", ";
    cout << endl;

    v1_itr = v1.begin();
    cout << "Add 100 to every element in the vector through the iterator" << endl;
    for (; v1_itr != v1.end(); v1_itr++) *v1_itr += 100; // for문의 증감 연산자에 v1_itr++이라 되어 있는데, 주솟값 증가시키는 방법은 전치 후치 연산자로만 가능

    cout << "Accee the element with range-for loop in the vector" << endl;
    for (auto& e : v1) cout << e << ", ";
    cout << endl;

    cout << "Accee the element with for loop in the vector" << endl;
	for (int i = 0; i < v1.size(); i++) cout << v1[i] << ", "; //v1[i]보단 v1.at(i)가 더 안전
    cout << endl;
}

void sizeTest() {
    vector <int> v1;
    v1.push_back(10);
    v1.push_back(20);
    v1.push_back(30);
    cout << "size of vector: " << v1.size() << endl;
}

void capacityTest() {
    vector <int> v1;
    v1.push_back(10);
    v1.push_back(20);
    v1.push_back(30);
    cout << "capacity of vector: " << v1.capacity() << endl;
}

void atTest() {
    vector <int> v1;
    v1.push_back(10);
    v1.push_back(20);
    v1.push_back(30);

    int& e = v1.at(1);

    cout << e << endl;
    e = 60;
    cout << v1[1] << endl;

}

void backTest() { // 검증할 함수 
    vector<int> v1;

	v1.push_back(10);
    v1.push_back(20);
    cout << v1.back() << endl;

    v1.push_back(30);
	cout << v1.back() << endl; // 해당 vector 변수의 맨 뒤의 원소를 반환
}

void beginTest() { // 검증할 함수
    vector<int> v1;

    v1.push_back(10);
    cout << *(v1.begin()) << endl;

    v1.push_back(20);
    cout << *(v1.begin()) << endl; // 해당 vector 변수의 맨 앞의 원소를 반환
}

void endTest() { // 검증할 함수
    vector<int> v1;

    v1.push_back(10);
    cout << *(v1.end() - 1) << endl;

    v1.push_back(20);
    cout << *(v1.end() - 1) << endl; // 해당 vector 변수의 맨 뒤의 원소 + 1 위치의 반환, 따라서 따로 -1 처리해야 함

}

void clearTest() { // 검증할 함수
    vector<int> v1;

    v1.push_back(10);
    cout << v1.at(0) << " v1 size: " << v1.size() << " v1 capacity: " << v1.capacity() << endl;

    v1.clear(); //v1에 있는 모든 요소를 없애지만, capacity는 그대로
    cout << " v1 size: " << v1.size() << " v1 capacity: " << v1.capacity() << endl;
}

int main(int argc, char const* argv[]) {
    //itrTest();
    //assignTest();

    backTest();
    cout << endl;
    
    beginTest();
    cout << endl;
    
    endTest();
    cout << endl;

    clearTest();
    return 0;
}
```
