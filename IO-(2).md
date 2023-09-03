# 입출력(I/O)-(2)

---

# 표준입출력과 File

## **표준입출력**

표준입출력은 콘솔(console, 도스창)을 통한 데이터 입력과 출력을 의미한다.

자바에서 표준입출력(standard I/O)를 위해 3가지 입출력 스트림을 제공하며, 자동적으로 생성되기때문에 스트림을 생성하는 코드를 작성하지 않아도 사용이 가능다.

### **표준입출력 스트림**

System.in: 콘솔로 부터 데이터를 입력받는데 사용

System.out: 콘솔로 데이터를 출력하는데 사용

System.err: ****콘솔로 데이터를 출력하는데 사용

### **표준입출력의 대상변경**

| static void setOut(PrintStream out) | System.out의 출력을 지정된 PrintStream으로 변경다. |
| --- | --- |
| static void setErr(PrintStream err) | System.err의 출력을 지정된 PrintStream으로 변경한다. |
| static void setIn(PrintStream in) | System.in의 입력을 지정된 PrintStream으로 변경한다. |

그러나 JDK 1.5부터 Scanner클래스가 제공되면서 System.in으로부터 데이터를 입력받아 작업하는 것이 편리해졌다.

## **RandomAccessFile**

자바에서는 입력과 출력이 각각 분리되어 별도로 작업하도록 설계되어 있으나, RandomAccessFile는하나의 클래스로 파일에 대한 입출력을 모두 할 수 있도록 되어있다.4

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/1f63df65-c224-4be6-a04f-ef58c544f3b3">

DataInputStream은 DataInput 인터페이스를 DataOutputStream은 DataOuput인터페이스로 구현되어있다. 이 두개의 클래스는 기본 자료형을 읽고 쓰기 위한 메서드 이기 때문에, RandomAccessFile클래스도 기본자료형 단위로 데이터를 읽고 쓸 수 있다.

### 생성자/메서드

| RandomAccessFile(File file, String mode)
RandomAccessFile(String fileName, String mode) | 주어진 file에 읽기 떠는 읽기와 쓰기를 하기 위한 RandomAccessFile인스턴스를 생성한다.
mode는 "r"가 "w" 두가지 값이 지정이 가능하다. "r" - 읽기 "w" - 쓰기 "rw" - 읽기와 쓰기 |
| --- | --- |
| FileChannel getChannel() | 파일의 파일 채널을 반환한다. |
| FileDescriptor getFD() | 파일의 파일 디스크립터를 반환한다. |
| long getFilePointer() | 파일 포인터의 위치를 알려준다. |
| long length() | 파일의 크기를 얻을 수 있다 ( Byte 단위 ) |
| void seek(long pos) | 파일 포인터의 위치를 변경한다. 위치는 파일의 첫 부분부터 pos크기만큼 떨어진 곳이다 (Byte 단위 ) |
| void setLength(long newLength) | 파일의 크기를 지정된 길이로 변경한다 (Byte단위) |
| int skipBytes(int n) | 지정된 수만큼 byte를 건너뛴다. |

## File

앞서 살펴본 입출력 스트림을 사용하면 파일을 통한 입출력 작업을 수행할 수 있다. 하지만 파일의 제거나 디렉터리에 관한 작업 등은 입출력 스트림을 통해서는 수행할 수 없다.

자바는 이러한 입출력 작업 이외의 파일과 디렉터리에 관한 작업을 File 클래스를 통해 처리하도록 하고 있다.

### 생성자/메서드


| File(String fileName) | 주어진 문자열을 이름으로 갖는 파일을 위한 File인스턴스를 생성한다. 파일 뿐만 아니라 디렉토리도 같은 방법으로 다룬다. |
| --- | --- |
| File(String pathName, String fileName)
File(File pathName, String fileName) | 파일의 경로와 이름을 따로 분리해서 지정할 수 있도록 한 생성자. 이 중 두번째 것은 경로를 문자열이 아닌 File인스턴스인 경우를 위해 제공 된 것이다. |
| File (URI uri) | 지정된 uri로 파일을 생성 |
| String getName() | 파일이름을 String으로 반환 |
| String getPath() | 파일의 경로는 String으로 반환 |
| String getAbsolutePath()
File getAbsoluteFile() | 파일의 절대경로를 String 또는 File로 반환 |
| String getParent()
File getParentFile() | 파일의 조상 디렉토리를 String 또는 File로 반환 |
| String getCanonicalPath()
File getCanonicalFile() | 파일의 정규경로를 String 또는 File로 반환 |
| static String pathSeparator
static char pathSeparatorChar | OS에서 사용하는 경로 구분자 ( 윈도우 ";" 유닉스,리눅스 : ":" ) |
| static String separator
static char separatorChar | OS에서 사용하는 이름 구분자 ( 윈도우 "\", 유닉스,리눅스 : "/" ) |

---

## 직렬화(Serialization)

직렬화(Serialization)란 객체를 데이터 스트림으로 만드는 것을 말한다.

즉, 객체에 저장된 데이터를 스트림에 쓰기위해 연속적(serial)인 데이터로 변환하는 것을 말한다.

반대로 스트림으로부터 데이터를 읽어서 객체를 만드는 것을 역직렬화(deserialization)이라고 한다.

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/c55566f8-2455-4591-980b-ef505c2ecdcc">

## ObjectInputStream, ObjectOutputStream

### **ObjectOutputStream 객체 직렬화**

직렬화(스트림에 객체를 출력) 에는 ObjectOutputStream을 사용한다.

객체가 직렬화될때 오직 객체의 인스턴스 필드값 만을 저장한다. static 필드나 메서드는 직렬화하여 저장하지 않는다.

### **ObjectInputStream 객체 역직렬화**

역직렬화(스트림으로부터 객체를 입력)에는 ObjectInputStream을 사용한다.

단, 역직렬화 할때 주의사항이 있는데, 직렬화 대상이 된 객체의 클래스가 외부 클래스라면, 클래스 경로(Class Path)에 존재해야 하며 import 된 상태여야 한다.

ObjectInputStream, ObjectOutputStream 은 각각 InputStream과 OutputStream을 직접 상속 받지만 기반스트림을 필요로 하는 보조스트림이다. 그래서 객체를 생성할때 입출력 할 스트림을 지정해주어야 한다.

## 직렬화가 가능한 클래스 만들기- Serializable, transient

### **Serializable**

객체 직렬화는 객체에 implements Serializable 만 선언해 주면 된다.

- 기본형 타입(boolean, char, byte, short, int, long, float, double)은 직렬화가 가능
- Serializable 인터페이스를 구현한 객체여야 한다. (Vector 클래스는 Serializable 인터페이스구현)
- 해당 객체의 멤버들 중에 Serializable 인터페이스가 구현되지 않은게 존재하면 안된다.
- transient 가 사용된 멤버는 전송되지 않는다. (보안 변수 : null 전송)

### transient

객체의 데이터 중 일부의 데이터는(패스워드와 같은 보안) 여러가지 이유로 전송을 하고 싶지 않을 수 있다. 이러한 변수는 직렬화에서 제외해야 되며, 이를 위해서 변수에 transient를 선언한다.

transient가 붙은 인스턴스변수의 값은 그 타입의 기본값으로 직렬화된다.

## 직렬화가능한 클래스의 버전관리

### **SerialVersionUID**

Serializable 인터페이스를 구현하는 모든 직렬화된 클래스는 serialVersionUID(이하 SUID) 이라는 고유 식별번호를 부여 받는다. 이 식별 ID는 클래스를 직렬화, 역직렬화 과정에서 동일한 특성을 갖는지 확인하는데 사용된다. 그래서 클래스 내부 구성이 수정될 경우, 기존에 직렬화한 SUID와 현재 클래스의 SUID 버전이 다르기 때문에 이를 인지하고 InvalidClassException 예외가 발생시켜 값 불일치 되는 현상을 미연에 방지한다.

단, 직렬화 스펙 상 serialVersionUID 값 명시는 필수가 아니며, 만일 클래스에 SUID 필드를 명시하지 않는다면, 시스템이 런타임에 클래스의 이름, 생성자 등과 같이 클래스의 구조를 이용해 암호 해시함수를 적용해 자동으로 클래스 안에 생성하게 된다.

### **클래스 버전 수동 관리**

만일 네트워크로 객체를 직렬화하여 전송하거나 협업을 하는 경우 수신자와 송신자 모두 같은 버전의 클래스를 가지고 있어야 할텐데, 만일 클래스가 조금만 변경사항이 있으면 모든 사용자에게 재배포해야 하는 애로사항이 생겨 프로그램을 관리하기 어렵게 만든다.

따라서 직렬화 클래스는 왠만한 상황에선 serialVersionUID 를 직접 명시해주어 클래스 버전을 수동으로 관리하는 것을 권장하는 편이다. SUID를 직접 명시해주면 클래스의 내용이 변경되어도, 클래스의 버전이 시스템이 자동 생성된 값으로 변경되지 않기 때문이다. 이외에도 런타임에 SUID를 생성하는 시간도 많이 잡아먹기 때문에 미리 명시를 강력히 권장되는 바이다.

serialVersionUID 는 private static final 으로 선언해야 하며 타입은 long 이다.