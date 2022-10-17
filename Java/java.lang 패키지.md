# java.lang 패키지
### java.lang 패키지의 클래스들은 import문 없이도 사용할 수 있다.

## Object 클래스
- Object 클래스는 모든 클래스의 최고 조상
- Object 클래스의 멤버들은 모든 클래스에서 바로 사용 가능
- Object 클래스는 멤버변수는 없고 오직 11개의 메서드만 가지고 있다.
> **protected** Object clone() : 객체 자신의 복사본을 반환한다.<br>
> public boolean equals(Object obj) : 객체 자신과 객체 obj가 같은 객체인지 알려준다. (같으면 true)<br>
> **protected** void finalize() : 객체가 소멸될 때 가비지 컬렉터에 의해 자동적으로 호출된다.(거의 사용 X)<br>
> public Class getClass() : 객체 자신의 클래스 정보를 담고 있는 Class인스턴스를 반환한다.<br>
> public int hashCode() : 객체 자신의 해시코드를 반환한다.<br>
> public String toString() : 객체 자신의 정보를 문자열로 반환한다.<br>
> public void notify() : 객체 자신을 사용하려고 기다리는 쓰레드를 하나만 깨운다.<br>
> public void notifyAll() : 객체 자신을 사용하려고 기다리는 모든 쓰레드를 깨운다.<br>
> public void wait(long timeout) : 다른 쓰레드가 notify()나 notifyAll()을 호출할 때까지 현재 쓰레드를 무한히 또는 지정된 시간(timeout)동안 기다리게 한다. (timeout은 천 분의 1초)

### equals(Object obj)
- 두 객체의 참조변수의 주소값으로 객체의 같고 다름을 판단한다.
- 객체의 주소값이 아닌 객체가 가진 멤버변수로 비교를 하기 위해서는 equals()메서드를 오버라이딩해서 사용하면 된다. 

### hashCode()
- 해싱(hashing)기법에 사용되는 '해시함수(hash function)'를 구현한 것
- 해시함수는 찾고자하는 값을 입력하면, 그 값이 저장된 위치를 알려주는 해시코드(hash code)를 반환한다.
- String클래스는 문자열의 내용이 같으면, 동일한 해시코드를 반환하도록 hashCode()가 오버라이딩 되어 있다.

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

### clone()
- 자신을 복제하여 새로운 인스턴스를 생성하는 메서드
- Object 클래스에 정의된 clone()은 단순히 인스턴스의 값만 복사하기 때문에 <br> 참조타입의 인스터스 변수가 있는 클래스는 완전한 인스턴스의 복제가 이루어지지 않는다. <br>
이 때 clone()를 오버라이딩 해서 사용하면 된다.
- clone()은 반드시 예외처리를 해야한다.

### 공변 반환타입
- 조상 메서드의 반환타입을 자손 클래스의 타입으로 변경을 허용하는 것(JDK 1.5부터 추가)
- 공변 반환타입을 사용하면, 조상의 타입이 아닌, 실제로 반환되는 자손 객체의 타입으로 반환할 수 있어서 번거로운 형변환이 줄어든다.
```java
Point copy = (Point)original.clone() -> Point copy = original.clone()
```

### 얕은 복사와 깊은 복사
- 얕은 복사
  - clone()은 단순히 객체에 저장된 값을 그대로 복제할 뿐, 객체가 참조하고 있는 객체까지 복제하지는 않는다.
  - 원본과 복제본이 같은 객체를 공유한다.
  - 이런 복제(복사)를 얕은 복사(shallow copy)라고 한다.
  - 얕은 복사에서는 원본을 변경하면 복사복도 영향을 받는다.
- 깊은 복사
  - 원본이 참조하고 있는 객체까지 복사하는 것은 깊은 복사(deep copy)라고 한다.
  - 깊은 복사에서는 원본과 복사본이 서로 다른 객체를 참조하기 때문에 원본의 변경이 복사본에 영향을 주지 않는다.

### getClass()
- 자신이 속한 클래스의 Class객체를 반환하는 메서드
```java
public final class Class implements ... {   // Class클래스
    ...
}
```
- Class객체는 클래스이 모든 정보를 담고 있으며, 클래스 당 1개만 존재하고, 클래스 로더(ClassLoader)에 의해 메모리에 올라갈 때, 자동으로 생성된다.

## String 클래스
#### 변경 불가능한(immutable) 클래스
- String 클래스에는 문자열을 저장하기 위해 문자형 배열 참조변수(char[]) value를 인스턴스 변수로 정의되어 있다.
```java
public final class String implements java.io.Serializable, Comparable {
    private char[] value;
    ...
}
```
- 인스턴스 생성 시 생성자의 매개변수로 입력받는 문자열은 인스턴스변수(value)에 문자형 배열(char[])로 저장되는 것이다.
- String 클래스는 앞에 final이 붙어 있으므로 다른 클래스의 조상이 될 수 없다.
- 한 번 생성된 String 인스턴스가 갖고 있는 문자열은 읽어 올 수만 있고, 변경은 불가능 하다.
  - 예를 들어 +연산자를 이용해서 문자열을 결합하는 경우 인스턴스 내의 문자열이 바뀌는 것이 아니라 새로운 문자열이 담긴 String 인스턴스가 생성되는 것이다.

#### 문자열 비교
문자열을 만드는 두 가지 방법, **문자열 리터럴을 지정하는 방법**과 **String 클래스의 생성자를 사용**해서 만드는 방법이 있다.
- String 클래스의 생성자를 이용하는 경우 new 연산자에 의해서 메모리할당이 이루어지기 때문에 항상 새로운 String 인스턴스가 생성된다.
- 하지만 문자열 리터럴은 이미 존재하는 것을 재사용하는 것이다.

#### 기본형 값을 String으로 변환
- 기본형 값을 String으로 변환하는 방법에는 `빈 문자열을 더하는 방법`과 `valueOf()`를 사용하는 방법이 있다.
```java
int i = 100;
String str1 = i + "";               // 100을 "100"으로 변환하는 방법 1
String str2 = String.valueOf(i);    // 100을 "100"으로 변환하는 방법 2
```

#### String을 기본형 값으로 변환
- String을 기본형으로 변환하는 방법에는 `valueOf()`를 사용하거나 `parseXxx()`를 사용하면 된다.
```java
String str = "100";
int i = Integer.valueOf(str);       // "100"을 100으로 변환하는 방법 1
int i2 = Integer.parseInt(str);     // "100"을 100으로 변환하는 방법 2
```

## StringBuffer 클래스와 StringBuilder 클래스
### StringBuffer 클래스
- String 클래스는 인스턴스를 생성할 때 지정된 문자열을 변경할 수 없지만 StringBuffer 클래스는 변경이 가능하다.
- StringBuffer 클래스는 String 클래스와 같이 문자열을 저장하기 위한 char형 배열의 참조변수를 인스턴스 변수로 선언해 놓고 있다.
```java
public final class StringBuffer implements java.io.Serializable {
  private char[] value;
  ...
}
```
#### StringBuffer의 생성자
- StringBuffer 인스턴스를 생성할 때는 StringBuffer(int length)를 사용해서 StringBuffer 인스턴스에 저장될 문자열의 길이를 고려하여 여유있는 크기로 지정하는 것이 좋다.
- 버퍼의 크기를 지정해주지 않으면 16개의 문자를 저장할 수 있는 크기의 버퍼를 생성한다.
```java
public StringBuffer (int length) {
  value = new char[length];
  shared = false;
}

public StringBuffer() {
  this(16);	                        // 버퍼의 크기를 지정하지 않을 때, 버퍼의 크기는 16이 된다.
}

public StringBuffer(String str) {
  this(str.length() + 16);              // 지정한 문자열의 길이보다 16이 더 크게 버퍼를 생성한다.
  append(str);
}
```

#### StringBuffer의 비교
- StringBuffer 클래스는 equals 메서드를 오버라이딩하지 않아서 StringBuffer 클래스의 equals 메서드를 사용해도 등가비교연산자(==)로 비교한 것과 같은 결과를 얻는다.
```java
StringBuffer sb = new StringBuffer("123");
StringBuffer sb2 = new StringBuffer("123");

System.out.println(sb == sb2);          // false
System.out.println(sb.equals(sb2));     // false
```
- 반면에 toString()은 오버라이딩되어 있어서 StringBuffer 인스턴스에 toString()을 호출하면, 담고있는 문자열을 String으로 반환한다.
- 그래서 StringBuffer 인스턴스에 담긴 문자열을 비교하기 위해서는 StringBuffer 인스턴스에 toString()을 호출해서 String 인스턴스를 얻은 다음, equals() 메서드를 사용해서 비교해야한다.

### StringBuilder 클래스
- StringBuffer는 멀티쓰레드에 안전(thread safe)하도록 동기화되어 있다.
- 멀티 쓰레드로 작성된 프로그램이 아닌경우, StringBuffer의 동기화는 불필요하게 성능을 감소시킨다.
- 그래서 StringBuffer에서 **쓰레드의 동기화만 빼고** 완전히 똑같은 기능으로 작동하는 **StringBuilder 클래스**가 추가되었다.

### 래퍼(wrapper) 클래스

- 기본형 변수를 객체로 다뤄야할 때 사용하는 클래스
- 8개의 기본형을 대표하는 8개의 래퍼클래스가 있다.
- 래퍼클래스는 모두 equals() 가 오버라이딩 되어 있어 주소값이 아닌 객체가 가지고 있는 값을 비교한다.
- 또, toString() 도 오버라이딩 되어 있어 객체가 가지고 있는 값을 문자열로 변환하여 반환한다.

| 기본형  |  래퍼클래스   | 생성자                                                       | 활용예                                                       |
| :-----: | :-----------: | :----------------------------------------------------------- | :----------------------------------------------------------- |
| boolean |    Boolean    | Boolean (boolean value)<br />Boolean (String s)              | Boolean b = new Boolean (true);<br />Boolean b2 = new Boolean ("abc"); |
|  char   | **Character** | Character (char value)                                       | Character c = new Character ('a');                           |
|  byte   |     Byte      | Byte (byte value)<br />Byte (String s)                       | Byte b = new Byte (20);<br />Byte b2 = new Byte ("20");      |
|  short  |     Short     | Short (short value)<br />Short (String s)                    | Short s = new Short (10);<br />Short s2 = new Short ("10");  |
|   int   |  **Integer**  | Integer (int value)<br />Integer (String s)                  | Integer i = new Integer (100);<br />Integer i2 = new Integer ("100"); |
|  long   |     Long      | Long (long value)<br />Long (String s)                       | Long l = new Long (100);<br />Long l2 = new Long ("100");    |
|  float  |     Float     | Float (double value)<br />Float (float value)<br />Float (String s) | Float f = new Float (1.0);<br />Float f2 = new Float (1.0f);<br />Float f3 = new Float ("1.0f"); |
| double  |    Double     | Double (double value)<br />Double (String s)                 | Double d = new Double (1.0);<br />Double d2 = new Double ("1.0"); |

#### 오토박싱 & 언박싱(autoboxing & unboxing)

- 기본형 값을 래퍼 클래스의 객체로 자동 변환해주는 것을 '오토박싱(autoboxing)'이라고 하고, 반대로 변환하는 것을 '언박싱(unboxing)' 이라고 한다.

### 📝참고 문헌

- Java의 정석 3판 (도우출판, 남궁 성 지음)
