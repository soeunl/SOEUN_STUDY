<Day37- 0510>
<Java 입출력>

## 입출력(I/O)

❤️ java.io 패키지

1. 입출력이란?

   - Input/Output 입력 / 출력 -> 입출력
   - 컴퓨터 내부 또는 외부와 프로그램간의 데이터를 주고받는 것
   - 데이터의 주고 받음을 위해 필요

2. 스트림(stream) -> 우리가 앞시간에 배웠던 스트림과 다른 스트림이다. 데이터가 이동하는 통로를 뜻하는 개념

   - 데이터가 이동하는 통로
   - 입력 통로(입력 스트림)
   - 출력 통로(출력 스트림)

❤️ 입력 스트림

    - 바이트 단위 스트림(1바이트)
    🤍InputStream

    - 문자 단위 스트림(2~3바이트)
    🤍Reader

❤️ 출력 스트림

    - 바이트 단위 스트림(1바이트)
    🤍OutputStream

    - 문자 단위 스트림(2~3바이트)
    🤍Wirter

💛 바이트기반 스트림 : 데이터 크기가 바이트 단위 / 1바이트씩 읽어오는 스트림

1. 입력 스트림 - InputStream : 추상 클래스 - int read()가 핵심적인 메서드이다! 1바이트씩 읽어 오는 형태(int read())

   🤍 기반 스트림 : 직접 데이터에 접근해서 읽어오는 스트림
   FileInputStream - 직접 접근해서 1바이트씩 읽어오는 스트림 / 파일을 전부 다 읽으면 -1을 반환
   ByteArrayInputStream

   (참고)
   Unsigned : 양의정수
   Unsigned Byte 0 ~255

   입력스트림의 끝에 도달한 경우 반환값이 -1 / 바이트 범위에서 부족 -> 더 큰 자료형
   int read()

   🤍 보조 스트림 : 다른 스트림에 추가적인 기능을 부여해주는 스트림 (생성자 매개변수가 InputStream / 데코레이터 패턴)
   FilterInputStream : 보조스트림의 체계를 정리하기 위한 클래스

   - BufferedInputStream : 버퍼 기능추가 - 기본 버퍼 8kb
   - DataInputStream : 기본 자료형으로 데이터를 읽을 수 있는 기능 추가

   ObjectInputStream : 객체 형태로 변환하여 읽어오는 기능 추가
   InputStreamReader : 바이트 단위 스트림 -> 문자 단위 스트림으로 변환 기능

2. 출력 스트림 - OutputStream : 추상 클래스. void wirte(int...)
   🤍 기반 스트림 : 직접 데이터에 접근해서 출력하는 스트림 : 1바이트씩 읽어 오는 형태(int read())
   FileOutputStream
   ByteArrayOutputStream

   🤍 보조 스트림 : 다른 스트림에 추가적인 기능을 제공 - 생성자 매개변수 OutputStream
   FilterOutputStream : 보조스트림의 체계를 정의하기 위한 클래스

   - BufferedOutputStream : 출력스트림 + 버퍼기능
   - DataOutputStream : 기본 자료형으로 쓰기 기능 제공

   ObjectOutputStream : 객체 형태로 데이터를 출력하는 기능 추가
   OutputStreamWriter : 바이트 단위 스트림 -> 문자 단위 스트림으로 변환 기능

   (참고)
   데코레이터 패턴

💛 문자기반 스트림 : 데이터 크기가 문자 단위(유니코드 - 2, 3 바이트)

1. 입력 스트림

   - Reader : 추상 클래스(추상메서드가 정의)
     - 기반 스트림 : 데이터에 직접 접근하는 스트림
       - FileReader
       - CharArrayReader
       - StringReader
     - 보조 스트림 : 입력 스트림 + 추가기능 - 생성자 매개변수 Reader
       - FilterReader
         - BufferedReader : 버퍼기능
     - InputStreamReader
       : 바이트 단위 스트림 -> 문자 단위 스트림으로 변환 기능
       : Reader로 사용이 불가한 InputStream인 경우 변환
       : 생성자 매개변수 String charSetName, Charset cs : 변환하려고 하는 문자표(유니코드..)
       2바이트 유니코드
       3바이트 유니코드

2. 출력 스트림

   - Writer
     - 기반 스트림 : 데이터에 직접 접근하는 스트림
       - FileWriter
       - CharArrayWriter
       - StringWriter
     - 보조 스트림 : 출력 스트림 + 추가기능 - 생성자 매개변수 Writer
     - BufferedWriter : 버퍼기능
     - OutputStreamWriter : 바이트 단위 스트림 -> 문자 단위 스트림으로 변환 기능

❤️ 표준입출력 : 콘솔에 입력, 출력

1. System.in : InputStream
2. System.out : PrintStream
3. System.err : PrintStream

File

❤️ 직렬화(Serialization)

- 객체에 저장된 데이터를 스트림에 쓰기(write)위해 연속적인(serial) 데이터로 변환하는 것을 말한다.

1. ObjectInputStream
2. ObjectOutputStream
