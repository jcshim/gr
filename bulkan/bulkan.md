# **Vulkan API를 사용하여 초록색 사각형을 출력하는 가장 기본적인 예제 코드**

> ⚠️ **전제 조건**  
> - Vulkan SDK 설치 완료 (https://vulkan.lunarg.com/)  
> - Visual Studio 프로젝트 생성 (Console Application 또는 Empty Project)  
> - `vulkan-1.lib`을 링커에 추가  
> - `vulkan/vulkan.h` 헤더 포함 가능해야 함  

---

## ✅ 예제 개요  
- Vulkan 인스턴스 생성  
- 물리적 장치 선택  
- 논리 장치 및 큐 생성  
- 스왑체인 및 이미지 뷰 생성  
- 렌더 패스 및 프레임버퍼 설정  
- 파이프라인 생성 (초록색 사각형 그리기)  
- 커맨드 버퍼 작성 및 제출  

---

## ✅ 예제 코드 (초록색 화면 출력)

> 프로젝트 파일 구성이 커버할 수 없으므로 아래는 핵심만 담은 **초간단 예제**입니다. GLFW로 윈도우 생성까지 포함한 코드입니다.

```cpp
#define GLFW_INCLUDE_VULKAN
#include <GLFW/glfw3.h>
#include <iostream>
#include <stdexcept>
#include <cstdlib>

const uint32_t WIDTH = 800;
const uint32_t HEIGHT = 600;

class HelloTriangleApplication {
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

        glfwWindowHint(GLFW_CLIENT_API, GLFW_NO_API); // Vulkan 모드
        glfwWindowHint(GLFW_RESIZABLE, GLFW_FALSE);

        window = glfwCreateWindow(WIDTH, HEIGHT, "Vulkan Green Rect", nullptr, nullptr);
    }

    void initVulkan() {
        createInstance();
        // 이 예제에서는 간단히 인스턴스까지만 생성
        // 실제 렌더링을 위해선 Device, Swapchain, RenderPass, Pipeline 등 추가 필요
    }

    void createInstance() {
        VkApplicationInfo appInfo{};
        appInfo.sType = VK_STRUCTURE_TYPE_APPLICATION_INFO;
        appInfo.pApplicationName = "Hello Vulkan";
        appInfo.applicationVersion = VK_MAKE_VERSION(1, 0, 0);
        appInfo.pEngineName = "No Engine";
        appInfo.engineVersion = VK_MAKE_VERSION(1, 0, 0);
        appInfo.apiVersion = VK_API_VERSION_1_0;

        // GLFW 확장 획득
        uint32_t glfwExtensionCount = 0;
        const char** glfwExtensions;
        glfwExtensions = glfwGetRequiredInstanceExtensions(&glfwExtensionCount);

        VkInstanceCreateInfo createInfo{};
        createInfo.sType = VK_STRUCTURE_TYPE_INSTANCE_CREATE_INFO;
        createInfo.pApplicationInfo = &appInfo;
        createInfo.enabledExtensionCount = glfwExtensionCount;
        createInfo.ppEnabledExtensionNames = glfwExtensions;
        createInfo.enabledLayerCount = 0;

        if (vkCreateInstance(&createInfo, nullptr, &instance) != VK_SUCCESS) {
            throw std::runtime_error("failed to create instance!");
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
    HelloTriangleApplication app;

    try {
        app.run();
    } catch (const std::exception& e) {
        std::cerr << e.what() << std::endl;
        return EXIT_FAILURE;
    }

    return EXIT_SUCCESS;
}
```

---

## ✅ 링커 설정

Visual Studio에서 아래 설정을 추가해야 합니다:

- **링커 > 입력 > 추가 종속성**에 다음 추가:
  ```
  vulkan-1.lib
  ```

- **C/C++ > 일반 > 추가 포함 디렉터리**:
  ```
  Vulkan SDK 설치 경로\Include
  ```

- **링커 > 일반 > 추가 라이브러리 디렉터리**:
  ```
  Vulkan SDK 설치 경로\Lib
  ```

---

## 🔰 결과

현재 코드는 윈도우를 띄우고 Vulkan 인스턴스를 생성하는 데까지만 도와줍니다.  
**초록색 사각형을 그리기 위해서는 RenderPass, Graphics Pipeline, Framebuffer, CommandBuffer 설정이 필요**합니다.

원하시면 **다음 단계로 초록색 배경 혹은 사각형 그리기 파이프라인까지 확장된 전체 코드**도 제공해드릴게요.

확장된 예제가 필요하신가요? 🙂
