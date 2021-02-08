---
title: "C++ STL Sort"
date: 2020-10-22 17:29:21
tag: C++
---

> 평소 알고리즘 문제를 파이썬으로 푸는데 코딩테스트에서 파이썬을 지원해주지 않아서 급하게 C++을 공부하고 시험을 봤다. 결과는 sort함수 사용법을 잘 몰라서 한문제를 풀지 못했다 ㅠㅠ 그래서 공부 겸 정리 ! 

# 정의

알고리즘 헤더파일에서 제공하는 STL로써 범위내에서 주어진 원소들을 정렬한다. 정렬하는 방식은 오름차순, 내림차순 등이 있으며 Default는 오름차순이고, 동일한 원소에 대해서는 순서가 보장되지 않는다. 숫자뿐만 아니라 대소 비교가 가능한 모든 원소(char, string 등)를 정렬할 수 있다.

<br>

# 사용법

```C++
template <class RandomAccessIterator>
  void sort (RandomAccessIterator first, RandomAccessIterator last);
template <class RandomAccessIterator, class Compare>
  void sort (RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

* 2개 또는 3개의 argument를 필요로 한다. `first`와 `last`는 iterator로써 범위를 나타낸다. 두 **개의 객체를 비교해서 `first`가 `last`보다 작으면 true 그렇지 않다면 false를 리턴한다.** 

* `comp`에는 `greater<>()` 와 `less<>()`가 들어갈 수 있다. (예제는 아래에)

  * `greater<>()`

    ```C++
    // greater는 첫번째 인자가 두번째 인자보다 크면 true를 반환한다.
    cout << greater<int>()(10, 20) << endl; // true
    cout << greater<int>()(20, 10) << endl; // false
    ```

  * `less<>()`

    ```C++
    // less는 첫번째 인자가 두번째 인자보다 크면 true를 반환한다.
    cout << less<int>()(10, 20) << endl; // false
    cout << less<int>()(20, 10) << endl; // true
    ```

<br>

# 소스예제

* **기본 정렬 예제**

  ```C++
  #include <iostream>
  #include <algorithm>
  
  using namespace std;
  
  int main(){
  
      int arr[5];
      arr[0] = 0;
      arr[1] = 4;
      arr[2] = 3;
      arr[3] = 1;
      arr[4] = 5;
      sort(arr, arr + 5); // Default : 오름차순
  
      for (int i = 0; i < 5; i++)
          cout << arr[i] << endl;
      return 0;
  }
  ```

  결과

  ```C++
  0
  1
  2
  3
  4
  5
  ```

* **정렬(greater)**

  ```C++
  #include <iostream>
  #include <algorithm>
  
  using namespace std;
  
  int main(){
  
      int arr[5];
      arr[0] = 0;
      arr[1] = 4;
      arr[2] = 3;
      arr[3] = 1;
      arr[4] = 5;
      sort(arr, arr + 5, greater<int>());
  
      for (int i = 0; i < 5; i++)
          cout << arr[i] << endl;
      return 0;
  }
  ```

  결과

  ```C++
  5
  4
  3
  2
  1
  0
  ```

* **정렬(less)**

  ```c++
  #include <iostream>
  #include <algorithm>
  
  using namespace std;
  
  int main(){
  
      int arr[5];
      arr[0] = 0;
      arr[1] = 4;
      arr[2] = 3;
      arr[3] = 1;
      arr[4] = 5;
      sort(arr, arr + 5, less<int>());
  
      for (int i = 0; i < 5; i++)
          cout << arr[i] << endl;
      return 0;
  ```

  결과

  ```C++
  0
  1
  2
  3
  4
  5
  ```

* **사용자 정의 정렬 (이름을 기준으로 내림차순 정렬)**

  ```C++
  #include <iostream>
  #include <vector>
  #include <algorithm>
  #include <string>
  
  using namespace std;
  
  class Person{
  public:
      string name;
      int age;
      Person(string name, int age){
          this->name = name;
          this->age = age;
      }
  };
  
  bool cmp(const Person &a, const Person &b){
      return a.name > b.name; // 부등호를 바꾸면 오름차순 정렬
  }
  
  int main(){
      vector<Person> v;
      v.push_back(Person("Ace", 22));
      v.push_back(Person("Luffy", 28));
      v.push_back(Person("Zoro", 26));
      v.push_back(Person("Robin", 25));
      v.push_back(Person("Brook", 40));
      sort(v.begin(), v.end(), cmp);
      for (int i = 0; i < v.size(); i++)
          cout << v[i].age  << ", " <<  v[i].name << endl;
  }
  ```

  결과

  ```C++
  26, Zoro
  25, Robin
  28, Luffy
  40, Brook
  22, Ace
  ```

* **사용자 정의 정렬(숫자를 기준으로 오름차순 정렬)**

  ```C++
  #include <iostream>
  #include <algorithm>
  
  using namespace std;
  
  bool asc(int a, int b) {
    return a < b;
  }
  
  int main(void){
    int data[5] = {2, 3, 4, 1, 5};
    
    sort(data, data+5, asc);
    for(int i=0; i< 5; i++){
      cout << data[i] << endl;
    }
    return 0;
  }
  ```

  결과

  ```C++
  1
  2
  3
  4
  5
  ```

  <br>

출처 : (https://www.acmicpc.net/blog/view/22) , (https://hongku.tistory.com/153), (https://hyeonstorage.tistory.com/315)