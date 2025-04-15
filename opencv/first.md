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
