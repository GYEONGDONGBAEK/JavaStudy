<h2>1. 배열이란?</h2>
<p>배열은 같은 타입의 여러 변수를 하나의 묶음으로 다루는 것입니다.</p>
<p>배열의 참조변수는 실제 값이 저장되는 것이 아닌 실제 값이 저장된 위치의 주소를 가집니다.</p>
<pre><code>// 정수형 변수 score 1 ~ 5
int score1, score2, score3, score4, score5;
// 정수형 배열 참조변수 score
int[] score = new int[5];</code></pre>
<h2>2. 배열의 선언과 생성</h2>
<p>배열의 선언 : 배열을 다루기 위한 참조변수의 선언</p>
<table>
  <thead>
    <tr>
      <th>선언방법</th>
      <th>선언예</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>타입[] 변수이름;</td>
      <td>int[] score;</td>
    </tr>
    <tr>
      <td>타입 변수이름[];</td>
      <td>int score[];</td>
    </tr>
  </tbody>
</table>
<pre><code>// 배열을 선언(배열을 다루기 위한 참조변수 선언)
타입[] 변수이름;
int[] score;
// 배열을 생성(실제 저장공간을 생성)
변수이름 = new 타입[길이]
score = new int[5];</code></pre>

<h2>3. 배열의 인덱스</h2>
<p>배열의 인덱스 : 각 요소에 자동으로 붙는 번호입니다.</p>
<p>인덱스(index)의 범위는 0부터 배열의 길이-1까지입니다.</p>
<pre><code>int[] score = new int[5];
// score의 길이는 5이지만 인덱스는 0 ~ 4까지입니다.</code></pre>

<h2>4. 배열의 길이</h2>
<p>배열이름.length : 배열의 길이(int형 상수)</p>
<p>배열은 한번 생성하면 그 길이를 바꿀 수 없습니다.</p>
<p>배열은 연속적인 값의 집합이기 때문에 각 배열의 크기는 정해져 있습니다.</p>
<p>배열 뒤에 메모리의 공간이 비어있는지 확신할 수 없기 때문에 크기 변동이 안됩니다.</p>
<p>만약에 더 큰 사이즈로 바꾸고 싶으면 새롭게 큰 공간에 기존 배열을 복사해주어야 합니다.</p>
<p>int[] arr = new int[5]; // 길이가 5인 int 배열</p>

<h2>5. 배열의 초기화</h2>
<p>배열의 각 요소에 처음으로 값을 저장하는 것</p>
<p>자동초기화가 된다(int는 0으로 초기화 된다)</p>
<pre><code>// 초기화 방법 1
int[] score = new int[5];
score[0] = 50;
score[1] = 60;
score[2] = 70;
score[3] = 80;
score[4] = 90;
// 초기화 방법 2
int[] score = { 50, 60, 70, 80, 90 };
// 방법 2는 나눠서 초기화할 수 없다
int[] score;
score = {50, 60, 70, 80, 90};
// 방법 2를 나눠서 초기화할 경우 방법3
int[] score;
score = new int[]{50, 60, 70, 80, 90};</code></pre>

<h3>6. 배열의 출력</h3>
<pre><code>int[] iArr = { 100, 95, 80, 70, 60 };
// 배열을 가리키는 참조변수 iArr의 값을 출력한다
System.out.println(iArr); // [I@14318bb]와 같은 메모리의 주소가 출력된다
// 예외로 char 배열은 값이 출력이 된다
char[] chArr = { 'a', 'b', 'c', 'd' };
System.out.println(chArr); // abcd
// for문을 사용
for(int i = 0; i < iArr.length; i++) {
System.out.println(iArr[i]);
}

// 배열 iArr의 모든 요소를 출력한다.[100, 95, 80, 70, 60]이 출력된다
System.out.println(Arrays.toString(iArr));// 문자열로서 출력 된다</code></pre>

<h3>7. 배열의 활용</h3>
<pre><code>// 1. 총합과 평균
int sum = 0;
float average = 0f;
int[] score = {100, 88, 100, 100, 90};

for(int i = 0; i < score.length; i++) {
sum += score[i];
}
average =(float)sum/score.length ;

System.out.println("총합 : " + sum);
System.out.println("평균 : " + average);

// 2. 최대값과 최소값
int[] score = {79, 88, 91, 32, 100, 55, 95};

int max = score[0], min = score[0];