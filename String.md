# 자바 String에 대해

---

Java에서 String은 특별한 참조 자료형이다. String 객체는 자바에 내장된 클래스로 위와 같이 new 키워드로 새로운 객체를 생성할 수도 있고, " "안에 값을 입력하여 생성할 수도 있다.

자바의 문자열은 java.lang 패키지의 String클래스의 인스턴스로 관리된다. 소스상에서 문자열 리터럴은 String 객체로 자동 생성되지만, String 클래스의 다양한 생성자를 이용해서 직접 String 객체를 생성해서 사용 할 수도 있다.

아래의 코드에서 몇개의 객체가 생성이 될까?

<aside>
💡

```
public class StringExample {
  public static void main(String [] args) {
    String s1="cat";
    String s2="cat";
		String s3=new String("cat");
  }
}
```

</aside>

두 가지 방식 모두 String 객체를 생성한다는 사실은 같지만, JVM이 관리하는 메모리 구조상에서 명백히 다르다. 아래의 그림은 두가지 방법으로 String 객체를 생성했을 때, JVM 메모리상에 어떻게 존재하는지에 대한 그림이다.

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/f6e5a062-56bc-4004-a8f8-73c41354e7f3">

자바의 String은 특별한 '참조 자료형'이다. new 생성자를 이용해서 인스턴스를 생성한 뒤, heap에서 메모리 관리가 이루어 진다는 사실은 다른 참조 자료형과 다를게 없다. 하지만 다른 참조형과는 다르게 변하지 않는다는 불변성(immutable)을 가지고 있다.

만약 위에 그림에서 s4=s1+s2 를 실행한다면 CatCat 값을 가지는 String 객체를 새로 생성하고 s4는 그 생성된 객체를 참조하게 된다.

따라서 위 코드에서 생성되는 String 객체의 갯수는 2개이다.