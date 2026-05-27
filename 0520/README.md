
0519-3.cpp 에서는 일반키(adwx)로 좌우위아래 움직이게 한 것

0520.cpp 에서는 특수키 할게여
```c++
GLfloat xRot = 0.0f;
GLfloat yRot = 0.0f;

void SpecialKey(int key, int x, int y) {

	if (key == GLUT_KEY_UP)
		xRot -= 2.0f;
	if (key == GLUT_KEY_DOWN)
		xRot += 2.0f;
	if (key == GLUT_KEY_LEFT)
		yRot -= 2.0f;
	if (key == GLUT_KEY_RIGHT)
		yRot += 2.0f;

	if (xRot > 360.0f)
		xRot -= 360.0f;
	if (xRot < 0.0f)
		xRot += 360.0f;
	if (yRot > 360.0f)
		yRot -= 360.0f;
	if (yRot < 0.0f)
		yRot += 360.0f;

	glutPostRedisplay();
}
```
	glPushMatrix();

	glTranslatef(xTran, yTran, 0.0f);
  glPopMatrix();
```c++
```

int main에 추가하기
```c++
glutSpecialFunc(SpecialKey); // 특수키
```

ㅡㅡ
그린 원을 앞면과 뒷면의 색을 다르게 만들어 보자 (각자알아서 해보기)
ㅡㅡ
솔리드 물체 (원뿔 그리기)
 
원뿔 그리시오 
키보드 조작으로 rotation되어야 함 
- glBegin(GL_TRIANGLE_FAN) 사용 ●
- # define GL_PI 3.1415f 사용 ●
- glEnable(GL_CULL_FACE)사용 ●
- 카메라 위치와 방향은 기본 값
- 16개 조각


학번.cpp 파일로 제출


	if (bCull)
		glEnable(GL_CULL_FACE);
	else
		glDisable(GL_CULL_FACE);




밑면은 


여기서 원뿔을 그리는 게 과제야.
내 아이디어는 z축의 - 방향(x,y 는 0,0인)에 점을 찍으면 원뿔이 만들어진다고 생각

rotation 하면 뒤로 가려지는 부분은 안보여야 하는데 지금 그런거 상관없이 계속 모든 면이 보여서 이게 3d원뿔처럼 안느껴지는게 문제야 해결해줘

다시 처음으로 돌아가서.
