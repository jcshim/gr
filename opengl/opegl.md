
### 🎨 우리가 만들고 싶은 것

컴퓨터 화면에 아래처럼 생긴 삼각형을 색칠해서 보여주는 거예요.

```
    🔺(빨강 꼭짓점)
   / \
  /   \
(초록) (파랑)
```

---

### 🧱 이 코드의 역할을 아주 쉽게 나눠볼게요!

#### 1. `#include`와 `#pragma`

```cpp
#include <windows.h>
#include <gl/GL.h>
#pragma comment(lib, "opengl32.lib")
```

* 컴퓨터가 OpenGL(삼각형 그리기 도구)을 사용할 수 있게 준비해주는 코드예요.
* `windows.h`는 윈도우 창을 만드는 마법상자,
* `gl.h`는 그림 그리는 마법붓!
* `#pragma`는 "이걸 꼭 같이 써야 해!"라고 알려주는 것이에요.

---

#### 2. `WndProc` 함수 – 그림을 그리는 마법 상자

```cpp
LRESULT CALLBACK WndProc(HWND h, UINT m, WPARAM w, LPARAM l)
```

* 이 함수는 **"창이 열릴 때", "그림 그릴 때", "창을 닫을 때"** 무엇을 할지 알려줘요.

##### (1) 창이 처음 열릴 때

```cpp
if (m == WM_CREATE) {
  ...
  glClearColor(0.2f, 0.3f, 0.4f, 1);
}
```

* `WM_CREATE`는 "창을 만들었어요!"라는 뜻이에요.
* `glClearColor(...)`는 배경색을 **파란빛 나는 회색**으로 정하는 거예요.

##### (2) 그림 그릴 시간!

```cpp
else if (m == WM_PAINT) {
  ...
  glBegin(GL_TRIANGLES);
  glColor3f(1, 0, 0); glVertex2f(0, 0.5f);    // 빨강 꼭짓점
  glColor3f(0, 1, 0); glVertex2f(-0.5f, -0.5f); // 초록 꼭짓점
  glColor3f(0, 0, 1); glVertex2f(0.5f, -0.5f);  // 파랑 꼭짓점
  glEnd();
  ...
}
```

* 삼각형 그리기 시작! (`glBegin`)
* 꼭짓점 하나하나에 색을 정해주고 위치도 정해줘요.
* `glFlush()`는 “그림 완성했어요!” 하고 보내주는 거예요.
* `SwapBuffers()`는 “이제 화면에 보여줘!”라는 뜻이에요.

##### (3) 창 닫기

```cpp
else if (m == WM_DESTROY) {
  ...
}
```

* 창이 닫히면 마법붓을 정리하고, 프로그램을 끝내요.

---

#### 3. `wWinMain` 함수 – 시작 버튼!

```cpp
int WINAPI wWinMain(...)
```

* 여기서부터 **프로그램이 진짜 시작**해요!
* `"OpenGL"`이라는 이름의 창을 만들고 (`CreateWindowEx`)
* 계속해서 마우스, 키보드 같은 입력을 받으면서, 화면도 갱신해줘요.

---

### 📌 초등학생이 기억하면 좋은 키워드

| 단어           | 쉬운 뜻                                      |
| ------------ | ----------------------------------------- |
| OpenGL       | 컴퓨터에 그림을 그리게 해주는 도구                       |
| 윈도우 창        | 우리가 그림을 볼 수 있는 창문                         |
| 꼭짓점(Vertex)  | 삼각형의 점                                    |
| 색상(Color)    | 빨강, 초록, 파랑 등을 정하는 것                       |
| 메시지(Message) | “창을 만들었어요!”, “그림 그릴 시간이에요!”처럼 컴퓨터가 보내는 신호 |

---

### 💡 더 쉬운 예시로 연습하고 싶다면?

이 코드는 조금 어려운 윈도우 마법들이 많아서, 처음에는 Raylib 같은 더 쉬운 그림 도구를 써보는 것도 좋아요.
(예: `raylib.h`는 한 줄이면 삼각형을 그릴 수 있어요!)

```
#include <windows.h>
#include <gl/GL.h>
#pragma comment(lib, "opengl32.lib")

LRESULT CALLBACK WndProc(HWND h, UINT m, WPARAM w, LPARAM l) {
    static HDC dc; static HGLRC rc;
    if (m == WM_CREATE) {
        PIXELFORMATDESCRIPTOR pfd = { sizeof(pfd),1,PFD_DRAW_TO_WINDOW | PFD_SUPPORT_OPENGL | PFD_DOUBLEBUFFER,PFD_TYPE_RGBA,32 };
        dc = GetDC(h); int pf = ChoosePixelFormat(dc, &pfd);
        SetPixelFormat(dc, pf, &pfd);
        rc = wglCreateContext(dc); wglMakeCurrent(dc, rc);
        glClearColor(0.2f, 0.3f, 0.4f, 1);
    }
    else if (m == WM_PAINT) {
        BeginPaint(h, (PAINTSTRUCT*)&l);
        glClear(GL_COLOR_BUFFER_BIT);
        glBegin(GL_TRIANGLES);
        glColor3f(1, 0, 0); glVertex2f(0, 0.5f);
        glColor3f(0, 1, 0); glVertex2f(-0.5f, -0.5f);
        glColor3f(0, 0, 1); glVertex2f(0.5f, -0.5f);
        glEnd(); glFlush(); SwapBuffers(dc);
        EndPaint(h, (PAINTSTRUCT*)&l);
    }
    else if (m == WM_DESTROY) {
        wglMakeCurrent(0, 0); wglDeleteContext(rc); ReleaseDC(h, dc); PostQuitMessage(0);
    }
    return DefWindowProc(h, m, w, l);
}

int WINAPI wWinMain(HINSTANCE hInst, HINSTANCE, PWSTR, int nCmd) {
    const wchar_t* cls = L"GLWin";
    WNDCLASS wc = { 0 }; wc.lpfnWndProc = WndProc; wc.hInstance = hInst; wc.lpszClassName = cls;
    RegisterClass(&wc);
    HWND w = CreateWindowEx(0, cls, L"OpenGL", WS_OVERLAPPEDWINDOW, 100, 100, 800, 600, 0, 0, hInst, 0);
    ShowWindow(w, nCmd);
    MSG msg;
    while (GetMessage(&msg, 0, 0, 0)) DispatchMessage(&msg);
    return 0;
}
```

![image](https://github.com/user-attachments/assets/daa82a2a-fec8-4161-8023-0719d863e3d2)

