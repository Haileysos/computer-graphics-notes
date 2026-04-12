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

void ChangeSize(GLsizei w, GLsizei h) { // 1 

	GLint wSize = 100; // 2
	GLfloat aspectRatio; // 3

	if (h == 0) // 4
		h = 1;

	glViewport(0, 0, w, h); // 5 

	glMatrixMode(GL_PROJECTION); // 6
	glLoadIdentity(); // 7

	// (left, right, bottom, top, near, far)
	aspectRatio = (GLfloat)w / (GLfloat)h; // 8
	if (w <= h) // 9
		glOrtho(-wSize, wSize, -wSize / aspectRatio, wSize / aspectRatio, -1, 1); // 10
	else // 11
		glOrtho(-wSize * aspectRatio, wSize * aspectRatio, -wSize, wSize, -1, 1); // 12

	glMatrixMode(GL_MODELVIEW); // 13
	glLoadIdentity(); // 14
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

|   |   |
|---|---|
| 켜자마자 | <img width="20%" alt="image" src="https://github.com/user-attachments/assets/198e23a0-3586-4da0-8236-18eb451a8f71" /> |
| 가로로 늘리면? | <img width="40%" alt="image" src="https://github.com/user-attachments/assets/23748f54-1915-4ae7-a6d3-4794c345276a" /> |
| 세로로 늘리면? | <img width="20%" alt="image" src="https://github.com/user-attachments/assets/0435d1b6-640c-46f4-8bae-19788eab48f9" /> |

<br><br><br>
