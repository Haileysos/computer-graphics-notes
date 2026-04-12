우리가 그림을 그리고 있는 공간은 Ortho 그래픽 공간이다.  
내쪽으로 튀어나오냐 들어가느냐가 z축이 됨 (내 쪽으로 튀어나오는게 +z 방향)   

# 점 그리기  
- 3D 캔버스 내에서 무언가를 그릴 지점을 선택하기 위해서는 OpenGL함수인 glVertex()를 사용
- x축으로 50만큼 y축으로 50만큼 이동한 지점에 점을 찍는 코드
  - glVertex3f(50.0f, 50.0f 0.0f); (Z 좌표는 0.0으로 고정)
	- glvertex2f(50.0f, 50.0f)
	- glVertex4f()

### `glBegin(GL_POINTS)`  
- glBegin의 인자인 GL_POINT는 OpenGL로 하여금 이어지는 버텍스가 점으로 해석되도록 함
- 따라서 이어지는 두 좌표는 점으로 해석되어, 화면에 두 점이 그려짐
```c++
glBegin(GL_POINTS); //기본 모델로 점을 선택한다.
glVertex3f(0.0f, 0.0f, 0.0f);	// 점을 지정한다.
glVertex3f(50.0f, 50.0f, 50.0f); // 또 다른 점을 지정한다.
```
<br>
### `glPointSize(GLfloat크기)`  
- 점의 크기 변경










이거 먼소리지  

지원되는 점의 크기 범위와 단계를 얻어야....... 어느 범위 내에서 크기를 설정해야하는 지 알아야.....
	- 시스템에서 지원되는 점 크기의 범위(size), 점 크기 사이의 최소치 (단계값, step)
	GLfloat sizes[2];		// 지원되는 점 크기의 범위를 저장한다.
	GLfloat step;		// 지원되는 점 크기의 간격을 저장한다.
	GLGetfloatv(GL_POINT_SIZE_RANGE, sizes);
	GLGetfloatv(GL_POINT_SIZE_GRANULARITY, &step);
	- sizes 배열은 각각 지원되는 점의 최소치와 최대치를 저장
	- step 변수는 크기 사이의 간격을 저장
