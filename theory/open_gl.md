## Open GL 이란?
- Open GL 은 프로그래밍 언어가 아니라 API 표준
- Open GL 은 GPU(그래픽카드) 에 명령을 전달하는 API  
- 명령 전달 루트 : CPU → Open GL → GPU 
- Khronos Group에서 관리

→ OpenGL = GPU 에게 “이렇게 그려라”하고 명령하는 규칙  
<br><br>

## 라이브러리  
- 특정 기능이 구현된 코드 집합(compiled code)

e.g. OpenCV, SDL, FreeType ...  
> 라이브러리 : 실제 기능  

<br><br>

## API    
- 함수 및 명령어들의 정의를 제공하는 인터페이스 규약
- 실제 구현이 아니라 “이렇게 써라”라는 약속

> API : 사용법

<br><br>

## Open GL 의 역할  
- c / c++ 같은 언어에서 Open GL 라이브러리를 호출해 사용  
- Open GL 은 '그리기' 기능만 있음
- 창 생성 /  마우스 입력 처리 기능 X

↓ 이런 기능을 미리 구현해서 가져다 쓰게 해주는 라이브러리들이 있음 !
<br>

## Open GL 을 도와주는 라이브러리들  
- 창(window)과 입력(input)을 다루는 라이브러리 
  - GLUT : Open GL Utility Toolkit, 오래된 라이브러리, 윈도우 생성, 입력 처리, 이밴트 루프 제공 → 학습에 용이
  - FreeGLUT : GLUT 의 오픈소스 대체 라이브러리, GLUT 와 100% 호환 → 우리가 사용  
- GLFW : 창 관리, 멀티모니터 지원, 조이스틱 제어 등 → 현대적인 게임 개발에 필요한 기능들을 가지고 있음
- GLM : 수학계산(행렬,벡터)을 편하게 해줌
<br><br>

# Open GL 이 호환성을 유지하는 방법  
? Open GL이 OS 나 GPU 제조사(NVIDIA, Intel 등)의 서로 다른 드라이버에서도 어떻게 호환성을 유지할까 ?
OpenGL 은 “표준(API)” 만 정의, 실제 구현은 GPU 제조사가 담당.  
즉, Open GL = 규칙 / GPU 제조사 = 실제 실행 코드 작성.  
GPU 제조사들(NVIDIA, Intel 등)은 Open GL 표준을 기반으로 자기 하드웨어에 맞는 드라이버를 만듦  
개발자는 OpenGL API 만 사용하면 됨, 어떠한 GPU 에서도 동일 코드 실행 가능    

→ Open GL은 “규칙”이고, GPU 제조사는 그 규칙을 실행하는 드라이버를 만듦  
<br><br>

## OPEN GL 구조

| 함수 접두어  |      소속     |            역할            |
| ------------ | -------------- | -------------------------- |
| gl           | OpenGL (Core)  | GPU(그래픽카드)에 직접 명령 |
| glu          | GLU (Utility)  | 복잡한 계산 처리           |
| glut         | GLUT (Toolkit) | 창/입력 관리               |


## 파이프라인  
- 두 개 이상의 분리된 상태 또는 단계가 이어지는 처리 과정

## Open GL 파이프라인 
OpenGL API 호출  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ↓  
명령 저장 (버퍼)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ↓  
변환 & 조명 (Transform & Lighting) : 물체 위치 이동/회전 + 빛 계산해 밝기/그림자 표현  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ↓  
래스터라이즈 (Rasterization) : 3D 에서 2D 픽셀로 변환  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ↓  
프레임버퍼 (Framebuffer) : 최종 화면 출력  
<br><br>

## 데이터 타입 함수 이름 규칙  
glColor3f(...)  

`gl` : open GL 라이브러리  
`Color` : 루트명령(기능)  
`3` : 인자의 개수  
`f` : 인자의 타입 (float)  






ㅡ실습ㅡ
파란색으로 채워진 창 출력하기
#inlcude<GL/glut.h>
#inlcude<stdio.h>
#inlcude<iostream>
//장면 렌더링
void RenderScene(void){
	std::cout << "RenderScene" << std::endl;
	//현재 색상을 사용하여 화면을 지운다
	glClear(GL_COLOR_BUFFER_BIT);
	//드로잉 명령을 전달한다
	glFlush();
}

void SetupRC(void){
	std::cout << "SetupRC" << std::endl;
	glClearColor(0.0f, 0.0f, 1.0f, 1.0f);
}

int main(int argc, char** argv){
	glutInit(&argc, argv);
	glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB);
	glutInitWindowSize(640, 480);
	glutInitWindowPosition(100, 100);
	glutCreateWindow("simple");

	SetupRC();
	glutDisplayFunc(RenderScene);

	glutMainLoop();
}
