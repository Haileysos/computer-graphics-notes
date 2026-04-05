# 아래 조건들을 준수하여 오른쪽 그림대로 출력되도록 코딩해라  
- glutInitWindowSize(640,480) 으로 fix
- viewport는 windowsize와 동일
- glRectf(0,240,320,0)으로 fix
- glOrtho()만 수정해야 함
- 화면에 출력되는 빨간색 사각형의 실제 크기도 glRectf(0,240,320,0)와 같아야 함

glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB);
glutInitWindowSize(640,480);
glutInitWindowPosition(500,500) 
glutCreateWindow("simple")


정답코드
```c++
#include <gl/glut.h>
#include <stdio.h>
#include <iostream>

void RenderScene(void) {

	std::cout << "RenderScene" << std::endl;

	glClear(GL_COLOR_BUFFER_BIT);

	int sizeA = 200;
	glViewport(0, 0, 640, 480);

	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	glOrtho(-320, 320, -240, 240, -1, 1); // 실제 화면에 보이는 이미지의 
	glMatrixMode(GL_MODELVIEW);
	glLoadIdentity();

	glColor3f(1.0f, 0.0f, 0.0f);
	glRectf(0, 240, 320, 0);

	glutSwapBuffers();
}

void SetupRC(void) {
	std::cout << "SetupRC" << std::endl;
	glClearColor(0.0f, 0.0f, 1.0f, 1.0f); // 화면을 지울 색상을 파랑으로 설정
}

int main(int argc, char** argv) {
	glutInit(&argc, argv);
	glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB);
	glutInitWindowSize(640, 480); // window size 는 640, 480 으로 fix
	glutInitWindowPosition(500, 500);
	glutCreateWindow("simple");

	glutDisplayFunc(RenderScene);

	glutMainLoop();
}
```
