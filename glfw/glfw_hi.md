```
#include <GLFW/glfw3.h>
#include <iostream>

int main() {
    if (!glfwInit()) {
        std::cerr << "GLFW 초기화 실패!" << std::endl;
        return -1;
    }

    glfwWindowHint(GLFW_CLIENT_API, GLFW_NO_API); // Vulkan용
    GLFWwindow* window = glfwCreateWindow(800, 600, "Hello GLFW", nullptr, nullptr);

    while (!glfwWindowShouldClose(window)) {
        glfwPollEvents(); // 입력 처리
    }

    glfwDestroyWindow(window);
    glfwTerminate();
    return 0;
}
```
