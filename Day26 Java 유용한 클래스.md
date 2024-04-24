<Day26 - 0424>
<JAVA 유용한 클래스>

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

    - int hash(Object... values) :
    - int hashCode(Object o)

## java.util.Random 클래스

## java.util.Scanner 클래스

## java.util.StringTokenizer 클래스
