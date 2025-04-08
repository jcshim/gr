# **Visual Studio에서 Vulkan으로 삼각형을 출력하기

---

## ✅ 1단계: Vulkan SDK 설치

1. [https://vulkan.lunarg.com/sdk/home](https://vulkan.lunarg.com/sdk/home) 접속
2. 자신의 Windows 버전에 맞는 SDK 다운로드 및 설치
3. 설치 후 **환경 변수(VULKAN_SDK)**가 자동 설정됨

---

## ✅ 2단계: Visual Studio 프로젝트 생성

1. Visual Studio 실행 → `콘솔 애플리케이션(C++)` 새 프로젝트 생성
2. 이름 예: `vk1`

---

## ✅ 3단계: NuGet으로 GLFW 설치
1. Visual Studio ** 프로젝트 > NuGet 패키지 관리자 > 찿아보기 > glfw ** 설치하기

---

## ✅ 4단계: 코드 추가

`main.cpp`에 다음 템플릿 코드 붙여넣기 (Vulkan 초기화 및 창 생성까지)

```cpp
#define GLFW_INCLUDE_VULKAN
#include <GLFW/glfw3.h>
#include <iostream>

int main() {
    glfwInit();
    glfwWindowHint(GLFW_CLIENT_API, GLFW_NO_API);

    GLFWwindow* window = glfwCreateWindow(800, 600, "Vulkan Window", nullptr, nullptr);

    while (!glfwWindowShouldClose(window)) {
        glfwPollEvents();
    }

    glfwDestroyWindow(window);
    glfwTerminate();
    return 0;
}
```

🟡 위 코드는 창만 생성합니다. Vulkan 초기화 + 삼각형 출력은 다음 단계에서 추가!

---
## Visual Studio에서 shaders 폴더를 만들고 그 속에 다음 2개의 파일(shader.vert, shader.frag)을 생성한다. 

## ✅ 5단계: 쉐이더 준비 (.vert / .frag)

예시:
```glsl
// shader.vert
#version 450

layout(location = 0) out vec3 fragColor;

vec2 positions[3] = vec2[](
    vec2(0.0, -0.5),
    vec2(0.5, 0.5),
    vec2(-0.5, 0.5)
);

vec3 colors[3] = vec3[](
    vec3(1.0, 0.0, 0.0),
    vec3(0.0, 1.0, 0.0),
    vec3(0.0, 0.0, 1.0)
);

void main() {
    gl_Position = vec4(positions[gl_VertexIndex], 0.0, 1.0);
    fragColor = colors[gl_VertexIndex];
}
```

```glsl
// shader.frag
#version 450

layout(location = 0) in vec3 fragColor;

layout(location = 0) out vec4 outColor;

void main() {
    outColor = vec4(fragColor, 1.0);
}
```

---

## ✅ 6단계: 쉐이더 SPIR-V 컴파일

1. `glslc`는 Vulkan SDK에 포함됨
2. 명령어 (cmd에서 실행):

```bash
glslc shader.vert -o vert.spv
glslc shader.frag -o frag.spv
```

---

## ✅ 7단계: 삼각형 그리는 전체 코드 복사하여 추가

### **[삼각형을 실제로 그리는 전체 코드](https://vulkan-tutorial.com/code/17_swap_chain_recreation.cpp)**

---

## ✅ 8단계: Visual Studio 버전 바꾸기

속성 페이지 > 구성 속성 > C/C++ > 언어 > C++ 언어 표준
→ [ ISO C++17 표준 (/std:c++17) ] 이상 버전을 선택

![image](https://github.com/user-attachments/assets/db34f616-bd12-4b3b-ac23-88b3d1474841)

