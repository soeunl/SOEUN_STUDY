<Day38- 0513>
<Database 입출력, java.io 패키지 >

## 입출력(I/O) java.io 패키지

1. 입출력이란?

   - Input/Output 입력 / 출력
   - 컴퓨터 내부 또는 외부와 프로그램간의 데이터를 주고받는 것

2. 스트림(stream)
   - 데이터가 이동하는 통로
   - 입력 통로(입력 스트림)
   - 출력 통로(출력 스트림)

❤️ 바이트기반 스트림(1바이트) : 데이터 크기가 바이트 단위 / 1바이트씩 읽어오는 스트림

1.  💙 입력 스트림 - InputStream : 추상 클래스
    InputStream : int read()

    💛 기반 스트림 : 직접 데이터에 접근해서 읽어오는 스트림
    FileInputStream
    ByteArrayInputStream

    (참고)
    Unsigned : 양의 정수
    Unsined Byte 0~255

    입력 스트림의 끝에 도달한 경우 반환값이 -1 / 바이트 범위에서 부족 -> 더 큰 자료형
    int read()

    💛 보조 스트림 : 다른 스트림에 추가적인 기능을 부여

    - 생성자 매개변수 InputStream
      FilterInputStream : 보조스트림의 체계를 정리하기 위한 클래스 (BufferedInputStream, DataInputStream)
      ObjectInputStream
      InputStreamReader

2.  💙 출력 스트림 - OutputStream : 추상 클래스

        💛 기반 스트림 : 직접 데이터에 접근해서 출력하는 스트림
        FileOutputStream
        ByteArrayOutputStream

        💛 보조 스트림 : 다른 스트림에 추가적인 기능을 제공

        - 생성자 매개변수 OutStream
          FilterOutputStream : 보조스트림의 체계를 정의하기 위한 클래스 (BufferedOutputStream, DataOutptStream)
          ObjectOutputStream
          OutputStreamWriter

        (참고)
        데코레이터 패턴
        (핵심 기능을 추가기능(목적)과 함께 대신해서 수행해주는 패턴)
        핵심 기능이 목적이 아님

        class BufferedInputStream extends InputStream {

        private InputStream in;

        public BufferedInputStream(InputStream in) {

        this.in = in;

        }

        // read 메서드의 기능은 추가적인 기능과 함께 다른 스트림의 기능을 대신 수행

        public int read() {

            // 버퍼 기능에 대한 코드... // 추가 기능

            int byte = in.read();

            // 버퍼 기능에 대한 코드... //추가 기능

            return byte;

        }

    }

❤️ 문자기반 스트림 : 데이터 크기가 문자 단위(유니코드 - 2, 3 바이트)

1. 💙 입력 스트림 - Reader : 추상 클래스
   기반 스트림
   보조 스트림

2. 💙 출력 스트림

🤍 표준입출력 : 콘솔에 입력, 출력

1. System.in : InputStream
2. System.out : PrintStream
3. System.err : PrintStream

File

🤍 직렬화(Serialization)

- 객체에 저장된 데이터를 스트림에 쓰기(write)위해 연속적인(serial) 데이터로 변환하는 것을 말한다.

1. ObjectInputStream
2. ObjectOutputStream
