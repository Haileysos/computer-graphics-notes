# 아래 조건들을 준수하여 아래 그림대로 출력하라  
- glutInitWindowSize(500, 500); 으로 fix
- glViewport(0, 0, 500, 500); 으로 fix
- glOrtho(0, 500, 0, 500, -1, 1); 으로 fix
- glRectf()만 수정해야 함

  <img width="20%" alt="image" src="https://github.com/user-attachments/assets/a941d609-f85f-4214-b339-6db93d75879f" /> ← 결과물

<table>
  <tr>
    <td width=40%>
      <img width="100%" alt="image" src="https://github.com/user-attachments/assets/c1879e2a-aa72-4ab5-81d4-48754fda6427" />
    </td>
    <td>
		    🤍 빨간 사각형이 (250,250) (250,375) (375,250) (375,375) 꼭짓점으로 이루어져 있음<br>
     　　∴ Rectf → (250, 375) (375, 250) or (250, 250) (375, 375)
    </td>
  </tr>
</table>

```c++

#include <gl/glut.h>
#include <stdio.h>
#include <iostream>

void RenderScene(void) {

	std::cout << "RenderScene" << std::endl;

	glClear(GL_COLOR_BUFFER_BIT);

	int sizeA = 200;
	glViewport(0, 0, 500, 500); // fixed

	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	glOrtho(0, 500, 0, 500, -1, 1); // fixed
	glMatrixMode(GL_MODELVIEW);
	glLoadIdentity();

	glColor3f(1.0f, 0.0f, 0.0f);
	glRectf(250, 375, 375, 250); //	or glRectf(250, 250, 375, 375); 

	glutSwapBuffers();
}

void SetupRC(void) {
	std::cout << "SetupRC" << std::endl;
	glClearColor(0.0f, 0.0f, 1.0f, 1.0f);
}

int main(int argc, char** argv) {
	glutInit(&argc, argv);
	glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB);
	glutInitWindowSize(500, 500); // fixed
	glutInitWindowPosition(500, 500);
	glutCreateWindow("simple");

	SetupRC();
	glutDisplayFunc(RenderScene);

	glutMainLoop();
}
```
