
# **WebXR**
웹 브라우저에서 \*\*VR(Virtual Reality, 가상현실)\*\*과 **AR(Augmented Reality, 증강현실)** 경험을 제공하기 위한 **Web API**입니다. 
즉, 별도의 앱 설치 없이 웹 브라우저만으로도 VR/AR 콘텐츠를 체험할 수 있도록 해주는 기술입니다.

---

### 🔧 핵심 개념

| 항목                 | 설명                                                                |
| ------------------ | ----------------------------------------------------------------- |
| **WebXR API**      | WebXR Device API의 약자. 브라우저에서 XR 디바이스와 상호작용할 수 있도록 해주는 API         |
| **XR**             | "Extended Reality"의 약자. VR, AR, MR(Mixed Reality)을 모두 포함하는 포괄적 용어 |
| **WebGL / WebGPU** | WebXR에서 3D 그래픽을 렌더링할 때 사용하는 그래픽스 API                              |
| **세션(Session)**    | XR 환경이 시작되는 단위. VR/AR 뷰를 보여줄 때 세션을 생성하고 렌더링을 시작함                  |

---

### 🧠 WebXR이 왜 중요한가요?

1. **웹 브라우저에서 직접 실행**
   → 사용자가 별도 앱 설치 없이 VR/AR 체험 가능

2. **멀티 플랫폼 지원**
   → Oculus Quest, HoloLens, Android ARCore, iOS ARKit 등과 호환

3. **Three.js 등과의 통합 용이**
   → Three.js를 통해 간단하게 WebXR 콘텐츠 제작 가능

---

### 📱 대표적인 WebXR 예시

* **가상 박물관**: 사용자가 VR 헤드셋으로 웹 브라우저에 접속하면 실제처럼 전시 관람 가능
* **증강현실 쇼핑**: 웹캠을 통해 가구를 실제 방에 배치한 듯 보이게 하는 AR 기능
* **WebXR Games**: 브라우저에서 바로 실행되는 3D VR 게임

---

### 🛠️ 주요 기술 스택

* HTML + JavaScript
* WebXR API
* Three.js, Babylon.js (렌더링 라이브러리)
* WebGL/WebGPU
* A-Frame (WebXR을 쉽게 사용할 수 있게 만든 프레임워크)

---

### ✅ 간단한 코드 예 (A-Frame 사용 예시)

[A-Frame](https://aframe.io/examples/showcase/responsiveui/)

```html
<html>
  <head>
    <script src="https://aframe.io/releases/1.3.0/aframe.min.js"></script>
  </head>
  <body>
    <a-scene>
      <a-box position="0 1 -3" color="blue"></a-box>
      <a-sky color="#ECECEC"></a-sky>
    </a-scene>
  </body>
</html>
```

브라우저에서 실행하면 기본 VR 씬이 생성되며, WebXR을 지원하는 기기에서는 헤드셋으로 볼 수 있습니다.

---

### 📌 요약

* **WebXR = 웹 브라우저 기반 VR/AR 플랫폼**
* 다양한 장치에서 호환 가능
* Three.js, A-Frame과 함께 사용하면 손쉽게 XR 콘텐츠 제작 가능
