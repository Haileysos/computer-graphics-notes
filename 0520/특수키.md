
0519-3.cpp 에서는 일반키(adwx)로 좌우위아래 움직이게 한 것

0520.cpp 에서는 특수키로 회전시키는 거 할게여
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
```c++
void RenderScene(void) {
    ....
	glPushMatrix();

	glRotatef(xRot, 1.0f, 0.0f, 0.0f);
	glRotatef(yRot, 0.0f, 1.0f, 0.0f);

 	glPopMatrix();
```
```c++
int main(int argc, char** argv) {
	....
	glutSpecialFunc(SpecialKey); // 특수키
}
```
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

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
