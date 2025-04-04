## 🧭 Vulkan 입문자를 위한 학습 로드맵

### 📘 1. **전제 지식 갖추기**
- ✅ C++ 기본 문법 (포인터, 클래스, RAII 등)
- ✅ 그래픽스 기초 이해 (좌표계, 렌더링 파이프라인, 쉐이더 등)
- ✅ GPU 동작 방식(프레임 버퍼, 렌더 패스 등)

---

### 🧱 2. **환경 설정**
- [ ] Vulkan SDK 설치 (LunarG 공식)
- [ ] Visual Studio or CMake + VSCode + MinGW
- [ ] GLFW 설치 (창 생성, 이벤트 처리용)
- [ ] Validation Layer + RenderDoc (디버깅 필수)

---

### 🧪 3. **기초 프로젝트: Hello Vulkan**
> 목표: "창을 띄우고, 초록색으로 Clear"

학습 포인트:
- Vulkan 인스턴스 생성
- 디바이스 선택 (GPU)
- 스왑체인 생성
- 렌더패스, 프레임버퍼 구성
- 커맨드 버퍼 녹화 및 제출
- `vkQueuePresentKHR`로 화면 출력

---

### 🎨 4. **삼각형 렌더링 (쉐이더 포함)**
> 목표: 삼각형을 그리기

학습 포인트:
- Vertex Buffer, Index Buffer
- GLSL 쉐이더 → SPIR-V 컴파일
- 파이프라인 객체 생성 (`VkPipeline`)
- Descriptor, Uniform 추가 (선택)

---

### ⚙️ 5. **입출력과 동적 변환**
> 목표: 마우스/키보드 입력, 뷰 행렬 변환 등

학습 포인트:
- 카메라 매트릭스 (MVP 행렬)
- Uniform Buffer 업데이트
- GLFW 이벤트 연결

---

### 📦 6. **모델 로딩 및 텍스처**
> 목표: OBJ 파일, PNG 텍스처 로딩

학습 포인트:
- 이미지 읽기 (STB 이미지)
- 샘플러, 텍스처 매핑
- 동적 메모리 전송 (`staging buffer`)

---

### 🧠 7. **고급 렌더링 주제**
> 예: 멀티패스, 섀도우 매핑, G-buffer 등

학습 포인트:
- 여러 렌더패스 구성
- Framebuffer chaining
- Compute Shader 활용

---

## 📚 추천 자료

| 분류 | 추천 |
|------|------|
| 공식 튜토리얼 | [https://vulkan-tutorial.com](https://vulkan-tutorial.com) (★★★★★) |
| 책 | *Vulkan Programming Guide* (Red Book), *Vulkan Cookbook* |
| 유튜브 강좌 | Brandon Jones, TheCherno Vulkan 시리즈 |
| 디버깅 툴 | RenderDoc, Vulkan Configurator (Validation Layer GUI) |

---

## 🚀 보너스: "최소 예제 → 빌드 성공" 후 성취감을 얻자!
- 작은 성공을 쌓으며 가야 지치지 않습니다.
- 처음엔 "초록색 화면"이라도, 한 걸음 한 걸음 가다 보면 멋진 3D 엔진도 만들 수 있어요 😄

---

필요하시면 각 단계에 맞는 **실습 예제 코드, 강의 자료, 혹은 GitHub 템플릿**도 추천드릴게요.  
어떤 단계부터 시작하실 건가요? 시작을 도와드릴게요! 🎯
