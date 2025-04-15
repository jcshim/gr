
## 🎨 Shaders란?
**쉐이더(Shader)** 는 GPU에서 실행되는 작은 프로그램으로, **그래픽을 그리는 방식**을 제어합니다.
즉, **"화면에 무엇을 어떻게 그릴지"를 결정하는 코드**입니다.

## 🧩 쉐이더의 종류 (기본 2가지)
### 1. **Vertex Shader (버텍스 쉐이더)**
- **입력:** 정점(Vertex, 점)의 위치
- **역할:**  
  - 3D 좌표를 2D 화면 좌표로 변환
  - 정점 색상, 텍스처 좌표 등 계산
- 📌 예시: 삼각형의 각 꼭짓점 위치를 화면에 맞게 변환
### 2. **Fragment Shader (프래그먼트 쉐이더, 픽셀 쉐이더)**
- **입력:** 화면에 찍힐 **각 픽셀**
- **역할:**  
  - 픽셀의 최종 색상을 계산
  - 텍스처 적용, 조명 효과 등 포함
- 📌 예시: 삼각형 내부의 각 픽셀을 빨간색으로 칠하기
## 🎯 쉐이더는 왜 필요한가?
- 성능: CPU 대신 GPU에서 병렬로 빠르게 실행
- 표현력: 조명, 그림자, 반사, 애니메이션 등 자유롭게 구현 가능
- 맞춤 렌더링: 내가 원하는 스타일로 화면을 표현할 수 있음
## 🛠 쉐이더 언어
- **GLSL** (OpenGL / Vulkan용)
- **HLSL** (DirectX용)
- **SPIR-V** (Vulkan에서 사용하는 바이트코드)
예를 들어, Vulkan에서는 GLSL 코드를 작성한 후 SPIR-V로 **컴파일**해서 사용합니다.
## 📄 간단한 GLSL 예시 (삼각형 색칠하기)
### Vertex Shader (`vert.glsl`)
```glsl
#version 450
layout(location = 0) in vec2 inPosition;
void main() {
    gl_Position = vec4(inPosition, 0.0, 1.0);
}
```
### Fragment Shader (`frag.glsl`)
```glsl
#version 450
layout(location = 0) out vec4 outColor;
void main() {
    outColor = vec4(1.0, 0.0, 0.0, 1.0); // 빨간색
}
```
---
## 🧪 Vulkan에서는 어떻게 쓰나요?
1. 위 GLSL 쉐이더 코드를 `.spv`로 컴파일 (예: `glslangValidator` 사용)
2. Vulkan 코드에서 SPIR-V 파일을 로드하고, 쉐이더 모듈 생성
3. 파이프라인에 등록해서 렌더링 수행
---
## GLSL → SPIR-V 컴파일 방법?
C:/VulkanSDK/1.4.309.0/Bin/**glslc.exe** shader.vert -o vert.spv
C:/VulkanSDK/1.4.309.0/Bin/**glslc.exe** shader.frag -o frag.spv


