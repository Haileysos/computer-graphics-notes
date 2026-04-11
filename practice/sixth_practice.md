# 창 크기 변화에 따른 모델 비율 유지  
- 내가 창 크기를 바꿔도 빨간 사각형이 비율을 유지를 해야함
- how?
- glOrtho()를 잘 컨트롤 하면,,,
- glViewport는 창 크기와 동일하게 함  



```c++
#include <gl/glut.h>
#include <stdio.h>
#include <iostream>

void RenderScene(void) {

	std::cout << "RenderScene" << std::endl;

	glClear(GL_COLOR_BUFFER_BIT);
	glColor3f(1.0f, 0.0f, 0.0f);
	glRectf(-0.25f, 0.25f, 0.25f, -0.25f); 

	glutSwapBuffers();
}

// ChangeSize 함수 추가!!!
void ChangeSize(GLsizei w, GLsizei h) {

	GLint wSize = 100;
	GLfloat aspectRatio;

	if (h == 0)
		h = 1;

	glViewport(0, 0, w, h);

	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();

	// (left, right, bottom, top, near, far)
	aspectRatio = (GLfloat)w / (GLfloat)h;
	if (w <= h)
		glOrtho(-wSize, wSize, -wSize / aspectRatio, wSize / aspectRatio, -1, 1);
	else
		glOrtho(-wSize * aspectRatio, wSize * aspectRatio, -wSize, wSize, -1, 1);

	glMatrixMode(GL_MODELVIEW);
	glLoadIdentity();
}

void SetupRC(void) {
	std::cout << "SetupRC" << std::endl;
	glClearColor(0.0f, 0.0f, 1.0f, 1.0f);
}

int main(int argc, char** argv) {
	glutInit(&argc, argv);
	glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB);
	glutInitWindowSize(500, 500); // fixed
	glutInitWindowPosition(400, 400);
	glutCreateWindow("simple");

	glutDisplayFunc(RenderScene);
	glutReshapeFunc(ChangeSize); // 추가!!!

	SetupRC();

	glutMainLoop();
}

```
<br><br><br>
