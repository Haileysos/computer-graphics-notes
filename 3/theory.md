
### glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB);
```c++
glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB);
```  
`glutInitDisplayMode()` : 창의 표시 방식(display mode)을 초기 설정하는 함수

`GLUT_SINGLE` : 싱글 버퍼 사용 → 버퍼를 하나만 사용하는 방식  
`GLUT_DOUBLE` : 더블 버퍼 사용 → 버퍼를 두 개 사용하는 방식  

`GLUT_RGB` : 색상을 RGB 방식으로 표현하겠다는 뜻  
###### 버퍼(buffer)는 화면에 그릴 내용을 잠시 담아두는 공간  

#### 싱글 버퍼 
- 모든 드로잉 명령이 출력창에서 진행됨  
- 그림을 그리는 공간 = 실제 화면에 보여지는 공간
#### 더블 버퍼  
- 드로잉 명령이 오프스크린 버퍼에서 실행된 후, 출력창으로 옮겨지는 방식으로 진행됨
- 애니매이션 효과를 낼 때 주로 사용  
#### RGB
- Red / Green / Blue    
- 색상을 RGB 계열로 쓰겠다는 뜻
- 실제 색 지정 함수에서는 Alpha 값까지 포함해 RGBA 형식으로 사용하는 경우가 많음

<br><br>

###	SetupRC();
```c++
SetupRC();
```  
`SetupRC();` : 렌더링 전에 필요한 Open GL 초기화  
#### SetupRC();
- Open GL 에서 제공하는 함수가 아님. 우리가 만든 그냥 함수 (함수 이름 변경 가능)  
- Open GL 은 상태 기반(State Machine)이라 “미리 설정해둔 값”을 기준으로 그림을 그림  
- 그래서 그리기 전에 환경세팅을 해줘야 함 (배경색/조명/색상 등)  
- 프로그램 싱행 시 딱 한 번만 실행됨  

<br><br>

###	glutMainLoop();
```c++
glutMainLoop();
```
`glutMainLoop();` : GLUT 프레임웍 실행  
#### glutMainLoop();
- 프로그램이 본격적으로 시작
- 프로그램이 종료될 때까지 운영체제에 관련된 event loop 수행
- 키보드 입력, 마우스 입력, 창 크기 변경 등의 event 감지 → 해당 event 에 연결된 콜백 함수 호출
- 즉, event를 기다리면서 콜백 함수를 계속 실행하는 무한 루프  

<br><br>

###	glClearColor(0.0f, 0.0f, 1.0f, 1.0f);
```c++
glClearColor(0.0f, 0.0f, 1.0f, 1.0f);
```
`glClearColor(R, G, B, A);` : 화면을 지울 어떤 색으로 지울지 "색을 결정"하는 함수
#### glClearColor(R, G, B, A);
- 어떤색으로 초기화 할 지 결정  
- ★ 실제로 화면을 지우기 위해서는 glClear 을 호출해야 함 ★  

<br><br>

###	glClear(GL_COLOR_BUFFER_BIT);
```c++
glClear(GL_COLOR_BUFFER_BIT);
```
`glClear(GL_COLOR_BUFFER_BIT);` : 
#### glClear(GL_COLOR_BUFFER_BIT);
- 














	glFlush();
지금까지 내가 호출한 Open GL 명령들을 드라이버안에만 쌓아두지말고, GPU가 실제로 보기 시작 할 수 있는 쪽으로 보냄
주로 GLUT_SINGLE(단일버퍼)인 경우 사용
	glutDisplayFunc(func); 이거 중요하다★
func함수를 호출하는 콜백함수
창의 이동/크기 변경될때마다 호출됨

Open GL Command Flow : CPU -> Driver -> GPU -> Framebuffer -> Display(Monitor)

출력창 초기 실행시 검정색만출력(초기샛팅값=파란색)or흰색화면만출력
가정:gpu 혹은os종류 및 버전에 따라 더블버퍼를 기본값으로 사용하는 경우
해결 : 
glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB);-> glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB);
glFlush(); -> glutSwapBuffers();
glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB); -> glFinish();
