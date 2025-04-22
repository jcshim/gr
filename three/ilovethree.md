```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Three.js Cube - 작은 창</title>
  <style>
    body { margin: 0; overflow: hidden; }
    canvas {
      position: absolute;
      left: 0;
      top: 0;
      width: 320px;
      height: 240px;
    }
  </style>

  <script type="importmap">
    {
      "imports": {
        "three": "https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.module.js"
      }
    }
  </script>
</head>
<body>
  <script type="module">
    import * as THREE from 'three';

    // 기본 설정
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(75, 320 / 240, 0.1, 1000); // 카메라 비율도 320:240 고정
    const renderer = new THREE.WebGLRenderer({ antialias: true });
    renderer.setSize(320, 240); // 320x240 고정
    renderer.setClearColor('gray'); // CSS 색 이름도 가능
    document.body.appendChild(renderer.domElement);

    // 큐브 만들기
    const geometry = new THREE.BoxGeometry(2,2,2);
    const material = new THREE.MeshStandardMaterial({ color: 0x0077ff });
    const cube = new THREE.Mesh(geometry, material);
    scene.add(cube);

    // 큐브를 45도(x, y축) 회전
    cube.rotation.x = Math.PI / 4;
    cube.rotation.y = Math.PI / 4;

    // 조명 추가
    const light = new THREE.DirectionalLight(0xffffff, 1);
    light.position.set(5, 5, 5);
    scene.add(light);

    const ambientLight = new THREE.AmbientLight(0x404040);
    scene.add(ambientLight);

    // 카메라 위치 조정
    camera.position.set(0, 0, 5);

    // 단순 렌더링
    function animate() {
      requestAnimationFrame(animate);
      renderer.render(scene, camera);
    }

    animate();
  </script>
</body>
</html>
```
