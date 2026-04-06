
fixed
- glRectf(-0.25f, 0.25f, 0.25f, -0.25f)
- glutInitWindowSize(500, 500); 
- glOrtho(-1, 1, -1, 1, -1, 1); 
glViewport()을 수정하여 다름 출력을 만드시오

0331-3.cpp
glViewport(x, y, width, height);
정답은
glViewport(0, 0, 250, 500); 
