#
아래는 **GLFW + OpenGL**을 사용하여 초록색 사각형을 출력하는 
**C++ 전체 예제 코드**입니다. 

주의할 점은 `GLFW`는 Nuget으로 설치
**GLAD** 는 수동 설치 glad.c, glad.h, khrplatform.h 다운로드 및 프로젝트에 삽입

---

### ✅ 예제 코드: 초록색 사각형 출력

```cpp
#pragma comment(lib, "opengl32.lib")
#include <glad.h>  // OpenGL 함수 로더
#include <GLFW/glfw3.h>
#include <iostream>

// 정점 셰이더
const char* vertexShaderSource = R"(
#version 330 core
layout (location = 0) in vec2 aPos;
void main() {
    gl_Position = vec4(aPos, 0.0, 1.0);
}
)";

// 프래그먼트 셰이더 (초록색)
const char* fragmentShaderSource = R"(
#version 330 core
out vec4 FragColor;
void main() {
    FragColor = vec4(0.0, 1.0, 0.0, 1.0); // Green
}
)";

int main() {
    if (!glfwInit()) {
        std::cerr << "GLFW 초기화 실패!" << std::endl;
        return -1;
    }

    // OpenGL 3.3 Core Profile
    glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 3);
    glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 3);
    glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);

    GLFWwindow* window = glfwCreateWindow(800, 600, "초록 사각형", nullptr, nullptr);
    if (!window) {
        std::cerr << "윈도우 생성 실패!" << std::endl;
        glfwTerminate();
        return -1;
    }
    glfwMakeContextCurrent(window);

    // GLAD 초기화
    if (!gladLoadGLLoader((GLADloadproc)glfwGetProcAddress)) {
        std::cerr << "GLAD 초기화 실패!" << std::endl;
        return -1;
    }

    // 셰이더 컴파일
    GLuint vertexShader = glCreateShader(GL_VERTEX_SHADER);
    glShaderSource(vertexShader, 1, &vertexShaderSource, nullptr);
    glCompileShader(vertexShader);

    GLuint fragmentShader = glCreateShader(GL_FRAGMENT_SHADER);
    glShaderSource(fragmentShader, 1, &fragmentShaderSource, nullptr);
    glCompileShader(fragmentShader);

    // 셰이더 프로그램 연결
    GLuint shaderProgram = glCreateProgram();
    glAttachShader(shaderProgram, vertexShader);
    glAttachShader(shaderProgram, fragmentShader);
    glLinkProgram(shaderProgram);

    glDeleteShader(vertexShader);
    glDeleteShader(fragmentShader);

    // 사각형 정점 데이터 (2개의 삼각형으로 구성)
    float vertices[] = {
        -0.5f,  0.5f, // 왼쪽 위
        -0.5f, -0.5f, // 왼쪽 아래
         0.5f, -0.5f, // 오른쪽 아래

        -0.5f,  0.5f, // 왼쪽 위
         0.5f, -0.5f, // 오른쪽 아래
         0.5f,  0.5f  // 오른쪽 위
    };

    GLuint VAO, VBO;
    glGenVertexArrays(1, &VAO);
    glGenBuffers(1, &VBO);

    glBindVertexArray(VAO);
    glBindBuffer(GL_ARRAY_BUFFER, VBO);
    glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);

    // 정점 속성 설정
    glVertexAttribPointer(0, 2, GL_FLOAT, GL_FALSE, 2 * sizeof(float), (void*)0);
    glEnableVertexAttribArray(0);

    // 렌더링 루프
    while (!glfwWindowShouldClose(window)) {
        glfwPollEvents();

        glClearColor(0.2f, 0.2f, 0.2f, 1.0f); // 배경색 (회색)
        glClear(GL_COLOR_BUFFER_BIT);

        glUseProgram(shaderProgram);
        glBindVertexArray(VAO);
        glDrawArrays(GL_TRIANGLES, 0, 6);

        glfwSwapBuffers(window);
    }

    // 정리
    glDeleteVertexArrays(1, &VAO);
    glDeleteBuffers(1, &VBO);
    glDeleteProgram(shaderProgram);

    glfwDestroyWindow(window);
    glfwTerminate();
    return 0;
}
```

---

### ✅ 컴파일 방법 (Windows 기준)

1. **GLFW**와 **GLAD**를 설치해야 합니다.

   * GLFW: Nuget에서 GLFW로 검색 또는 `vcpkg install glfw3`
   * GLAD: [https://glad.dav1d.de/](https://glad.dav1d.de/)에서 `OpenGL 3.3`, `Core` 프로필 선택 후 다운로드
2. Visual Studio에서:
   * GLAD 헤더와 `.c` 파일 프로젝트에 추가
  
![image](https://github.com/user-attachments/assets/fb32d297-fa61-496c-8e5b-7e401bd675ef)
