# 아래 조건들을 준수하여 아래 그림대로 출력하라  
- glutInitWindowSize(640,480) 으로 fix
- viewport는 windowsize와 동일
- glRectf(0,240,320,0)으로 fix
- glOrtho()만 수정해야 함
- 화면에 출력되는 빨간색 사각형의 실제 크기도 glRectf(0,240,320,0)와 같아야 함
  
  <img width="20%" alt="image" src="https://github.com/user-attachments/assets/6f05954d-32ff-40f6-85ab-78bfdc5220ca" /> ← 결과물    

<table>
  <tr>
    <td width=40%>
      <img width="100%" alt="1" src="https://github.com/user-attachments/assets/d401271e-07c0-4bc0-8aa1-f12c4d8f0c59" />
    </td>
    <td>
		💛 glutInitWindowSize(640,480) fixed <br><br>
		💜 viewport는 windowsize와 동일<br>
		　　→ 0, 0, 640, 480 <br><br>
		❤️‍🔥 glRectf(0,240,320,0) fixed <br>
		　　→ (0, 240), (320, 0)을 꼭짓점으로 하는 사각형 <br><br>
		🤍 ∴ ortho → -320, 320, -240, 240, -1, 1 <br><br>
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
	glViewport(0, 0, 640, 480); // window size 와 동일

	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	glOrtho(-320, 320, -240, 240, -1, 1); 
	glMatrixMode(GL_MODELVIEW);
	glLoadIdentity();

	glColor3f(1.0f, 0.0f, 0.0f);
	glRectf(0, 240, 320, 0); // fixed

	glutSwapBuffers();
}

void SetupRC(void) {
	std::cout << "SetupRC" << std::endl;
	glClearColor(0.0f, 0.0f, 1.0f, 1.0f);
}

int main(int argc, char** argv) {
	glutInit(&argc, argv);
	glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB);
	glutInitWindowSize(640, 480); // fixed
	glutInitWindowPosition(500, 500);
	glutCreateWindow("simple");

	SetupRC();
	glutDisplayFunc(RenderScene);

	glutMainLoop();
}
```
