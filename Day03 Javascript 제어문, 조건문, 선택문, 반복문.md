<Day03 - 0321>
<Javascript 제어문(조건문, 선택문, 반복문)>

# 조건문
    - 조건식의 값이 참(true), 거짓(false)인지에 따라 제어
    - 소괄호() 안에는 조건식, 중괄호{} 안에는 실행 코드가 주로 들어감
    - 조건식에서 false가 되는 기타 데이터
            * 0, null, ""(빈문자), null, undefined는 false로 인식을 하고 그 이외의 값은 true로 인식
    - 조건식을 여러개 사용할 경우 논리연산자 사용
            * 조건식1|| 조건식2 : 조건식1이 참이거나 조건식2가 참일때
            * 조건식1 && 조건식2 : 조건식1과 조건식2가 모두 참일때
    - if문 안에 if 문을 중첩해서 사용할 수 있음

        (예시) 
            if(조건식) {// 논리, 비교 연산자가 주로..
            // 조건식이 참일 때 실행되는 코드
            }

        (예시)
            if(조건식) {
            // 조건식이 참일 때 실행되는 코드
            } else {
                // 조건식이 거짓일 때 실행되는 코드
            }

        (예시)
            if (조건식1) {
            // 조건식1이 참일 때 실행되는 코드
            } else if (조건식2) {
                // 조건식1은 거짓이고 조건식2가 참일 때 실행되는 코드
            } else if (조건식3) {
                // 조건식1, 조건식2는 거짓이고 조건식3이 참일 때 실행되는 코드
            } else {
                // 모든 조건이 거짓일 때 실행되는 코드
            }


# 선택문
    - 여러개(case) 중에서 하나를 선택
    - 값의 일치 여부 체크, 선택
    - 변수에 할당된 값이 case의 각 값에 매칭되면 매칭된 코드가 실행 
    - 키워드 값과 일치하는 시점 -> 실행 시점, break를 만날때까지 실행
    - 최종적으로 매칭되는 값이 없는 경우는 default 부분의 코드 실행
    - 각 case에서 break가 없다면 매칭이 된 case가 있으면 다음 case로    넘어가며 값을 계속 출력

        (예시) 
            var 변수 = 초기값;
            switch (변수) {
                case 값1 : 코드1;
                    break;
                case 값2 : 코드2;
                    break;
                case 값3 : 코드3;
                    break;
                case 값4 : 코드4;
                    break;
                default : 코드5;	// 일치하는 키워드가 없는 경우
            }


        (예시)
            var floor = 3;
            switch (floor) {
                case 1 : console.log("1층");
                    break;
                case 2 : console.log("2층");
                    break;
                case 3 : console.log("3층");
                    break;
                case 4 : console.log("4층");
                    break;
                case 5 : console.log("5층");
                    break;
            }


# 반복문
    1. while문
        
        while (조건식) {
                // 조건식이 true일때 반복 실행되는 부분 
            }

        (예시)
        var total = 0;
        var num = 1;

        while(num <= 100){
            total += num;  // total = total + num;
            num++  //num = num + 1;
        }

        console.log(total); -> 5050

     - while구분에서는 반복 구간을 탈출할 수 있는 조건을 반드시 구현해야함
        (없을 경우 무한 loop)

     2. do ~ while문
        - do { }로 정의된 반복 실행을 적어도 1번은 실행하고 while 조건식에 따라 반복
        - 조건이 거짓이더라도 한번은 실행됨 (조건식이 아래쪽에 있기 때문)
        - 조건식 : 반복을 유지하는 조건 / 반복을 중단할 수 있는 조건

        var 변수 = 초기값; 

            do {
                // 최소 한번 이상 실행되는 반복 처리
            } while(조건식);

        (예시)   
        var num = 10;
            do {
                console.log(num); // 10
                num++;
            } while (num < 10);

         (예시)
         var total = 0, num = 1;

            do {
                total += num;
                num++
            } while (num <= 100);

    3. for문
        - 횟수가 정해진 반복문에 특화된 형태
        - while, do~while과 마찬가지로 조건식을 만족하면 반복
        - for문은 초기값, 조건식, 증감식을 통한 일정 구간 반복

            for(초기값; 조건식; 증감식) {
                // 반복 실행되는 코드
            }

            (예시)
            var total = 0;
            for (var i = 0; i < 100; i++) { total += i;}


        * 횟수가 정해진 반복문의 필수 요소
            - 초기값, 조건식, 증감식

        * 반복문의 관례
            - 횟수, 순서
                index : 0부터 시작하는 순서 번호
                index에서 따온 변수명 i를 관례적으로 사용
                i 다음에는 알파벳 순서대로 j, k ... 

        * break : 반복문을 중단

        * continue : 반복 건너뛰기


# 짝수만 구하기
    - var total = 0
        for (var i = 1; i <=100; i++) {
            if ( i % 2 == 1 ) {
                continue // 홀수 일때 건너뛰기
            }
            total += i; // 짝수
        }

   - var total = 0
        for (var i = 1; i <=100; i++) {
            if ( i % 2 == 1 ) {
                // 홀수
            } else {
                // 짝수
            }
        }


# 중첩반복문
    - 반복문 안에 반복문
        while + while, whlie + for, ..
        for + while, for + for ..


# 구구단 만들기
    - for (var i=2; i<=9; i++) {
        console.log('-------' + i + '단------');
        for (var j=1; j<=9; j++) {
            console.log( i + 'X' + j + '=' + (i*j));
        }
    }


    