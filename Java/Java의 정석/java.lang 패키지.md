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
- 