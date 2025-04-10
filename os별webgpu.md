### ✅ 사용되는 백엔드(API)는 다음과 같습니다:

| 플랫폼 | 브라우저 | WebGPU 내부 구현 (백엔드) |
|--------|----------|----------------------------|
| **Windows** | Chrome, Edge | **Direct3D 12** |
| **Linux** | Chrome | **Vulkan** |
| **macOS** | Chrome, Safari | **Metal** |
| **Android** | Chrome | **Vulkan** |
| **iOS** (미지원) | - | WebGPU **공식 미지원**, 실험적 Metal 가능성 |
| **ChromeOS** | Chrome | Vulkan 또는 D3D12 |

---

### 🔧 어떻게 동작하는가?

WebGPU는 표준 API지만, **브라우저 내에서는 내부적으로 "플랫폼별 네이티브 그래픽 API"로 매핑됩니다**.  
구체적으로는 다음과 같은 WebGPU 구현체가 그 역할을 수행합니다:

- **Dawn** (by Google): WebGPU → Direct3D 12 / Vulkan / Metal
- **wgpu-native** (by Mozilla): Rust 기반, 동일하게 Vulkan/D3D12/Metal로 백엔딩

Three.js의 `WebGPURenderer`는 `navigator.gpu`를 통해 **브라우저의 WebGPU 구현체(Dawn 등)**에 접근하고,  
이 구현체는 사용 중인 플랫폼에 따라 적절한 API를 자동으로 선택하여 GPU와 통신합니다.

---

### 🔍 요약

당신의 코드:

```js
import WebGPURenderer from 'three/addons/renderers/webgpu/WebGPURenderer.js';
```

이 부분은 **Three.js가 WebGPU API를 통해 그래픽을 처리**하도록 만들지만,  
실제 GPU 호출은 아래와 같이 **플랫폼 종속적으로 네이티브 API로 바뀝니다**:

- 🪟 Windows → Direct3D 12  
- 🐧 Linux → Vulkan  
- 🍎 macOS → Metal

---

### 🧪 참고 Tip: 백엔드 확인 방법

만약 실제로 **어떤 백엔드(D3D12, Vulkan 등)가 사용되는지** 확인하고 싶다면:

- **Chrome 브라우저에서 `chrome://gpu`** 주소에 접속해 보세요.
- 거기서 `"WebGPU Backend in use"` 항목을 찾으면 됩니다.

---

필요하시면 WebGPU 백엔드 선택을 강제하는 실험 플래그나, `Dawn` 설정 관련 정보도 드릴 수 있어요.  
혹시 WebGPU를 수업/논문/연구에 활용하시는 건가요?
