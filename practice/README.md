```c++
// 파란색으로 채워진 창 출력하기
#include<GL/glut.h>
#include<stdio.h>
#include<iostream>

//장면 렌더링
void RenderScene(void){
	std::cout << "RenderScene" << std::endl;
	//현재 색상을 사용하여 화면을 지운다
	glClear(GL_COLOR_BUFFER_BIT);
	//드로잉 명령을 전달한다
	//glFlush();
 	glutSwapBuffers();
}

void SetupRC(void){
	std::cout << "SetupRC" << std::endl;
	glClearColor(0.0f, 0.0f, 1.0f, 1.0f);
}

int main(int argc, char** argv){
	glutInit(&argc, argv);
	glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB); // GLUT_SINGLE
	glutInitWindowSize(640, 480);
	glutInitWindowPosition(100, 100);
	glutCreateWindow("simple");

	SetupRC();
	glutDisplayFunc(RenderScene);

	glutMainLoop();
}
```

## ❔ 오류 ❔ 출력창 초기 실행 시, 검정/흰 화면만 출력 (초기샛팅값=파란색 임에도 불구하고)  

<br>  

####  💁‍♀️ 가정 : GPU 혹은 OS종류 및 버전에 따라 더블 버퍼를 기본값으로 사용하는 경우  

<br>

✅ 해결  

본인은 더블 버퍼가 기본값인 경우 임  

> glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB);  →  glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB);  

또, 더블 버퍼에서는 glFlush(); 대신에 glutSwapBuffers(); 를 사용함  

> glFlush();  →  glutSwapBuffers();  

<br>

✏️ 참고  

만약, 싱글 버퍼가 기본값인 경우,  

> glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB); 와 glFinish(); 를 씀
