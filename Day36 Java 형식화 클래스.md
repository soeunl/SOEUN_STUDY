<Day36 - 0509>
<Java 형식화 클래스>

## 형식화 클래스

java.text 패키지 : 형식화 관련 편의 클래스 모음

❤️ DecimalFormat

    숫자 -> 형식화된 문자열
    10000 -> 10,000

    format(..) : 숫자 -> 형식화된 문자열
    parse(..) : 형식화된 문자열 -> 숫자

    0 패턴 : 빈 자리는 0으로 다 채움
    # 패턴 : 빈 자리는 채우지 않음

❤️ SimpleDateFormat

    날짜 형식화 : java.util.Date 객체
    String format(..) : Date 객체 -> 형식화된 문자열
    Date parse(..) : 형식화된 문자열 -> Date 객체

❤️ ChoiceFormat

    format

    80#B
    70이상 80미만 -> C,  80 -> B (80점부터 B)

    80<B
    70이상 80이하 -> C  , 80 -> C (81점부터 B)

❤️ MessageFormat

    static String format(..) : 형식화된 문자열
    Object[] parse(..) : 형식화된 문자열 -> 원래 데이터로 변환
