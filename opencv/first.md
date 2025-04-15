### Visual Stdio 실행(콘솔앱), Nuget 에서 opencv4 검색 후 설치
### [hdf 라이브러리 다운로드 설치](https://support.hdfgroup.org/releases/hdf5/v1_14/v1_14_6/downloads/index.html)

### 콘솔창 없애려면
1. 프로젝트 > 속성> 링커 > 시스템 > 하위 시스템 Windows (/SUBSYSTEM:WINDOWS)
2. 프로젝트 > 속성> 링커 > 고급 > 진입점(엔트리 지점) mainCRTStartup
* mainCRTStartup을 엔트리 포인트로 지정하고, 하위시스템을 Windows로 두면, 콘솔 창이 생성되지 않고 프로그램이 백그라운드에서 실행됨

```
#include <opencv2/opencv.hpp>
using namespace cv;

int main() {
    // 400x400 크기의 흰 배경 이미지 생성
    Mat img = Mat::zeros(400, 400, CV_8UC3);
    img = Scalar(255, 255, 255); // 흰 배경으로 초기화

    // 파란색 사각형 그리기 (좌상단 (50, 50), 우하단 (350, 350))
    rectangle(img, Point(50, 50), Point(350, 350), Scalar(255, 0, 0), 3);

    imshow("사각형 이미지", img);
    waitKey(0);
    return 0;
}
```

[Image Download](https://raw.githubusercontent.com/jcshim/img/refs/heads/main/jcshim.jpg)
```
#include <opencv2/opencv.hpp>
using namespace cv;

int main() {
    Mat img = imread("d:\\jcshim.jpeg"); 
    if (img.empty()) {
        std::cout << "이미지를 불러올 수 없습니다.\n";
        return -1;
    }
    imshow("이미지", img);
    waitKey(0);
    return 0;
}
```
