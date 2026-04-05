# glutInitWindowSize(500,500), glViewport(0,0,500,500)의 값은 fix 시키고 다음과 같은 크기의 정사각형 그리기  
# 한 변의 길이가 창 한 변의 길이의 1/4인 정사각형 그리기  
<img width="20%" alt="image" src="https://github.com/user-attachments/assets/5618f0c2-7bb7-4ad9-8197-90c86f2cb8cc" /> ← 결과물  
<table>
  <tr>
    <td width=40%>
      <img width="100%" alt="1" src="https://github.com/user-attachments/assets/386fdb6b-bfaa-44e1-85ba-9a97dbb29c2a" />
    </td>
    <td>
		💛 windowsize → 500 x 500 <br><br>
		💜 viewport → 0, 0, 500, 500 <br><br>
		🤍 ortho → -1, 1, -1, 1, -1, 1 <br><br>
		　　∴ 창의 한 변의 길이 = 2 <br><br>
		❤️ 정사각형의 한 변의 길이 = 창 한 변의 길이 x 1/4 = 0.5 <br><br>
		❤️‍🔥 ∴ Rect → -0.25, -0.25, 0.25, 0.25 <br>
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

	glViewport(0, 0, 500, 500); // fixed

	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	glOrtho(-1, 1, -1, 1, -1, 1);
	glMatrixMode(GL_MODELVIEW);
	glLoadIdentity();

	glColor3f(1.0f, 0.0f, 0.0f);
	glRectf(-0.25f, -0.25f, 0.25f, 0.25f);

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
	glutInitWindowPosition(400, 400);
	glutCreateWindow("simple");

	SetupRC();
	glutDisplayFunc(RenderScene);

	glutMainLoop();
}
```
