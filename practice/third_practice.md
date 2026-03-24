# View(2-2-2) glutInitWindowSize(500,500), glViewport(0,0,500,500)의 값은 fix 시키고 다음과 같은 크기의 정사각형 그리기  
# 한 변의 길이가 창 한 변의 길이의 1/4인 정사각형 그리기  
<img width="20%" alt="image" src="https://github.com/user-attachments/assets/5618f0c2-7bb7-4ad9-8197-90c86f2cb8cc" /> ← 결과물  

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
	glutInitWindowSize(500, 500);
	glutInitWindowPosition(400, 400);
	glutCreateWindow("simple");

	SetupRC();
	glutDisplayFunc(RenderScene);

	glutMainLoop();
}
```
