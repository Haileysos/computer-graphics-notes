
###	glColor3f(1.0f, 0.0f, 0.0f);
```c++
glColor3f(1.0f, 0.0f, 0.0f);
```
`glColor3f(R, G, B);` : 이후에 그려질 도형의 색상을 설정하는 함수
#### glColor3f(R, G, B);
- R = 1 / G = 0 / B = 0
- 드로잉 색상을 적색으로 설정

<br><br><br>

###	glRectf(-0.5f, -0.5f, 0.5f, 0.5f);
```c++
glRectf(-0.5f, -0.5f, 0.5f, 0.5f);
```
`glRectf(x1, y1, x2, y2);` : 두 개의 꼭짓점을 이용해서 사각형을 그리는 함수
#### 	glRectf(x1, y1, x2, y2);
- (x1, y1) → 첫 번째 꼭짓점 / (x2, y2) → 두 번째 꼭짓점
- (x1, y1), (x2, y2) 는 서로 대각선에 위치함
- 위 코드는 (-0.5, -0.5)와 (0.5, 0.5)를 꼭짓점으로 하는 화면 중앙의 정사각형을 그림
+ `glColor3f` 로 설정한 색상이 사각형에 적용됨  

<br><br><br>

<< 코드에는 없음 >>
### glOrtho(-1,1,-1,1,-1,1)
```c++
glOrtho(-1,1,-1,1,-1,1)
```
`glOrtho(left, right, bottom, top, near, far)` : 2D 직교 투영 좌표계를 설정하 함수  
#### glOrtho(left, right, bottom, top, near, far)
- x : -1 ~ 1 / y = -1 ~ 1
- 일반적으로 직교 투영으로 [-1, 1] 범위 내에서 작동
- 즉, 2 x 2 크기의 정사각형 좌표
- 우리가 그리는 모든 도형은 이 좌표계 안에서 그려짐
- `glOrtho(-1,1,-1,1,-1,1)` 공간 안에서 정사각형`glRectf(x1, y1, x2, y2);` 를 그림

●●●●●●●●●●●이건멀까염 Near<far


-> glOrtho(-1,1,-1,1,-1,1) 공간에 정사각형glRectf(-0.5f, 0.5f, 0.5f, -0.5f);을 그렸는데,  
결과는 왜 정사각형이 아니고 직사각형으로 찌그러져서 나오는걸까?
왜냐하면  
내가 강제로 출력창을 직사각형으로 만들었기 때문이다. glutInitWindowSize(640, 480);  
창의 비율 -> 640 : 480 = 4: 3
좌표계는 정사각형 / 창은 직사각형 / 따라서 정사각형이 직사각형 창에 맞게 찌그러져서 들어간거임
해결
glutInitWindowSize(640, 480); -> glutInitWindowSize(500, 500); 으로 변경하면 됨
창을 정사각형으로 맞춘거임

더 정확한 방법이 있음
●●●●●glViewport(GLint x, GLint y, GLsizei width, GLsizei height)  라는 게 있음
●●●●●glViewport(x, y, width, height);
●●●●●  (x, y) :왼아래점
●●●●● 이 점박이 파트 gpt에 물어봐서 보강


glViewport(0, 0, 500, 500); 쓰면 됨 근데 이게뭐냐면 (일단 무슨 뜻이냐면, 시작점: 왼쪽 아래 (0,0) / 크기: 500 x 500 라는 뜻) / 좌표계를 실제 화면에 매핑하는 영역을 설정하는 함
glViewport(x, y, width, height); : x, y = 시작점 (왼쪽 아래) / width, height = 출력 크기
glViewport()의 default값은 glutInitWindowSize와 같음. 기본적으로 창 전체 영역으로 설정되어있다는 말임.
뭔 말이냐면 기본적으로 창 전체에 그림을 꽉 채운다는 말.
glViewport()는 일반적으로 glutInitWindowSize와 동일하게 많이 설정.
glutInitWindowSize(500, 500); 👉 창의 크기 자체를 설정 (모니터에 보이는 창 크기)->창 크기 = 500x500
glViewport(0,0,500,500); 👉 그 창 안에서 실제로 그림을 그릴 영역 설정->구리는 영역도 = 500x500
즉, 창 전체를 다 사용
왜?
"창 전체에 꽉 차게 그림을 그리고 싶으니까."
만약 다르게 하면 어떻게 되냐?
glutInitWindowSize(500, 500);
glViewport(0, 0, 250, 250);
결과 -> 왼쪽 아래 1/4 영역에만 그림이 나옴
glutInitWindowSize(500, 500);
glViewport(100, 100, 300, 300);
결과 -> 화면 가운데 작은 사각형 영역에만 그림
즉
정리하면
창 크기랑 그리는 영역을 같은 크기로 맞춰서 전체 화면에 꽉 차게 그리기 위해서 같이 설정한다
즉, glViewport는 보통 창 전체 영역에 그림을 출력하기 위해 glutInitWindowSize와 동일한 크기로 설정하는 경우가 많다.
