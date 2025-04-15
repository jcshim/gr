# Windows에서 Visual Studio로 Vulkan 무지게삼각형 그리기
### ✅ 1. Vulkan SDK 설치: https://vulkan.lunarg.com/ 환경변수(`VULKAN_SDK`)설정 됨 
### ✅ 2. Visual Studio 콘솔 프로젝트 생성 
### ✅ 3. NuGet으로 GLFW 설치 (창 생성용): 도구 > NuGet 패키지 관리자 > 찾아보기 탭 < **glfw**
### ✅ 4. 프로젝트 속성 설정
1. `C/C++ > 일반 > 추가 포함 디렉터리`에 다음 추가: **$(VULKAN_SDK)\Include**
2. `링커 > 일반 > 추가 라이브러리 디렉터리`에 다음 추가: **$(VULKAN_SDK)\Lib**
3. `링커 > 입력 > 추가 종속성`에 다음 추가: **vulkan-1.lib**
### ✅ 5. [삼각형 출력 코드 작성](https://docs.vulkan.org/tutorial/latest/_attachments/16_frames_in_flight.cpp)
## .\shaders 폴더를 만든다. 
1. .\shaders\ [shader.vert](https://vulkan-tutorial.com/code/09_shader_base.vert) 작성
2. .\shaders\ [shader.frag](https://vulkan-tutorial.com/code/09_shader_base.frag) 작성
3. cd .\shaders\ 및 컴파일 하기
4. C:/VulkanSDK/1.4.309.0/Bin/glslc.exe shader.vert -o vert.spv
5. C:/VulkanSDK/1.4.309.0/Bin/glslc.exe shader.frag -o frag.spv

## <p>$\it{\large{\color{#DD6565}오류 해결방안 / **VS 17** 이상을 설정해야 함.}}$</p>
프로젝트 > 속성 > 구성 속성 > 일반 > 플랫폼 도구 집합 > **Visual Studio 2022 (v143)** 선택

## 프로젝트 속성 변경하기 (프람프트창 없애기)
1. 프로젝트 > 속성> 링커 > 시스템 > 하위 시스템 Windows (/SUBSYSTEM:WINDOWS)
2. 프로젝트 > 속성> 링커 > 고급 > 진입점(엔트리 지점) mainCRTStartup
