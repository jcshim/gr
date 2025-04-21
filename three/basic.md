## **이 코드는 Three.js를 이용해 초록색 직사각형을 화면에 띄우는 프로그램이다.**

```
<body>
  <script src="https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.min.js"></script>
  <script>
    const T = THREE; // 별칭(alias) 선언
    const W = innerWidth;
    const H = innerHeight;

    const R = new T.WebGLRenderer();
    R.setSize(W, H);
    document.body.appendChild(R.domElement);

    const C = new T.PerspectiveCamera(75, W / H, 0.1, 1000);
    C.position.z = 5;
  
    const S = new T.Scene();
    const M = new T.Mesh(
      new T.PlaneGeometry(4, 2),
      new T.MeshBasicMaterial({ color: 0x00ff00 })
    );
    S.add(M);
    R.render(S, C);
  </script>
</body>
```
### 간단한 설명

- `T`는 `THREE`의 별명이다.
- `W`, `H`는 화면 너비, 높이이다.
- `R`은 화면에 그림을 그리는 렌더러다.
- `C`는 3D 장면을 보는 카메라다.
- `S`는 3D 장면(무대)이고,
- `M`은 초록색 직사각형 물체다.
- 마지막에 `R.render(S, C)`로 장면을 화면에 그린다.

---

**한 줄 요약:**  
> Three.js로 카메라, 장면, 물체를 만들고 화면에 렌더링하는 기본 코드다.

---

조금 더 짧게 요약하거나, 단계별 설명으로 풀어볼까? 🎯  
(원하면 바로 해줄게!)
