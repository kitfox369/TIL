# Initial page

## 외곽선 검출

> 출처 : [OpenCV 4로 배우는 컴퓨터 비전과 머신러닝](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=187822936)

* 외곽선이란?

    객체 영역 픽셀 중 배경 영역과 인접한 일련의 픽셀

* 객체 바깥쪽 외곽선과 안쪽 홀 외곽선으로 구분 가능
* 한 외곽선은 vector 타입으로 저장되고 객체는 여러 개일 경우가 존재하므로 vector&gt; 로 저장됨
* vector&gt; contours 라는 변수로 저장하였을 때
  * 전체 객체의 숫자 : contours.size\(\)
  * 해당 객체의 외곽선 의 점 갯수 : contours\[해당 객체 번호\].size\(\)
* void findContours\(InputArray Image, OutputArrayOfArrays contours, OutputArray hierarchy, int mode, int method, Point offset = Point\(\)\);
* void findContours\(InputArray Image, OutputArrayOfArrays contours, int mode, int method, Point offset = Point\(\)\);
  * Image : 입력 영상  
  * contours : 검출된 외곽선 정보
  * hierarchy : 외곽선 계층 정보
  * mode : 외곽선 검출 모드
  * offset : 외곽선 점 좌표의 오프셋\(이동 범위\)
* **findContours\(\)** : 영상 내부 객체들의 외곽선 검출 함수
  * 보톤 이진 영상을 사용
  * 픽셀 값이 0이 아니면 객체로 간주하여 외곽선 검출
* hierarchy 인자에는 보통 vector 타입\(4개의 int로 이루어진 벡터\)으로 외곽선의 계층 정보 저장
  * hierarchy\[i\]\[0\] : 다음 외곽선 번호
  * hierarchy\[i\]\[1\] : 이전 외곽선 번호
  * hierarchy\[i\]\[2\] : 자식 외곽선 번호
  * hierarchy\[i\]\[3\] : 부모 외곽선 번호
  * 해당 외곽선 존재하지 않으면 -1 삽입
* mode 인자에는 외곽선을 어떤 방식으로 검출할 것인지 설정해줌

| RetrievalModes 열거형 상수 | 설명 |
| :--- | :--- |
| RETR\_EXTERNAL | 객체 바깥쪽 외곽선만 검색, 계층 구조 만들지 X |
| RETR\_LIST | 객체 바깥,안쪽 외곽선 모두 검색,계층 구조 만들지 X |
| RETR\_CCOMP | 모든 외곽선 검색,2단계 계층 구조 |
| RETR\_TREE | 모든 외곽선 검색,전체 계층 구조 |

* method 인자에는 검출된 외곽선 점들의 좌표를 근사화 하는 방법 설정

| ContourApproximationModes 열거형 상수 | 설명 |
| :--- | :--- |
| CHAIN\_APPROX\_NONE | 모든 외곽선 점들의 좌표를 지정 |
| CHAIN\_APPROX\_SIMPLE | 외곽선 중에서 수평선, 수직선 대각선 성분은 끝점만 저장 |
| CHAIN\_APPROX\_TC89\_L1 | Teh & Chin L1 근사화 적용 |
| CHAIN\_APPROX\_TC89\_KCOS | Teh & Chin k cos 근사화 적용 |

* 검출한 외곽선 정보를 이용하여 영상 위에 외곽선을 그리고 싶다면 drawContours\(\) 함수 사용
* void drawContours\(InputOutputArray image, InputArrayOfArrays contours, int contourIdx, const Scalar& color, int thickness = 1, int lineType = LINE\_8, InputArray hierarchy = noArray\(\), int maxLevel = INT\_MAX, Point offset = Point\(\)\);
  * image : 외곽선을 그릴 영상
  * contours : findContours\(\) 함수로 구한 전체 외곽선 정보
  * contourIdx : 외곽선 번호, 음수 지정하면 전체 외곽선 그림
  * color : 외곽선 색상\(또는 밝기\)
  * thickness : 외곽선 두께, FILLED 또는 -1 지정하면 외곽선 내부를 채움
  * lineType : 외곽선 타입
  * hierarchy : 외곽선 계층 정보
  * maxLevel : 그릴 외곽선의 최대 레벨 \(0인 경우 지정한 번호의 외곽선만, 1보다 같거나 크면 그에 해당하는 하위 레벨의 외곽선까지 그림\)
  * offset : 추가적으로 지정할 외곽선 점 좌표의 오프셋, 이 좌표만큼 이동하여 그림

