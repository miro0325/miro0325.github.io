---
title: Structure&Class
date: YYYY-MM-DD HH:MM:SS +09:00
categories: [PORTPOLIO]
tags:
  [
    CS,
    Study
  ]
comments: false
math: true
mermaid: true
---

## 공부 내용

### C++

C++에서 struct와 class는 모두 사용자 데이터 타입을 정의할 때 사용된다.

struct와 클래스 둘다 멤버와 함수를 지닐 수 있다. 그러나 일반적으로 struct는 데이터 집합체로,
class는 객체 지향 프로그래밍에서 객체의 정의를 위해 사용한다.

struct와 class의 주요 차이점은 기본 제어 접근 수준이다. struct는 기본적으로 public으로 정의되며, 
class는 기본적으로 private로 정의됩니다.

private과 public 두 키워드는 초기화의 방법 차이를 발생시킨다.


struct는 멤버 변수 및 함수가 외부에 쉽게 접근 가능하도록 하는게 좋지만, class는 기본적으로 멤버 변수 및 함수에 대한 접근을 제한합니다.

**Struct**
```cpp
struct Position {
    int x;
    int y;
};

Position MultiplyPosition(Position pos1,Position pos2) {
    Position pos;
    pos.x = pos1.x * pos2.x;
    pos.y = pos1.y * pos2.y;
    return pos;
}

int main() {
  Position pos1 = {1,2};
  Position pos2 = {2,1};
  Position result;
  result = MultiplyPosition(pos1,pos2);
  return 0;
}
```
**Class**
```cpp
class Position {
    private:
      int x;
      int y;
    public:
      Position(int _x, int _y) {
        x = _x;
        y = _y;
      }
      int GetX() {
        return x;
      }
      int GetY() {
        return y;
      }

      Position MultiplyPosition(Position pos1, Position pos2) {
        int x = pos1.GetX() * pos2.GetX();
        int y = pos1.GetY() * pos2.GetY();
        Position pos(x,y); 
        return pos;
      }
};

int main() {
  Position pos1 = Positon(1,2);
  Position pos2 = Positon(2,1);
  Position newPos = pos1.MultiplyPosition(pos1,pos2);
  return 0;
}
```

### C#

C#에서 struct와 class의 차이는 Type의 차이를 지니고 있다.

구조체는 값 타입  
- 스텍 메모리에 생성  
클래스는 참조 타입  
- 힙 메모리에 생성  


#### 예시
```csharp
public struct TestStruct
{
    public int num;
}

public class TestClass
{
    public int num;
}

class Program
{
    public static void SetStruct(TestStruct test)
    {
        test.num = 1;
    }

    public static void SetClass(TestClass test)
    {
        test.num = 1;
    }

    static void Main(string[] args)
    {
        TestStruct testStruct = new TestStruct();
        testStruct.num = 0;
        TestClass testClass = new TestClass();
        testClass.num = 0;

        SetStruct(testStruct);
        SetClass(testClass);

        Console.WriteLine("Struct " + testStruct.num);
        Console.WriteLine("Class " + testClass.num);
    }
}
```
**출력**
```
Struct 0
Class 1
```

#### 구조체

구조체는 값 타입이기에 스택에 복사된 값이 함수에게 전달되어, 함수 내에서 값을 변경한다 하더라도 복사된 값이 변경될 뿐, 원본 값까지 영향을 받지 않는다.

구조체는 생성자는 선언할 수 있으나 반드시 파라미터가 있어야만한다.

구조체는 상속이 불가능하다.

구조체는 필드 선언 시 const 또는 static인 경우에만 초기화가 가능하다.

new 키워드를 사용하지 않고 인스턴스화 할수 있다.

구조체는 스택에 할당되기 때문에 GC가 발생하지 않는다.

너무 많은 변수들을 가지고 있는 구조체는 사용하지 않는다.  
구조체는 변수 값을 모두 스택에 저장하는데, 스택은 크기가 제한적이므로 너무 많은 양을 가지게 되면 스택 오버플로우가 발생할수 있다.

따라서 구조체는 변수의 크기가 작거나, 수명이 짧고, 자주 할당되는 객체는 구조체로 만들어주는 것이 좋다.
예를 들어 유니티에서는 `position, color, quaternion, rotation, scale`등이 구조체로 구현되있다.

#### 클래스

클래스는 참조 타입이기에 힙의 주소를 전달하여, 함수 내에서 값을 변경할 시 주소를 따라 원본 값이 변경된다.

클래스는 인스턴스를 생성할 때 마다 힙 메모리에 할당하기 때문에 값을 지우기 위해서는 GC가 필요하다.


#### 참고 자료

<https://sunshower99.tistory.com/27>
<https://funfunhanblog.tistory.com/96>