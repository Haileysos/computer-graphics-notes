
###	glColor3f(R, G, B);
```c++
glColor3f(1.0f, 0.0f, 0.0f);
```
: 이후에 그려질 도형의 색상을 설정하는 함수  
- R = 1 / G = 0 / B = 0
- 드로잉 색상을 적색으로 설정

<br><br><br>

###	glRectf(x1, y1, x2, y2);
```c++
glRectf(-0.5f, -0.5f, 0.5f, 0.5f);
```
: 두 개의 꼭짓점을 이용해서 사각형을 그리는 함수  
- (x1, y1) → 첫 번째 꼭짓점 / (x2, y2) → 두 번째 꼭짓점
- (x1, y1), (x2, y2) 는 서로 대각선에 위치함
- 위 코드는 (-0.5, -0.5)와 (0.5, 0.5)를 꼭짓점으로 하는 사각형을 그림
- glRectf(-0.5f, 0.5f, 0.5f, -0.5f); 도 가능함  
  → (-0.5, 0.5) (0.5, -0.5)를 꼭 짓점으로 하는 사각형이랑 똑같으니까
+ `glColor3f` 로 설정한 색상이 사각형에 적용됨  

<br><br><br>

### glOrtho(left, right, bottom, top, near, far)  ★ 순서 외워야 함
```c++
glOrtho(-1,1,-1,1,-1,1)
```
: 2D 직교 투영 좌표계를 설정하는 함수  
- 카메라 뷰
- x : -1 ~ 1 / y = -1 ~ 1 이 범위를 화면 꽉 채워서 보여줌
- 즉, 2 x 2 크기의 정사각형 좌표
- 우리가 그리는 모든 도형은 이 좌표계 안에서 그려짐
- `glOrtho(-1,1,-1,1,-1,1)` 공간 안에서 정사각형`glRectf(-0.5f, -0.5f, 0.5f, 0.5f);` 를 그림
- near < far 항상 near보다 far가 값이 커야함

<br><br><br>

### glMatrixMode(GL_PROJECTION); 
```c++
glMatrixMode(GL_PROJECTION);
```  
: 카메라/뷰포트 설정   
- 좌표값이 3개 존재함  
  1. 월드 좌표
  2. 카메라 좌표(카메라가 있어야 할 위치를 알려주는)
  3. 오브젝트의 좌표(우리가 그리는 오브젝트)
- 3D좌표를 2D화면에 매핑하는 과정  
  : glOrtho(), gluPerspective()등을 사용하여 카메라의 시야(FOV)설정

<br><br><br>  

### glMatrixMode(GL_MODELVIEW);
```c++
glMatrixMode(GL_MODELVIEW);
```    
: 객체변환 (이동, 회전, 크기변경)   
- glTranslatef(), glRotatef(), glScalef() 등을 사용하여 모델(도형)의 위치 및 크기 변환  
- 일반적으로 투영 행렬(GL_PROJECTION) 을 먼저 설정한 후, 모델뷰 행렬(GL_MODELVIEW)을 설정
- 일반적으로 glutReshapeFunc()에 적용 << 근데 우리는 일단 이거 씀glutDisplayFunc(RenderScene);

<br><br><br>  

### glViewport(GLint x, GLint y, GLsizei width, GLsizei height);
```c++
glViewport(0, 0, 500, 500); 
```    
: 좌표계를 실제 화면에 매핑할 영역을 설정하는 함수    
- x, y = 시작점 (왼쪽 아래) / width, height = 출력 크기
- glutInitWindowSize 창 안에서 실제로 그림을 그릴 영역을 설정하는 것
- 위 코드는 시작점이 왼쪽 아래 (0,0) 그리고 크기: 500 x 500
- glViewport()의 기본값은 glutInitWindowSize와 같음  
- 기본적으로 창 전체 영역으로 설정되어 있다는 말임
- glViewport()는 일반적으로 glutInitWindowSize와 동일하게 많이 설정
- 왜? "창 전체에 꽉 차게 그림을 그리고 싶으니까."

<br><br><br>
