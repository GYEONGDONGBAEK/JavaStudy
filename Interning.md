# 문자열 인터닝(String Interning)

---

String에 대해 Github에 정리한 내용이 있었다. 그때는 interning 이라는 용어는 모르고 String이 다시 선언될때 객체가 어떻게 참조되고, 참조되지 않는 객체들은 가비지 콜렉터에 의해 없어진다고 알고 있었다. 그러나 배열을 공부하던중에 궁금한 점이 생겼다.

<aside>
💡 String [] str= {"a","b","c"} 라고 하고 str[0]="d" 로 바꾸고 str[1]="a" 라고 하면 str[0] 이 가리키고 있던 "a"라는 객체는 사라지고 다시 "a"라는 객체가 만들어져서 str[1]이 새로 만들어진 "a"를 참조하는건지 아니면 원래 있던 "a" 참조하는건지

</aside>

이 내용이 궁금해 찾아보니 인터닝이라는 용어와 함께 String.intern 메서드가 정의되어있었다.

---

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/797f2070-d47e-4583-b0fc-61bfad595be2">

### **interning**(인터닝)

```arduino
String str1 = new String("cat");
String str2 = "ball";

//main
System.out.println(str1 == str1.intern());//false
System.out.println(str2 == str1.intern());//true
```

- `intern()`**메소드를 사용하면 Heap영역에 있는 인스턴스를 String Constant pool영역으로 이동한다.**
- 위 결과를 다시한번 살펴보면,
- `System.out.println(str1 == str1.intern());`는 `false`가 나타난다.
    - 이유는 `str1`은 이제 Heap영역이 아닌 String Constatn pool 영역에 있으므로 같은 인스턴스를 참조하지 않는다.
- `System.out.println(str2 == str1.intern());`는 `true`가 나타난다.
    - 위에서 본 바와 같이 `str1.intern()`으로 인해 `str1`은 String Constatn pool로 이동하였으므로 `str2`과 `str1`은 같은 인스턴스를 참조하는 것이다.
- **String 리터럴("")을 이용하여 String 객체를 생성하면 내부에서 intern(); 메소드를 호출한다.**
- **인터닝을 사용하면 문자열 비교 시** `equals()`보다 **속도적인 부분이나 메모리 부분에서 효과**를 얻을 수 있다.