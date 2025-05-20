GPU 셰이더 구조는 **GPU가 그래픽 데이터를 처리하는 핵심 프로그램 구성**으로, 그래픽 파이프라인의 각 단계를 **프로그래머가 직접 제어할 수 있게** 만든 것입니다. 주로 사용하는 셰이더에는 다음과 같은 종류가 있습니다:

---

## 🎯 주요 GPU 셰이더 종류 (그래픽스 파이프라인 기준)

| 셰이더                                | 역할                                       | 사용 위치                                |
| ---------------------------------- | ---------------------------------------- | ------------------------------------ |
| **Vertex Shader**                  | 정점 위치, 색상, 텍스처 좌표 등 처리. 3D 좌표 → 2D 화면 변환 | 초반 (정점 처리 단계)                        |
| **Tessellation Shader**            | 정점 사이를 세분화하여 더 정교한 지오메트리 생성              | 고급 렌더링 (옵션)                          |
| **Geometry Shader**                | 정점 집합(삼각형, 선 등)을 받아 새 도형 생성 가능           | 프리미티브 처리 단계 (옵션)                     |
| **Fragment Shader** (Pixel Shader) | 픽셀별 색상, 조명, 텍스처링 등 최종 출력 색상 계산           | 후반 (래스터화 이후)                         |
| **Compute Shader**                 | 렌더링과 무관한 일반 계산 (물리 시뮬레이션, AI 등)          | 별도 실행 (OpenGL 4.3+, Vulkan/WebGPU 등) |

---

## 🧱 GPU 셰이더 구조 요약 (데이터 흐름 관점)

```
[Vertex Buffer] → [Vertex Shader]
                    ↓
             [Tessellation Shader] (옵션)
                    ↓
             [Geometry Shader] (옵션)
                    ↓
           [Rasterization (픽셀화)]
                    ↓
             [Fragment Shader]
                    ↓
          [Framebuffer / 스크린 출력]
```

---

## 💡 각 셰이더 특징 요약

| 이름                  | 입력                  | 주요 작업            | 출력             |
| ------------------- | ------------------- | ---------------- | -------------- |
| **Vertex Shader**   | 정점 위치, 노멀, 텍스처 좌표 등 | 모델 → 뷰 → 투영 변환   | 스크린 좌표, 추가 데이터 |
| **Geometry Shader** | 도형(예: 삼각형) 단위       | 도형 복제, 라인 생성 등   | 새로운 도형         |
| **Fragment Shader** | 픽셀 위치, 텍스처 좌표 등     | 조명, 그림자, 텍스처 적용  | 최종 색상          |
| **Compute Shader**  | 자유로운 버퍼 데이터         | 행렬 곱셈, 필터링, AI 등 | 버퍼 결과          |

---

## 🔤 셰이더 언어 예시: GLSL (OpenGL), WGSL (WebGPU), HLSL (DirectX)

### ✔ GLSL로 작성한 간단한 Vertex + Fragment 셰이더 예:

```glsl
// Vertex Shader (GLSL)
#version 330 core
layout (location = 0) in vec3 aPos;
uniform mat4 u_MVP;
void main() {
    gl_Position = u_MVP * vec4(aPos, 1.0);
}

// Fragment Shader (GLSL)
#version 330 core
out vec4 FragColor;
void main() {
    FragColor = vec4(1.0, 0.5, 0.2, 1.0); // 주황색
}
```

---

## 🎓 셰이더 학습의 핵심 포인트

| 항목                                                | 설명                |
| ------------------------------------------------- | ----------------- |
| 셰이더는 GPU에서 실행되는 병렬 함수이다                           | 각 정점, 픽셀마다 병렬 실행됨 |
| GLSL은 OpenGL용 셰이더 언어                              | 구조가 C와 유사         |
| 셰이더는 `in/out`, `uniform` 등을 통해 CPU ↔ GPU 간 데이터 교환 |                   |
| 렌더링 품질은 거의 셰이더로 결정된다                              | 조명, 그림자, 반사, 굴절 등 |

---

셰이더 구조를 잘 이해하면 **Vulkan, WebGPU, Unity/Unreal의 커스텀 셰이더 작성**에도 적용이 가능합니다.
필요하시면 각 셰이더별 예제 코드, GLSL vs WGSL 비교표, 또는 실습용 샘플도 제공해 드릴 수 있어요.

특히 관심 있는 셰이더 단계가 있으신가요? (예: Fragment Shader로 조명 만들기 등)
