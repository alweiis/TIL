# java.lang 패키지
### java.lang 패키지의 클래스들은 import문 없이도 사용할 수 있다.
<br>

## Object 클래스
- Object 클래스는 모든 클래스의 최고 조상
- Object 클래스의 멤버들은 모든 클래스에서 바로 사용 가능
- Object 클래스는 멤버변수는 없고 오직 11개의 메서드만 가지고 있다.
> **protected** Object clone() : 객체 자신의 복사본을 반환한다.<br>
> public boolean equals() : 객체 자신과 객체 obj가 같은 객체인지 알려준다. (같으면 true)<br>
> **protected** void finalize() : 객체가 소멸될 때 가비지 컬렉터에 의해 자동적으로 호출된다.(거의 사용 X)<br>
> public Class getClass() : 객체 잔신의 클래스 정보를 담고 있는 Class인스턴스를 반환한다.<br>
> public int hashCode() : 객체 자신의 해시코드를 반환한다.<br>
> public String toString() : 객체 자신의 정보를 문자열로 반환한다.<br>
> public void notify() : 객체 자신을 사용하려고 기다리는 쓰레드를 하나만 깨운다.<br>
> public void notifyAll() : 객체 자신을 사용하려고 기다리는 모든 쓰레드를 깨운다.<br>
> public void wait(long timeout) : 다른 쓰레드가 notify()나 notifyAll()을 호출할 때까지 현재 쓰레드를 무한히 또는 지정된 시간(timeout)동안 기다리게 한다. (timeout은 천 분의 1초)

<br>

### equals(Object obj)
- 두 객체의 참조변수의 주소값으로 객체의 같고 다름을 판단한다.
- 객체의 주소값이 아닌 객체가 가진 멤버변수로 비교를 하기 위해서는 equals()메서드를 오버라이딩해서 사용하면 된다. 

<br>

### hashCode()
- 해싱(hashing)기법에 사용되는 '해시함수(hash function)'를 구현한 것
- 해시함수는 찾고자하는 값을 입력하면, 그 값이 저장된 위치를 알려주는 해시코드(hash code)를 반환한다.
- String클래스는 문자열의 내용이 같으면, 동일한 해시코드를 반환하도록 hashCode()가 오버라이딩 되어 있다.

<br>

### toString()
- 이 메서드는 인스턴스에 대한 정보를 문자열(String)로 제공할 목적으로 정의한 것이다.
- Object 클래스에 정의된 toString()
```java
public String toString() {
    return getClass().getName()+"@"+Integer.toHexString(hashCode());
}
```
- 클래스를 작성할 때 toString()을 오버라이딩 하지 않는다면, Object 클래스의 작성된 toString()가 호출돼 클래스 이름에 16진수의 해시코드를 얻는다.
- String 클래스의 toString()은 String 인스턴스가 갖고 있는 문자열을 반환하도록 오버라이딩 되어 있다.
- Date 클래스의 toString()은 갖고 있는 날짜와 시간을 문자열로 반환하도록 오버라이딩 되어 있다.

<br>

### clone()
- 자신을 복제하여 새로운 인스턴스를 생성하는 메서드
- Object 클래스에 정의된 clone()은 단순히 인스턴스의 값만 복사하기 때문에 <br> 참조타입의 인스터스 변수가 있는 클래스는 완전한 인스턴스의 복제가 이루어지지 않는다. <br>
이 때 clone()를 오버라이딩 해서 사용하면 된다.
- clone()은 반드시 예외처리를 해야한다.

<br>

### 공변 반환타입
- 조상 메서드의 반환타입을 자손 클래스의 타입으로 변경을 허용하는 것(JDK 1.5부터 추가)
- 공변 반환타입을 사용하면, 조상의 타입이 아닌, 실제로 반환되는 자손 객체의 타입으로 반환할 수 있어서 번거로운 형변환이 줄어든다.
```java
Point copy = (Point)original.clone() -> Point copy = original.clone()
```

<br>

### 얕은 복사와 깊은 복사
- 얕은 복사
  - clone()은 단순히 객체에 저장된 값을 그대로 복제할 뿐, 객체가 참조하고 있는 객체까지 복제하지는 않는다.
  - 원본과 복제본이 같은 객체를 공유한다.
  - 이런 복제(복사)를 얕은 복사(shallow copy)라고 한다.
  - 얕은 복사에서는 원본을 변경하면 복사복도 영향을 받는다.
- 깊은 복사
  - 원본이 참조하고 있는 객체까지 복사하는 것은 깊은 복사(deep copy)라고 한다.
  - 깊은 복사에서는 원본과 복사본이 서로 다른 객체를 참조하기 때문에 원본의 변경이 복사본에 영향을 주지 않는다.

<br>

### getClass()
- 자신이 속한 클래스의 Class객체를 반환하는 메서드
```java
public final class Class implements ... {   // Class클래스
    ...
}
```
- Class객체는 클래스이 모든 정보를 담고 있으며, 클래스 당 1개만 존재하고, 클래스 로더(ClassLoader)에 의해 메모리에 올라갈 때, 자동으로 생성된다.