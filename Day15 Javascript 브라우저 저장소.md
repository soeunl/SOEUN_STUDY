<Day15 - 0408>
<Javascrip 브라우저 저장소>

브라우저 저장소 - 키 - 값(문자열로 저장이 가능)

localStorage : 브라우저는 종료해도 데이터가 유지
sessionStorage : 브라우저를 종료하면 데이터가 삭제

    추가, 수정
        setItem("키", "값");

    조회
        getItem("키");

    삭제
        removeItem("키");

    전체삭제
        clear();

객체 -> JSON 문자열 - JSON.stringify(객체);
JSON 문자열 -> 객체 - JSON.parse(JSON 문자열);
