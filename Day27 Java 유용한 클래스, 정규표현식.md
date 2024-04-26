<Day27 - 0425>
<JAVA 유용한 클래스, 정규표현식>

# 유용한 클래스

## java.lang.Math 클래스

    - 수학 관련 편의 기능 클래스
    - 모두 정적 메서드로 구성

    ◆ 임의의 수
        - random() : 0~1사이의 임의의 실수를 반환

    ◆ 올림, 버림 반올림
        - ceil(double a) : 올림
        - floor(double a) : 버림
        - round(double a) : 반올림

    ◆ 절대값 : abs()
        - (예) -10 -> abs(-10) -> 10

    ◆ 제곱 : pow()
        - (예) pow(2, 3) -> 2의 3제곱

    ◆ 무작위 난수 : random()
        - (예) random() -> 0~1 미만의 무작위 난수

    ◆ 루트값 : sqrt()
        - (예) sqrt(9) -> 3 (9의 루트값 3)

## java.util.Objects 클래스

    - 객체를 다룰 때 사용하는 편의 기능 모음
    - 모든 메서드가 정적(static)
    - equals : 두 객체간의 주소 비교
    - deepEquals : 중첩된 객체를 재귀적으로 주소 비교

    (참고) Arrays.equals(..), Arrays.deepEquals(...)

    - int hash(Object... values) : 해시코드 생성
    - int hashCode(Object o) : 객체의 해시코드 조회 및 생성
    - boolean isNull(..) : 참조 변수가 null인지 체크
    - boolean nonNull(..) : 참조 변수가 null 아닌지 체크
    - requiredNonNullElse(...) : 특정 변수가 null이면 기본값을 부여
    - boolean equals(..) : 두 객체를 비교
    - boolean deepEquals(..) : 두 객체를 재귀적으로 비교(다차원 배열 비교 가능 )

## java.util.Random 클래스

    - Math.random() : 0 ~ 1 미만의 난수

    ```Java
    double randNum = Math.random();
    double randNum = new Random().nextDouble(); // 위 문장과 동일

    ```

    ```Java (1~6 사이의 정수를 난수로 얻는 법)
    int num = (int)(Math.random() \* 6) + 1;
    int num = new Random().nextInt(6) + 1; // 위 문장과 동일

    ```

## java.util.Scanner 클래스

    - 화면, 파일, 문자열과 같은 입력소스로 부터 문자데이터를 읽어오는데 도움을 줄 목적으로 JDK1.5부터 추가되었음
    - java.io
    - 데이터를 입력 받을 때 사용하는 편의 클래스
        - 터미널에서 입력
            InputStream System.in

        - 파일
            File
            FileInputStream ...

        - 네트워크...

## java.util.StringTokenizer 클래스

    - StringTokenizer는 긴 문자열을 지정된 구분자(delimiter)를 기준으로 토큰(token)이라는 여러 개의 문자열로 잘라내는 데 사용함
    - StringTokenizer는 구분자로 단 하나의 문자 밖에 사용하지 못하기 때문에 보다 복잡한 형태의 구분자로 문자열을 나누어야 할 때는 어쩔 수 없이 정규식을 사용하는 메서드를 사용해야 함
    - 구분 문자를 가지고 문자를 분리할 때
    - 토큰 : 구분 문자

# 정규 표현식 - java.util.regex패키지

    - 난이도가 높음
    - java.util.regex
        Pattern 클래스 : 정규표현식 패턴 객체를 생성
            - static compile("정규식 패턴") - Pattern 객체 생성
            - static compile("정규식 패턴", 플래그)
                플래그
                    Pattern.CASE_INSENSITIVE: 대소문자 구분 X

            - Matcher matcher(CharSequence str) : 패턴을 체크

        Matcher 클래스 : 패턴의 일치 여부체크, 일치하는 문자열 추출
            - boolean find() : 패턴에 일치 여부 체크, 다음 패턴으로 이동
            - String group() : 패턴에 일치하는 문자열 추출, 특정 그룹의 문자열 추출 (패턴이 정확하게 일치해야 함)
            - boolean matches() : 패턴의 일치 여부 체크 - 해당 패턴이 문자열 처음부터 등장

    패턴
    \w - [a-zA-Z0-9]
    \W - [^a-zA-Z0-9_]
    \s - 공백 문자 1개
    \S - 공백 문자가 아닌 문자

    \b : 문자 클래스 -> 백스페이스 키
            문자 클래스 외부 -> 단어와 단어 사이 공백
    \B : 단어 단어 사이 공백이 없는 패턴

    패턴+ : 패턴을 1번 이상 반복

    ^ : 문자 클래스[^...] : 부정 문자 클래스 [^0-9]: 숫자가 아닌 문자
        문자 클래스 외부 -> 시작하는 패턴^java -> java로 시작하는 패턴
        2가지를 구분해서 이해해야 함

    $ : 끝나는 패턴 -> java$ -> java로 끝나는 패턴

    패턴{반복횟수} : [0-9]{4} : 숫자 4개 \d{4}

    패턴{반복횟수} : 패턴의 반복횟수 이상 : \d{4,} -> 숫자 4개 이상

    패턴{시작횟수, 종료횟수} : \d{4,5} -> 숫자 4개 이상 5개 이하

    패턴{,종료횟수} : 패턴을 종료 횟수 이하로 반복 \d{,4} -> 숫자 4개 이하 (자바는 시작 횟수도 기입하여야 함)

    패턴+ : 패턴의 1번 이상 반복 / 패턴{1,} // 최대 매치
    패턴* : 패턴의 0번 이상 반복 / 패턴{0,} // 최소 매치

    패턴? : 패턴이 있어도 되고 없어도 되는 패턴 / 패턴{0,1}

    단어1|단어2|단어3 : 단어1, 단어2, 단어3, 중 하나라도 있으면 되는 패턴

    (패턴) : 그룹핑
        - (ABC){3} : ABC 패턴이 3번 반복
        - 특정 그룹의 패턴으로 특정 그룹의 문자열을 추출
        - 이미지 태그에서 src="주소"

    전방 탐색(?=패턴) -> 패턴 앞에 있는 패턴 (예) \w*(?=:) : 문자 앞에 있는 단어 여러개 패턴
    전방 부정탐색 (?!=패턴) (예)\w*(?!=:) : 문자가 아닌 앞에 있는 패턴

# String 클래스 매서드 중 정규 표현식을 지원 형식

자바스크립트
/패턴/ -> 정규표현식 객체

    플래그
    /패턴/i -> 대소문자 구분 X (CASE_INSENSITIVE)
    /패턴/m -> 여러 줄에 걸쳐 패턴 체크(MULTILINE)
    /패턴/g -> global : 전역에 걸쳐 패턴 체크

test(문자열) : 패턴이 일치하는지 체크
exec(문자열) : 패턴에 일치하는 문자열을 추출 - 커서 이동하면서 다음 패턴의 문자열을 추출 - 더이상 찾을 패턴이 없으면 null을 반환

<a class="..." href="..."...>
<A CLASS="...>

대소문자 구분 X, 전역에 걸쳐 체크, 여러 줄에 걸쳐 체크
/패턴/igm

# String 클래스

    boolean endsWith(...) : 특정 문자열로 끝나는지 체크
    boolean starts(..) : 특정 문자열로 시작하는지 체크

    static join
    static format(..)
    substring

    empty : 여백 미포함 체크
    Blank : 여백 포함 체크 (11버전 이후)


    indexOf : 왼쪽에서 오른쪽으로 검색
    lastlndexOf : 오른쪽에서 왼쪽으로 검색
    matches

    stripLeading
    stripTrailing

    (참고)

    equalsIgnoreCase : 대소문자 구분 없이 비교
    Locale : 지역화
    indexOf : 배열의 인덱스
    isEmpty : 비어 있는 경우
    isBlank : 공백문자열 포함하여 값이 있냐 없냐 체크
    join : 문자 결합
    length : 문자열 길이
    matches : 맞는지 틀린지 체크
    split : 쪼개진 문자를 정해진 만큼만 가져올때
    strip : 여백제거
    trim : 여백제거
    stripLeading : 앞쪽 여백 제거
    stripTrailing : 뒤쪽 여백 제거
    substring : 특정위치부터 문자를 잘라줌 (beginIndex이상 endIndex 미만)
    valueOf : 문자열 객체
