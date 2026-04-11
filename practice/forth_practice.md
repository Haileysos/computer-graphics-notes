# 아래 조건들을 준수하여 아래 그림대로 출력하라  
- glRectf(-0.25f, 0.25f, 0.25f, -0.25f) 으로 fix
- glutInitWindowSize(500, 500); 으로 fix
- glOrtho(-1, 1, -1, 1, -1, 1); 으로 fix
- glViewport()만 수정해야 함

<img width="20%" alt="image" src="https://github.com/user-attachments/assets/209dfff8-aa3a-477e-8440-bc601a831b5d" /> ← 결과물  

<table>
  <tr>
    <td width=40%>
      <img width="100%" alt="image" src="https://github.com/user-attachments/assets/2ec3e03c-e0ca-44a8-9719-f2a55598e57e" />
    </td>
    <td>
		  💛 windowsize → 500 x 500 <br><br>
		  🤍 ortho → -1, 1, -1, 1, -1, 1 <br><br>
		  ❤️‍🔥 rect → -0.25, 0.25, 0.25, -0.25 <br><br>
      오잉 근데 그림에서는 왜 정사각형이 아니고, 사각형이 직사각으로 찌그러져있지? 그리고 가운데에 위치하지도 않네?!!?!
    </td>
  </tr>
  <tr>
    <td width=40%>
      <img width="100%" alt="image" src="https://github.com/user-attachments/assets/298ada86-9fbc-42b7-b97b-cceb477e254c" />
    </td>
    <td>
      💜 viewport → 0, 0, 250, 500 <br><br>
      실제 그림을 그리는 도화지(viewport)가 윈도우의 절반 왼쪽으로 되어있어서 정사각형이 찌그러져 있던 것!!
    </td>
  </tr>
</table>



을 수정하여 다름 출력을 만드시오
```c++
#include <gl/glut.h>
#include <stdio.h>
#include <iostream>

void RenderScene(void) {

	std::cout << "RenderScene" << std::endl;

	int sizeA = 200;
	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	glViewport(0, 0, 250, 500); // ★ //
	glOrtho(-1, 1, -1, 1, -1, 1); // fixed
	glMatrixMode(GL_MODELVIEW);
	glLoadIdentity();

	glClear(GL_COLOR_BUFFER_BIT);
	glColor3f(1.0f, 0.0f, 0.0f);
	glRectf(-0.25f, 0.25f, 0.25f, -0.25f); // fixed

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
	glutInitWindowPosition(0, 0);
	glutCreateWindow("simple");

	glutDisplayFunc(RenderScene);
	SetupRC();

	glutMainLoop();
}

```
<br><br><br>
