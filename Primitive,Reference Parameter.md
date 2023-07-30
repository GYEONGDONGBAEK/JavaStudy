# [Java] 기본형 매개변수, 참조형 매개변수

---

### 기본형 매개변수

- 기본형 값 복사
- 변수의 값을 읽기만 가능

### 참조형 매개변수

- 인스턴스의 주소 복사
- 변수의 값을 읽고 변경 가능

---

## 기본형 매개변수

기본형 매개변수는 값만 가져오기 때문에 같은 참조변수라도 매개변수의 값에 따라 다른 값이 저장된다.

```java
class Data {
    int x;
}

class PrimitiveParamEx {
    public static void main(String[] args) {

        Data d = new Data();
        d.x = 10;
        System.out.println("main() : x = " + d.x);

        change(d.x);
        System.out.println("After change(d.x)");
        System.out.println("main() : x = " + d.x);

    }

    static void change(int x) {//기본형 매개변수
        x = 1000;
        System.out.println("change() : x = " + x);
    }
}
------------------------------
main() : x= 10
change() : x= 1000
After change(d.x)
main() : x=10
```

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/d821e360-b578-4557-8a9b-ad6fafbaa16a">

1. change 메서드가 호출되면서 d.x 의 값을 change 메서드의 매개변수인 x에 복사
2. change 메서드에서 x의 값을 1000으로 변경
3. change 메서드가 종료되면서 매개변수 x는 스택에서 제거

---

### 참조형 매개변수

기본형 매개변수와는 다르게 참조형은 주소를 가져오기 때문에 change 메서드의 값이 변경될 때 같이 변경된다.

```java
class Data {
    int x;
}

class ReferenceParamEx {
    public static void main(String[] args) {

        Data d = new Data();
        d.x = 10;
        System.out.println("main() : x = " + d.x);

        change(d);
        System.out.println("After change(d)");
        System.out.println("main() : x = " + d.x);

    }

    static void change(Data d) {
        d.x = 1000;
        System.out.println("change() : x = " + d.x);
    }
}
---------------------------------
main() : x = 10
change() : x = 1000
After change(d)
main() : x = 1000
```

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/5402cef8-3337-43a5-9ac7-5f78f166b10f">

1. change 메서드가 호출되면서 참조변수 d 의 주소가 매개변수 d에 복사 된다. 매개변수 d에 저장된 주소값으로 x에 접근 가능하다.
2. change메서드에서 x의 값을 1000으로 변경
3. change 메서드가 종료되면서 매개변수 d는 스택에서 제거