# 입출력(I/O)-(1)

---

# **스트림 (InputStream / OutputStream)**

- 데이터를 운반하는데 사용되는 연결 통로
- 자바에서 입출력을 수행하기 위해 필요
- 단방향 통신
- 입력/출력을 동시에 수행하려면 입력스트림, 출력스트림, 2개의 스트림 필요
- 바이트단위로 데이터 전송

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/d43219fa-e1f4-42fa-9e38-48a139045572">

## 입출력 스트림

스트림은 한 방향으로만 통신할 수 있으므로, 입력과 출력을 동시에 처리할 수는 없다.

따라서 스트림은 사용 목적에 따라 입력 스트림과 출력 스트림으로 구분된다.

자바에서는 java.io 패키지를 통해 InputStream과 OutputStream 클래스를 별도로 제공하고 있다.

즉, 자바에서의 스트림 생성이란 이러한 스트림 클래스 타입의 인스턴스를 생성한다는 의미다.

InputStream 클래스에는 read() 메소드가, OutputStream 클래스에는 write() 메소드가 각각 추상 메소드로 포함되어 있다.

| 클래스 | 메소드 | 설명 |
| --- | --- | --- |
| InputStream | abstract int read() | 해당 입력 스트림으로부터 다음 바이트를 읽어들임. |
|  | int read(byte[] b) | 해당 입력 스트림으로부터 특정 바이트를 읽어들인 후, 배열 b에 저장함. |
|  | int read(byte[] b, int off, int len) | 해당 입력 스트림으로부터 len 바이트를 읽어들인 후, 배열 b[off]부터 저장함. |
| OutputStream | abstract void write(int b) | 해당 출력 스트림에 특정 바이트를 저장함. |
|  | void write(byte[] b) | 배열 b의 특정 바이트를 배열 b의 길이만큼 해당 출력 스트림에 저장함. |
|  | void write(byte[] b, int off, int len) | 배열 b[off]부터 len 바이트를 해당 출력 스트림에 저장함. |

<aside>
💡 read() 메소드는 해당 입력 스트림에서 더 이상 읽어들일 바이트가 없으면, -1을 반환해야 한다.

그런데 반환 타입을 byte 타입으로 하면, 0부터 255까지의 바이트 정보는 표현할 수 있지만 -1은 표현할 수 없게 된다.

따라서 InputStream의 read() 메소드는 반환 타입을 int형으로 선언하고 있다.

</aside>

사용자는 이 두 메소드를 상황에 맞게 적절히 구현해야만 입출력 스트림을 생성하여 사용할 수 있다.

### 바이트기반 스트림 - InputStream, OutputStream

| 입력스트림 | 출력스트림 | 입출력 대상의 종류 |
| --- | --- | --- |
| FileInputStream | FileOutputStream | 파일 |
| ByteArrayInputStream | ByteArrayOutputStream | 메모리 |
| PipedInputStream | pipedOutputStream | 프로세스간의 통신 |
| AudioInputStream | AudioOutputStream | 오디오장치 |

### **보조스트림**

- 실제 데이터를 주고받는 스트림이 아니라 데이터를 직접 입출력 할 수 없음
- 스트림의 기능을 향상시키거나 새로운 기능을 추가하는 용도
- 기반스트림 생성 -> 기반스트림을 이용해서 보조스트림 생성

```java
FileInputStream fis = new FileInputStream("test.txt");

BufferedInputStream bis = new BufferedInputStream(fis);

bis.read();
```

| 입력 | 출력 | 설명 |
| --- | --- | --- |
| FilterInputStream | FilterOutputStream | 필터를 이용한 입출력 처리 |
| BufferedInputStream | BufferedOutputStream | 버퍼를 이용한 입출력 성능 향상 |
| DataInputStream | DataOutputStream | int, float와 같은 기본형 단위로 데이터를 처리하는 기능 |
| SequenceInputStream | X | 두 개의 스트림을 하나로 연결 |
| LineNumberInputStream | X | 읽어 온 데이터의 라인 번호를 카운트 |
| ObjectInputStream | ObjectOutputStream | 데이터를 객체 단위로 읽고 쓰는데 사용. 주로 파일을 이용하며 객체 직렬화와 관련있음 |
| X | PrintOutputStream | 버퍼를 이용하며, 추가적인 print관련 기능 |
| PushbackInputStream | X | 버퍼를 이용해서 읽어 온 데이터를 다시 되돌리는 기능 |

### 문자 기반 스트림

스트림은 기본적으로 바이트 단위로 데이터를 전송한다.

하지만 자바에서 가장 작은 타입인 char 형이 2바이트이므로, 1바이트씩 전송되는 바이트 기반 스트림으로는 원활한 처리가 힘든 경우가 있다.

따라서 자바에서는 바이트 기반 스트림뿐만 아니라 문자 기반의 스트림도 별도로 제공한다.

이러한 문자 기반 스트림은 기존의 바이트 기반 스트림에서 InputStream을 Reader로, OutputStream을 Writer로 변경하면 사용할 수 있다.

자바에서는 다음과 같은 다양한 문자 기반의 입출력 스트림을 제공하고 있다.

| 입력 스트림 | 출력 스트림 | 입출력 대상 |
| --- | --- | --- |
| FileReader | FileWriter | 파일 |
| CharArrayReader | CharArrayWriter | 메모리 |
| PipedReader | PipedWriter | 프로세스 |
| StringReader | StringWriter | 문자열 |

지금까지 살펴본 바이트 기반의 스트림과 문자 기반의 스트림은 활용 방법이 거의 같다.

따라서 문자 기반의 보조 스트림도 다음과 같이 제공된다.

| 입력 스트림 | 출력 스트림 | 설명 |
| --- | --- | --- |
| FilterReader | FilterWriter | 필터를 이용한 입출력 |
| BufferedReader | BufferedWriter | 버퍼를 이용한 입출력 |
| PushbackReader | X | 다른 입력 스트림에 버퍼를 이용하여 push back이나 unread와 같은 기능을 추가함. |
| X | PrintWriter | 다른 출력 스트림에 버퍼를 이용하여 다양한 데이터를 출력하기 위한 기능을 추가함. |

---

### InputStream과 OutputStream

### InputStream

<aside>
💡 바이트 기반 입력 스트림의 최상위 추상 클래스이다.

- 모든 바이트 기반 입력 스트림은 이 클래스를 상속 받는다.
- 파일 데이터를 읽거나 네트워크 소켓을 통해 데이터를 읽거나 키보드에서 입력한 데이터를 읽을 때 사용한다.
- InputStream은 읽기에 대한 다양한 추상 메소드들을 정의해 두어 사용할 수 있다.
- InputStream의 추상메소드를 오버라이딩하여 목적에 따라 데이터를 입력 받을 수 있다.
</aside>

**주요 메소드**

| 메소드(Method) | 설명 |
| --- | --- |
| int available() | 현재 읽을 수 있는 바이트 수를 반환한다. |
| void close() | 현재 열려있는 InputStream을 닫는다. |
| void mark(int readlimit) | InputStream에서 현재의 위치를 표시해준다. |
| boolean markSupported() | 해당 InputStream에서 mark()로 지정된 지점이 있는지에 대한 여부를 확인한다. |
| abstract int read() | InputStream에서 한 바이트를 읽어서 int값으로 반환한다. |
| int read(byte[] b) | byte[] b만큼의 데이터를 읽어서 b에 저장하고 읽은 바이트 수를 반환한다. |
| int read(byte[]b, int off, int len) | len만큼 읽어서 byte[] b의 off위치에 저장하고 읽은 바이트 수를 반환한다. |
| void reset() | mark()를 마지막으로 호출한 위치로 이동한다. |
| long skip(long n) | InputStream에서 n바이트만큼 데이터를 스킵하고 바이트 수를 반환한다. |

### OutputStream

<aside>
💡 바이트 기반 출력 스트림의 최상위 추상 클래스이다.

- 모든 바이트 기반 출력 스트림은 이 클래스를 상속 받는다.
- OutputStream의 추상메소드를 오버라이딩하여 목적에 따라 데이터를 입력 받을 수 있다.
</aside>

**주요메소드**

| 메소드(Method) | 설명 |
| --- | --- |
| void close() | OutputStream을 닫는다. |
| void flush() | 버퍼에 남아있는 출력 스트림을 출력한다. |
| void write(byte[] b) | 버퍼의 내용을 출력한다. |
| void write(byte[] b, int off, int len) | b배열 안에 있는 시작 off부터 len만큼 출력한다. |
| abstract void write(int b) | 정수 b의 하위 1바이트를 출력한다. |

# **ByteArrayInputStream 과 ByteArrayOutputStream**

**ByteArrayInputStream**과 **ByteArrayOutputStream**는 자바의 입출력 스트림 클래스다. 이들은 메모리 상의 바이트 배열에 데이터를 읽고 쓰는 데 사용된다. 각각 입력 스트림과 출력 스트림의 역할을 담당하며, 데이터를 바이트 단위로 다루는 데 유용하다. 주로 다른 곳에 입출력하기 전에 데이터를 임시로 바이트배열에 담아서 변환하는 등의 작업을 하는데 사용된다.

### **ByteArrayInputStream**

바이트 배열로부터 데이터를 읽어오는 입력 스트림

- 이미 메모리에 올라가 있는 데이터를 읽어오는 경우
- 네트워크나 파일로부터 데이터를 먼저 읽어와 메모리 상에서 처리하는 경우

### 주요 메서드

| int read() | 바이트를 읽어 반환. 읽을 데이터가 없을 경우 -1을 반환 |
| --- | --- |
| int read(byte[] buffer, int offset, int length) | 지정된 바이트 배열 buffer로부터 최대 length 바이트를 읽어온다. 실제로 읽어온 바이트 수를 반환하며, 더 이상 읽을 데이터가 없을 경우 -1을 반환 |
| int available() | 읽을 수 있는 남은 바이트 수를 반환 |

### ByteArrayOutputStream

ByteArrayOutputStream은 바이트 배열에 데이터를 쓰는 출력 스트림

- 데이터를 메모리에 누적해야 하는 경우.
- 처리한 데이터를 파일이나 네트워크로 한 번에 보내야 하는 경우.

### 주요 메서드

| void write(int byte) | 지정된 바이트를 출력 스트림에 씀 |
| --- | --- |
| void write(byte[] buffer, int offset, int length) | 지정된 바이트 배열 buffer의 offset 위치부터 length 바이트를 출력 스트림에 씀 |
| byte[] toByteArray() | 출력 스트림에 쓴 데이터를 바이트 배열로 반환 |
| void reset() | 출력 스트림의 내용을 초기화하여 다시 사용할 수 있도록 한다 |

## FileInputStream과 FileOutputStream

파일에 입출력을 하기 위한 스트림이다. 실제 프로그래밍에서 많이 사용되는 스트림 중 하나다.

### 생성자

| FileInputStream(String name) | 지정된 파일이름을 가진 실제 파일과 연결된 FileInputStream을 생성 |
| --- | --- |
| FileInputStream(File file) | 파일의 이름이 String이 아닌 File 인스턴스로 지정해주어야 하는 점을 제외하고 FileInputStream과 같다. |
| FileInputStream(FileDescriptor fdObj) | 파일 디스크립터(fdObj)로 FileInputStream을 생성 |
| FileOutputStream(String name) | 지정된 파일이름을 가진 실제 파일과 연결된 FileOutputStream을 생성 |
| FileOutputStream(String name, boolean append) | 지정된 파일이름을 가진 실제 파일과 연결된 FileOutputStream을 생성, 두번째 인자인 append를 true로 하면, 출력 시 기존의 파일내용의 마지막에 덧붙인다. false면, 기존의 파일 내용을 덮어쓰게 한다. |
| FileOutputStream(File file) | 파일의 이름이 String이 아닌 File 인스턴스로 지정해주어야 하는 점을 제외하고 FileOutputStream과 같다. |
| FileOutputStream(File file, boolean append) | 파일의 이름이 String이 아닌 File 인스턴스로 지정해주어야 하는 점을 제외하고 FileOutputStream(String name, boolean append)와 같다. |
| FileOutputStream(FileDescriptor fdObj) | 파일 디스크립터(fdObj)로 FileOutputStream을 생성 |

---

# 바이트기반의 보조스트림

FilterInputStream과 FilterOutputStream은 InputStream/OutputStream의 자손이면서, 모든 보조스트림의 조상이다.

자체적으로 입출력을 수행할 수 없기 때문에 기반 스트림이 필요하다.

모든 메서드는 단순히 기반스트림의 메서드를 그대로 호출할 뿐이다.

생성자로 인스턴스를 생성할 수 없으므로 상속을 통해 오버라이딩을 통해 보조기능을 추가할 수 있다.

```java
public class FilterInputStream extends InputStream{
    protected volatile InputStream in;
    // 접근제어자가 proteced이므로 생성자를 사용할 수 없다.
    protected FilterInputStream(InputStream in){ 
        this.in = in;
    }

    public int read() throws IOException{
        return in.read();
    }
    ...
}
```

<aside>
💡 **FilterInputStream의 자손**

- BufferedInputStream, DataInputStream, PushbackInputStream 등

**FilterOutputStream의 자손**

- BufferedOuputStream, DataOutputStream, PushbackOutputStream 등
</aside>

## BufferedInputStream과 BufferedOutputStream

스트림의 입출력의 효율을 높이기 위해 사용하는 보조스트림이다.

한 바이트씩 입출력하는 것 보다는 버퍼(바이트배열)를 이용해서  한 번에 여러 바이트를 입출력하는 것이 빠르기 때문이다. 대부분의 입출력 작업에 사용된다.

### 생성자

| BufferedInputStream(InputStream in, int size) | 주어진 InputStream인스턴스를 입력소스(input source)로 하며 지정된 크기(byte 단위) 의 버퍼를 갖는 BufferedInputStream 인스턴스를 생성한다. |
| --- | --- |
| BufferedInputStream(InputStream in) | 주어진 InputStream인스턴스를 입력소스(input source)로 하며 버퍼의 크기를 지정해주지 않으므로 기본적으로 8192byte 크기의 버퍼를 갖게 된다. |
| BufferedOutputStream(OutputStream out, int size) | 주어진 OutputStream인스턴스를 입력소스(Output source)로 하며 지정된 크기(byte 단위) 의 버퍼를 갖는 BufferedOutputStream 인스턴스를 생성한다. |
| BufferedOutputStream(OutputStream out) | 주어진 OutputStream인스턴스를 입력소스(Output source)로 하며 버퍼의 크기를 지정해주지 않으므로 기본적으로 8192byte 크기의 버퍼를 갖게 된다, |

### 메서드

| flush() | 버퍼의 모든 내용을 출력소스에 출력한 다음, 버퍼를 비운다. |
| --- | --- |
| close() | flush()를 호출해서 버퍼의 모든 내용을 출력소스에 출력하고, BufferedOutputStream 인스턴스가 사용하던 모든 자원을 반환한다. |

## DataInputStream과 DataOutputStream

DataInputStream/DataOutputStream은 FilterInputStream과 FilterOutputStream의 자손이며DataInput인터페이스와 DataOuput인터페이스를 각각 구현하였기 때문에, 데이터를 읽고 쓰는데

있어서 byte가 아닌 8가지 기본 자료형의 단위로 쓸 수 있는 장점이 있다.

기본 자료형의 값은 16진수로 표현하여 저장합니다.

### 생성자

| DataInputStream(InputStream in) | 주어진 InputStream인스턴스를 기반스트림으로 하는 DataInputStream인스턴스를 생성한다. |
| --- | --- |
| DataOutputStream(OutputStream out) | 주어진 OutputStream인스턴스를 기반스트림으로 하는 DataOutputStream인스턴스를 생성한다. |

### 메서드

| 타입 read타입() | 각 타입에 맞게 값을 읽어온다. 더 이상 읽을 값이 없으면 EOFException을 발생시킨다.  |
| --- | --- |
| void readFully(byte[] b)
void readFully(byte[] b, int off, int len) | 입력스트림에서 지정된 배열의 크기만큼 또는 지정된 위치에서 len만큼 데이터를 읽어온다. 파일의 끝에 도달하면 EOFException이 발생하고, I/O에러가 발생하면 IOException 이 발생한다. |
| String readUTF() | UTF-8형식으로 쓰여진 문자를 읽는다
더 이상 읽을 값 없으면EOFException을 발생시킵니다. |
| static String readUTF(DataInput in) | 입력스트림(in) 에서 UTF-8형식의 유니코드를 읽어온다. |
| int skipByte(int n) | 현재 읽고 있는 위치에서 지정된 숫자(n) 만큼을 건너뛴다. |
| void writeBoolean(boolean b)
void writeByte(int b)
void writeChar(int c)
void writeShort(int s)
void writeInt(int i)
void writeLong(long l)
void writeFloat(float f)
void writeDouble(double b) | 각 자료형에 알맞는 값을 출력한다. |
| void writeUTF(String s) | UTF형식으로 문자를 출력한다. |
| void writeChars(String s) | 주어진 문자열을 출력한다. writeChar(int c) 메서드를 여러번 호출한 결과와 같다. |
| int size() | 지금까지 DataOutputStream에 쓰여진 byte의 수를 알려 준다. |

## ****SequenceInputStream****

여러 개의 입력스트림을 연속적으로 연결해서 하나의 스트림으로부터 데이터를 읽는 것과 같이 처리할 수 있도록 도와준다.

생성자를 제외하고 나머지 작업은 다른 입력스트림과 다르지 않다.

큰 파일을 여러 개의 작은 파일로 나누었다가 하나의 파일로 합치는 것과 같은 작업을 수행할때 사용하면 좋다.

SequenceInputStream은 다른 보조스트림과 달리 FilterInputStream의 자손이 아닌 InputStream을 바로 상속받아서 구현했다.

### 생성자

| SequenceInputStream(Enumeration e) | Enumeration에 저장된 순서대로 입력스트림을 하나의 스트림으로 연결다. |
| --- | --- |
| SequenceInputStream(InputStream s1, InputStream s2) | 두 개의 입력스트림을 하나로 연결한다. |

## **PrintStream**

PrintStream은 데이터를 기반스트림에 다양한 형태로 출력할 수 있는 print, println, printf와 같은

메서드를 오버라이딩하여 제공한다.

데이터를 적절한 문자로 츨력하는 것이기 때문에 문자기반 스트림 역할을 수행한다. PrintStream보다 향상된 기능의 문자기반 스트림인 PrintWrite가 있으나 System.out이 PrintStream이다 보니 둘다 사용할 수 밖에 없다. PrintStream과 PrintWrite가 거의 같은 기능을 가지고 있지만, PrintWriter가 PrintStream에 비해 다양한 언어의 문자를 처리하는데 적합하기 때문에 가능하면 PrintWriter를 사용하는 것이 좋다.

### 생성자/ 메서드

| PrintStream(File file)
PrintStream(File file, String csn)
PrintStream(OutputStream out)
PrintStream(OutputStream out, boolean autoFlush)
PrintStream(OutputStream out, boolean autoFlush, String encoding)
PrintStream(String fileName)
PrintStream(String fileName, String csn) | 지정된 출력스트림을 기반으로 하는 PrintStream 인스턴스를 생성한다. autoFlush의 값을 true로 하면 println메서드가 호출되거나 개행문자가 출력될 때 자동으로 flush된. 기본값은 false다. |
| --- | --- |
| boolean checkError() | 스트림을 flush하고 에러가 발생했는지 알려준다. |
| void print(타입 타입변수)
void println(타입 타입변수) | 인자로 주어진 값을 출력소스에 문자로 출력한다. println메서드는 출력 후 줄바꿈을 하고, print메서드는 줄을 바꾸지 않는다. |
| void println() | 줄바꿈 문자를 출력함으로써 줄을 바꾼다. |
| PrintStream printf(String format, Object… args) | 정형화된 출력을 가능하게 한다. |
| protected void setError() | 작업 중에 오류가 발생했음을 알린다. |

### printf() 에 사용될 수 있는 옵션

| format | 설명 ( 정수 ) | 결과 ( int i = 65 ) |
| --- | --- | --- |
| %d | 10진수 (decimal Integer) | 65 |
| %o | 8진수 (octal Integer) | 101 |
| %x | 16진수 (hexadecimal Integer) | 41 |
| %c | 문자 | A |
| %s | 문자열 | 65 |
| %5d | 5자리의 숫자, 빈자리는 공백으로 채움 | 65 |
| %-5d | 5자리의 숫자. 빈숫자는 공백으로 채웁니다.(왼쪽 정렬) | 65 |
| %05d | 5자리의 숫자. 빈자리는 0으로 채웁니다. | 00065 |

| format | 설명 ( 문자열 ) | 결과 ( String str = "ABC" ) |
| --- | --- | --- |
| %s | 문자열(string) | ABC |
| %5s | 5자리 문자열, 빈자리는 공백으로 채운다. | ABC |
| %-5s | 5자리의 문자열 빈자리는 공백으로 채운다(왼쪽) | ABC |

| format | 설명 ( 실수 ) | 결과 ( float f= 1234.56789 ) |
| --- | --- | --- |
| %e | 지수형태로 표현(exponent) | 1.234568e+03 |
| %f | 10진수(decimal float) | 1234.56789 |
| %3.1f | 소수점이상 최소6자리 최소 3자리, 소수점 이하 1자리(  두번째는 반올림 ) | 1234.6 |
| %8.1f | 소수점이상 최소 6자리, 소수점 이하 1자리출력될 자리수를 최소 8자리를 확보 빈자리는공백으로 채워짐집니다. | 1234.6 |
| %08.1f | 소수점이상 최소 6자리, 소수점 이하 1자리출력될 자리수를 최소 8자리를 확보 빈자리는 0으로 채워짐집니다. | 001234.6 |
| %-8.1f | 소수점이상 최소 6자리, 소수점 이하 1자리출력될 자리수를 최소 8자리(소수점포함)를 확보합니다.빈자리는 공백으로 채원집니다.(왼쪽정렬) | 1234.6 |

| format | 설명  ( 특수문자 ) |
| --- | --- |
| \t | 탭(tab) |
| \n | 줄바꿈 문자(new line) |
| %% | % |

| format | 설명 ( 날짜와 시간 ) | 결과 |
| --- | --- | --- |
| %t%tH:%tM | 시분(24시간) | 21:0521:05 |
| %tT%tH:%tm:%tS | 시분초(24시간) | 21:05:3321:05:33 |
| %tD%tm/%td/%ty | 연월일 | 08/04/1708/04/17 |
| %tF%tY-%tm-%td | 연월일 | 2017-08-042017-08-04 |

---

# 문자기반 스트림

## **Reader와 Writer**

Reader/Write는 모든 문자기반의 스트림의 조상역할을 한다.

byte배열 대신 char 배열을 사용한 다는 것 이외에는 InputStream/OutputStream의 메서드와

똑같다.

Reader/Writer 그리고 자손들은 여러 종류의 인코딩과 자바에서 사용하는 유니코드간의 변환을 자동적으로 처리해준다.  Reader는 특정 인코딩을 읽어서 유니코드로 변환하고 Writer는 유니코드를 특정인코딩으로 변환하여 저장한다.

### 메서드

| abstract void close() | 입력스트림을 닫음으로써 사용하고 있던 자원을 반환한다. |
| --- | --- |
| void mark(int readlimit) | 현재위치를 표시해놓는다. 후에 reset()에 의해서 표시해 놓은 위치로 다시 되돌아 갈수 있다. |
| boolean markSupported() | mark()와 reset()을 지원하는지 알려준다. |
| int read() | 입력소스로부터 하나의 문자를 읽어온다 char의 범위 0~65335범위의 정수를 반환하며, 입력스트림의 마지막 데이터에 도달하면, -1 반환한다. |
| int read(char[] c) | 입력소스로부터 매개변수로 주어진 배열 c의 크기만큼 읽어서 배열 c에 저장한다. 읽어 온 데이터의 개수 또는 -1을 반환한다. |
| abstract int read(char[] c, int off, int len) | 입력소스로부터 최대 len개의 문자를 읽어서, 배열 c의 지정된 위치(off)부터 읽는 만큼 저장한다. 읽어 온 데이터의 개수 또는 -1을 반환한다. |
| boolean ready() | 입력소스로부터 데이터를 읽을 준비가 되어있는지 알려준다. |
| void reset() | 입력소스에서의 위치를 마지막으로 mark()가 호출되었던 위치로 되돌린다. |
| long skip(long n) | 현재 위치에서 주어진 문자 수(n)만큼을 건너뛴다. |
| Writer append(char c) | 지정된 문자를 출력소스에 출력한다. |
| Writer append(charsequence c) | 지정된 문자열(charSequence)을 출력소스에 출력한다. |
| Writer append(charsequence c, int start, int end) | 지정된 문자열의 일부를 출력소스에 출력한다. |
| abstract void close() | 출력스트림을 닫음으로써 사용하고 있던 자원을 반환한다. |
| abstract void flush() | 스트림의 버퍼에 있는 모든 내용을 출력소스에 쓴. ( 버퍼가 있는 스트림에만 해당됨 ) |
| void write(int b) | 주어진 값을 출력소스에 쓴다. |
| void write(char[] c) | 주어진 배열 c에 저장된 모든 내용을 출력소스에 다. |
| abstract void write(char[] c, int off, int len) | 주어진 배열 c에 저장된 내용 중에서 off번째부터 len길이 만큼만 출력소스에 쓴다. |
| void write(String str) | 주어진 문자열(str)을 출력소스에 쓴다. |
| void write(String str, int off, int len) | 주어진 문자열(str)의 일부를 출력소스에 쓴다. ( off번째 문자부터 len개 만큼의 문자열 ) |

## FileReader와 FileWriter

파일로부터 텍스트데이터를 읽고, 파일을 쓰는데 사용된다. 사용방법은 FileInputStream/FileOutputStream과 다르지 않다.

## PipedReader와 PipedWriter

PipedReader/PipedWriter는 쓰레드 간에 데이터를 주고받을 때 사용된다.

다른 스트림과는 달리 입력과 출력스트림을 하나의 스트림으로 연결해서 데이터를 주고 받는

특징이 있다.

입출력을 마친 후 한쪽 스트림만 닫아도 나머지 스트림은 자동으로 닫다.

## StringReader와 StringWriter

StringReader/StringWriter는 CharArrayReader/CharArrayWriter와 같이 입출력 대상이 메모리인 스트림이다.

StringWriter에 출력되는 데이터는 내부의 StringBuffer에 저장된다.

<aside>
💡 StringBuffer getBuffer() : StringWriter에 출력한 데이터가 저장된 StringBuffer를 반환합니다.

String toString() : StringWriter에 출력된 문자열을 반환합니다

</aside>

## **BufferedReader와 BufferedWriter**

BufferedReader/BufferedWriter는 버퍼를 이용해서 입출력의 효율을 높일 수 있도록 해주는 역할을

한다. 버퍼를 이용하면 입출력의 효율이 비교할 수 없을 정도로 좋아지기 때문에 사용하는 것이

좋다.

BufferedReader의 readLine()을 사용하면 데이터를 라인단위로 읽을 수 있고, BufferedWriter는 newLine() 이라는 줄바꿈 해주는 메서드를 가지고 있다.

## **InputStreamReader와 OutputStreamWriter**

InputStreamReader/OutputStreamWriter는 바이트기반 스트림을 문자기반 스트림으로 연결시켜주는 역할을 한다. 

바이트기반 스트림의 데이터를 지정된 인코딩의 문자 데이터로 변환하는 작업을 수행한다.

### 생성자/메서드

| InputStreamReader(InputStream in) | OS에서 사용하는 기본 인코딩의 문자로 변환하는 InputStreamReader를 생성한다 |
| --- | --- |
| InputStreamReader(InputStream in, String encoding) | 지정된 인코딩을 사용하는 InputStreamReader를 생성한다. |
| getEncoding() | InputStreamReader의 인코딩을 알려준다. |
| OutputStreamWriter(OutputStream in) | OS에서 사용하는 기본 인코딩의 문자로 변환하는 OutputStreamWriter를 생성한다. |
| OutputStreamWriter(OutputStream in, String encoding) | 지정된 인코딩을 사용하는 OutputStreamWriter를 생성한다. |
| String getEncoding() | OutputStreamWriter의 인코딩을 알려준다. |