



	glMatrixMode(GL_PROJECTION); -> 카메라/뷰포트 설정
좌표값이 3개 존재한다 1.월드좌표 2. 카메라좌표(카메라가잇어야할위치를알려주는) 3. 오브젝트의좌ㅊ표(우리가 그리는 오브젝트)
3d좌표를 2d화면에 매핑하는과정
glOrtho(), gluPerspective()등을 사용하여 카메라의 시야(FOV)설정
	glMatrixMode(GL_MODELVIEW); ->객체변환 (이동,회전,크기변경)
glTranslatef(), glRotatef(), glScalef() 등을 사용하여 모델(도형)의 위치및크기변환

->일반적으로 투영 행렬(GL_PROJECTION) 을 먼저 설정한 후, 모델뷰 핼ㅇ렬(GL_MODELVIEW)을 설정
-> 일반적으로 glutReshapeFunc()에 적용 <<근데 우리는 일단 이거 씀glutDisplayFunc(RenderScene);

glOrtho(-1,1,-1,1,-1,1)
카메라뷰
(left, right, bottom, top, near, far) 순서 ★외워야함
near < far <<항상 near보다 far가 값이 커야함>>
