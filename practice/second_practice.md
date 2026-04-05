# 빨간 네모 그리기 (glRectf, )
<img width="20%" alt="image" src="https://github.com/user-attachments/assets/df541e71-3d60-4239-8c38-a5327a6a7d42" /> ← 결과물

```c++
#include <gl/glut.h>
#include <stdio.h>
#include <iostream>
//장면 렌더링
void RenderScene(void) {
	std::cout << "RenderScene" << std::endl;
	//현재 색상을 사용하여 화면을 지운다
	glClear(GL_COLOR_BUFFER_BIT);

	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	glOrtho(-1, 1, -1, 1, -1, 1);
	glMatrixMode(GL_MODELVIEW);
	glLoadIdentity();

	glColor3f(1.0f, 0.0f, 0.0f);
	glRectf(-0.25f, -0.25f, 0.25f, 0.25f);
	//드로잉 명령을 전달한다
	glutSwapBuffers();
}

void SetupRC(void) {
	std::cout << "SetupRC" << std::endl;
	glClearColor(0.0f, 0.0f, 1.0f, 1.0f);
}

int main(int argc, char** argv) {
	glutInit(&argc, argv);
	glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB);
	glutInitWindowSize(640, 480);
	glutInitWindowPosition(400, 400);
	glutCreateWindow("simple");

	SetupRC();
	glutDisplayFunc(RenderScene);

	glutMainLoop();
}
```
## ❔ 오류 ❔ glOrtho(-1, 1, -1, 1, -1, 1) 공간에 정사각형 glRectf(-0.5f, 0.5f, 0.5f, -0.5f);을 그렸는데, 결과는 왜 정사각형이 아니고 직사각형으로 나오는걸까?

<br>  

####  💁‍♀️ 원인 : glutInitWindowSize(640, 480); 내가 강제로 출력창을 직사각형으로 만들었기 때문이다.  
창의 비율 → 640 : 480 = 4: 3   
좌표계는 정사각형 but 창은 직사각형 ∴ 정사각형이 직사각형 창에 맞게 찌그러져서 들어간거임    

<br>

✅ 해결
> glutInitWindowSize(640, 480); → glutInitWindowSize(500, 500); 으로 변경하면 됨  

창을 정사각형으로 맞춘거임  

<br>

✏️ 추가  
> glViewport(GLint x, GLint y, GLsizei width, GLsizei height); 사용해보자

보통 glViewport는 glutInitWindowSize와 동일하게 설정하므로 → glViewport(0, 0, 500, 500)

만약 glutInitWindowSize와 다르게 하면?  
glutInitWindowSize(500, 500); 일 때,  

| glViewport(0, 0, 500, 500)        | <img width="20%" alt="image" src="https://github.com/user-attachments/assets/ff51c5f5-96bb-4d39-b98e-e6c503e57886" />   |  
|:---------------------------------:|:-----------------------------------------------------------------------------------------------------------------------:|  
| glViewport(0, 0, 250, 250);       | <img width="20%" alt="image" src="https://github.com/user-attachments/assets/e1f128ec-97a4-4d32-b99d-c5b3ae38d526" />   |  
| glViewport(100, 100, 300, 300);   | <img width="20%" alt="image" src="https://github.com/user-attachments/assets/d28fa455-70f1-4209-a088-e7454f0ebb96" />   |

<img width="20%" alt="image" src="https://github.com/user-attachments/assets/c8a2c1ab-e281-47aa-8f15-52559f779be5" /> ← 결과물

```c++
#include <gl/glut.h>
#include <stdio.h>
#include <iostream>
//장면 렌더링
void RenderScene(void) {
	std::cout << "RenderScene" << std::endl;
	//현재 색상을 사용하여 화면을 지운다
	glClear(GL_COLOR_BUFFER_BIT);

	glViewport(0, 0, 500, 500);
	// glViewport(0, 0, 250, 250);
	// glViewport(100, 100, 300, 300);

	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	glOrtho(-1, 1, -1, 1, -1, 1);
	glMatrixMode(GL_MODELVIEW);
	glLoadIdentity();

	glColor3f(1.0f, 0.0f, 0.0f);
	glRectf(-0.25f, 0.25f, 0.25f, -0.25f);
	//드로잉 명령을 전달한다
	glutSwapBuffers();
}

void SetupRC(void) {
	std::cout << "SetupRC" << std::endl;
	glClearColor(0.0f, 0.0f, 1.0f, 1.0f);
}

int main(int argc, char** argv) {
	glutInit(&argc, argv);
	glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB);
	glutInitWindowSize(500, 500); // 원래 640, 480 이었음
	glutInitWindowPosition(400, 400);
	glutCreateWindow("simple");

	SetupRC();
	glutDisplayFunc(RenderScene);

	glutMainLoop();
}
```










