## ✅ Visual Studio 설정 전제
- **Vulkan SDK 설치:** [https://vulkan.lunarg.com/](https://vulkan.lunarg.com/)
- 설치 후, **환경변수(VULKAN_SDK)**가 자동 설정됩니다.
- Visual Studio 프로젝트 속성:
  - `C/C++ > 일반 > 추가 포함 디렉터리`: `$(VULKAN_SDK)\Include`
  - `링커 > 일반 > 추가 라이브러리 디렉터리`: `$(VULKAN_SDK)\Lib`
  - `링커 > 입력 > 추가 종속성`: `vulkan-1.lib`

---

## 🧾 main.cpp 예제 코드 (초록색 Clear)

```cpp
#define GLFW_INCLUDE_VULKAN
#include <GLFW/glfw3.h>
#include <iostream>
#include <stdexcept>
#include <cstdlib>
#include <vector>

const uint32_t WIDTH = 800;
const uint32_t HEIGHT = 600;

class HelloVulkanApp {
public:
    void run() {
        initWindow();
        initVulkan();
        mainLoop();
        cleanup();
    }

private:
    GLFWwindow* window;
    VkInstance instance;

    void initWindow() {
        glfwInit();
        glfwWindowHint(GLFW_CLIENT_API, GLFW_NO_API); // Vulkan only
        window = glfwCreateWindow(WIDTH, HEIGHT, "Vulkan Window", nullptr, nullptr);
    }

    void initVulkan() {
        createInstance();
    }

    void createInstance() {
        VkApplicationInfo appInfo{};
        appInfo.sType = VK_STRUCTURE_TYPE_APPLICATION_INFO;
        appInfo.pApplicationName = "Hello Vulkan";
        appInfo.applicationVersion = VK_MAKE_VERSION(1, 0, 0);
        appInfo.pEngineName = "No Engine";
        appInfo.engineVersion = VK_MAKE_VERSION(1, 0, 0);
        appInfo.apiVersion = VK_API_VERSION_1_0;

        uint32_t glfwExtensionCount = 0;
        const char** glfwExtensions = glfwGetRequiredInstanceExtensions(&glfwExtensionCount);

        VkInstanceCreateInfo createInfo{};
        createInfo.sType = VK_STRUCTURE_TYPE_INSTANCE_CREATE_INFO;
        createInfo.pApplicationInfo = &appInfo;
        createInfo.enabledExtensionCount = glfwExtensionCount;
        createInfo.ppEnabledExtensionNames = glfwExtensions;
        createInfo.enabledLayerCount = 0;

        if (vkCreateInstance(&createInfo, nullptr, &instance) != VK_SUCCESS) {
            throw std::runtime_error("failed to create Vulkan instance!");
        }
    }

    void mainLoop() {
        while (!glfwWindowShouldClose(window)) {
            glfwPollEvents();
        }
    }

    void cleanup() {
        vkDestroyInstance(instance, nullptr);
        glfwDestroyWindow(window);
        glfwTerminate();
    }
};

int main() {
    HelloVulkanApp app;
    try {
        app.run();
    } catch (const std::exception& e) {
        std::cerr << "오류: " << e.what() << std::endl;
        return EXIT_FAILURE;
    }
    return EXIT_SUCCESS;
}
```

---

## 🚀 이 코드를 실행하면?
- Vulkan을 초기화하고 GLFW로 창을 생성합니다.
- 아직 스왑체인이나 렌더 패스 없이 기본 인스턴스만 생성합니다.
- 실제 초록색 Clear는 다음 단계에서 렌더 패스와 커맨드 버퍼 추가 후 가능합니다.

---

## ✅ 다음 단계 원하시나요?
- 스왑체인 구성 + 커맨드 버퍼 → **초록색 배경 Clear**
- 삼각형 렌더링
- 쉐이더 추가 등

필요하신 수준에 맞춰 단계적으로 확장해드릴게요.  
**어디까지 구현하고 싶으신가요? (예: 배경 색상, 삼각형, 쉐이더 포함 등)**
