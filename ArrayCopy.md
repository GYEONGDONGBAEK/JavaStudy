# JAVA 배열 복사

---

### 얕은 복사

- 실제로는 하나의 주소 값을 가지고 있으므로 하나라고 볼 수 있다.
- 복사된 배열이나 원본 배열이 변경될 때 서로 간의 값이 같이 변경된다.

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/fc2308bd-04c5-4358-b51f-993db11ba4c2">

```java
public class Array_Copy{
    public static void main(String[] args)  {
        int[] a = { 1, 2, 3, 4 };
        int[] b = a;
    }
}
```

### 깊은 복사

- 객체의 실제 값을 새로운 객체로 복사하는 것이다.
- 복사된 배열이나 원본 배열이 변경될 때 서로 간의 값은 바뀌지 않는다.

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/4eef6425-4195-4078-9a52-1a3166e006ee">

```java
public class Array_Copy{
    public static void main(String[] args)  {
        int[] a = { 1, 2, 3, 4 };
        int[] b = new int[a.length]; 
        for (int i = 0; i < a.length; i++) {
            b[i] = a[i];
        }
    }
}
```

---

# ****배열을 복사하는 여러가지 메서드****

### ****Object.clone()****

```java
public class Array_Copy{
    public static void main(String[] args)  {
        int[] a = { 1, 2, 3, 4 };
        int[] b = a.clone();
    }
}
```

Array.clone()을 사용하면 배열을 쉽게 복사할 수 있습니다. 깊은 복사의 가장 보편적인 방법이다.

### ****System.arraycopy()****

```java
public class Array_Copy{
    public static void main(String[] args)  {
        int[] a = { 1, 2, 3, 4 };
        int[] b = new int[a.length];
        System.arraycopy(a, 0, b, 0, a.length);
    }
}
```

System.arraycopy() 메서드는 주어진 시작 위치에서 특정 길이만큼의 배열 요소를 복사하여 대상 배열에 붙여 넣는다.

### ****Arrays.copyOf()****

```java
import java.util.Arrays;

public class Array_Copy{
    public static void main(String[] args)  {
        int[] a = { 1, 2, 3, 4 };
        int[] b = Arrays.copyOf(a, a.length);
    }
}
```

Arrays클래스는 배열을 조작할 수 있는 메소드를 가진 클래스다. 지정된 배열을 복사하며, 필요에 따라 0으로 채워서 복사본이 지정된 길이를 가지게 한다. 즉, 원본 배열과 복사본 배열에서 모두 유효한 인덱스라면 동일한 값을 가지지만, 원본에서는 유효하지 않지만 복사본에서 유효한 인덱스에 대해서는 복사본은 ‘0’ 의 값을 가진다.

### Arrays.copyOfRange

```java
import java.util.Arrays;

public class Array_Copy{
    public static void main(String[] args)  {
        int[] a = { 1, 2, 3, 4 };
        int[] b = Arrays.copyOfRange(a, 1, 3);
    }
}
```

Arrays.copyOf()는 배열의 처음~지정한 length까지 복사하는 메서드였다면 Arrays.copyOfRange() 메서드는 복사할 배열의 시작점도 지정할 수 있다. 즉, 지정된 배열의 지정된 범위를 새 배열에 복사한다. 범위의 초기 인덱스는 반드시 0과 원본배열.length 사이에 존재해야 한다.

## 복사 메서드의 속도 비교

```java
public class CopyTimeTest {
		//데이터 10건일때 속도
		System.arraycopy 시간: 2200 ns
		Arrays.copyOf 시간: 22100 ns
		Arrays.copyOfRange 시간: 2800 ns
		Object.clone 시간: 4000 ns
		//데이터가 10000건일때 속도
		System.arraycopy 시간: 22700 ns
		Arrays.copyOf 시간: 50300 ns
		Arrays.copyOfRange 시간: 49800 ns
		Object.clone 시간: 30200 ns
		//데이터가 1000000건일때 속도
		System.arraycopy 시간: 2126500 ns
		Arrays.copyOf 시간: 2373300 ns
		Arrays.copyOfRange 시간: 2216400 ns
		Object.clone 시간: 2318000 ns
}
```

---

# ****2차원 배열의 복사****

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/fd7ac3fc-e793-49c0-a4c9-ac8a10e2d120">

간단히 말하자면, 2차원 배열은 1차원 배열의 배열로 이루어져 있다. 즉 행 또는 열로 표현 할 수 있는 각 차원이 실제로는 별도의 1차원 배열을 참조하고 있는것이다. 그래서 a[x][y] 에서 a[x]는 1차원 배열을 가리키는 참조이며, a[x][y] 는 그 1차원 배열의 특정 요소를 가리키는 참조이다.

일반적인 복사 메서드를 사용한다면 a[x]가 가리키는 1차원 배열의 참조만 복사되고, 그 1차원 배열 안의 실제 값들은 복사 되지 않는다. 즉 **‘얉은 복사’** 가 일어난다. 복사된 배열에서 a[x][y]를 변경한다면 원본 배열에도 영향을 끼치게 된다.

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/f1438ea9-f206-4a5e-81fe-00807d8fbb5a">

그렇기에 2차원 배열을 복사하기 위해선 2중 반복문, 반복문 + 복사메서드를 사용할 수 있다.

### 2중 반복문 활용

```java
public static void main(String[] args)  {
        int a[][] = {{1,2,3},{4,5,6,},{7,8,9}};
        int[][] b = new int[a.length][a[0].length];
	    
        for(int i=0; i<a.length; i++) {
            for(int j=0; j<a[i].length; j++) {
                b[i][j] = a[i][j];  
            }
        }
    }
```

### 반복문 + 복사 메서드

```java
public static void main(String[] args) {
	        int[][] original = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
	        int[][] copy1 = copyWithSystemArraycopy(original);
	        int[][] copy2 = copyWithArraysCopyOf(original);
	        int[][] copy3 = copyWithArraysCopyOfRange(original);

	        copy1[0][0] = 10;  
	        copy2[1][1] = 20;  
	        copy3[2][2] = 30;  

	        System.out.println("원본 배열: ");
	        printArray(original);

	        System.out.println("System.arraycopy 복사: ");
	        printArray(copy1);

	        System.out.println("Arrays.copyOf 복사: ");
	        printArray(copy2);

	        System.out.println("Arrays.copyOfRange 복사: ");
	        printArray(copy3);
	    }

	    public static int[][] copyWithSystemArraycopy(int[][] original) {
	        int[][] copy = new int[original.length][];
	        for (int i = 0; i < original.length; i++) {
	            copy[i] = new int[original[i].length];
	            System.arraycopy(original[i], 0, copy[i], 0, original[i].length);
	        }
	        return copy;
	    }

	    public static int[][] copyWithArraysCopyOf(int[][] original) {
	        int[][] copy = new int[original.length][];
	        for (int i = 0; i < original.length; i++) {
	            copy[i] = Arrays.copyOf(original[i], original[i].length);
	        }
	        return copy;
	    }

	    public static int[][] copyWithArraysCopyOfRange(int[][] original) {
	        int[][] copy = new int[original.length][];
	        for (int i = 0; i < original.length; i++) {
	            copy[i] = Arrays.copyOfRange(original[i], 0, original[i].length);
	        }
	        return copy;
	    }

	    public static void printArray(int[][] array) {
	        for (int[] row : array) {
	            for (int num : row) {
	                System.out.print(num + " ");
	            }
	            System.out.println();
	        }
	    }
```

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/1a4114b3-e220-424d-bab6-809b9dd618fa">