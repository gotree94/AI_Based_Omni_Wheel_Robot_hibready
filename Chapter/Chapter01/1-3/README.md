# 사람과 동물을 인식하는 로봇 구현

## 1.3.1 학습모델 준비하기

1) PC와 로봇을 Micro 5pin 케이블로 연결한다.


2) 로봇의 전원 스위치를 ON 시킨다.


3) PC의 "실행" 앱에서 아래와 같이 입력 하여 로봇에 접속한다.

```
\\192.168.55.1
```
![](030.png)

![](032.png)


4) 로봇과 접속이 완료되면 아래와 같이 풀더가 표시된다.


5) 아래 위치로 이동한다.


6) 작업을 위한 폴터를 새로 생성한다.


7) 앞에서 만든 최종 학습모델 'recognition' 폴터와 'training_data' 폴더 내의  'detection_classes.txt' 파일을 복사하여 'AI Test' 폴터에 붙여 넣는다.



## 1.3.2 모델 최적화하기

1) 프로그램 파일 생성

(1) 로봇 접속을 위해 크롬 퓁 브라우저에 아래와 같이 주소를 입력한다.

```
유선접속 : 192.168.55.1:8888
무선접속 : 로봇 IP:8888
```

(2) 실습용 폴더로 이동 한다.

(3) 우측의 'New' 버튼을 눌러 'Python 3'를 생성한다.

(4) 상단 'Untitled'를 선택하여 실습 제목을 변경한다.


2) 프로그램 작성

* 영상처리를 위해 'cv2' 모듈을 추가한다.

* 인공지능 학습에 필요한 파이썬 모듈이 설치된 'bready' 모듈 중 객체감지 최적화에 필요한 "TFTRT_detection" 모듈을 추가한다.

* 인공지능 학습에 필요한 파이썬 모듈이 설치된 'bready' 모듈 중 객체감지에 필요한 'objectDetector' 모듈을 추가한다.

```
import cv2
import bready.object_detection_toold.trt_utils.detection.TFTRT_convert_model_api as TFTRT_detection
from bready.object_detection_tools import ObjectDetector
```

* 'convertToOptimizationModel()' 함수를 사용하여 최종 학습 모델을 로봇에 장착된 jetson 보드에 적합하도록 최적화시킨다.
* 첫번때 파라미터는 최종 학습 모델의 경로, 두번째 파라미터는 최적화시킨 모델을 저장할 경로를 설정한다.

```
TFTRT_detection.convertToOptimizationModel(
  'regocnition',
  'optimization',
  config_name='pipeline.config',
  checkpoint_name='modle.ckpt'
)
```

3) 실행 및 결과

(1) 동작을 실행하기 위해 상단의 'Restart' 버튼을 선택한다.

(2) 모델 최적화가 완료되면 실행 결과가 나타난다.


## 1.3.3 로봇에서 사람과 동물 감지

1) 프로그램 파일 생성

(1) 우측의 'New' 버튼을 눌러 'Python 3'를 생성한다.

(2) 상단 'Untitled'를 선택하여 실습 제목을 변경한다.

2) 프로그램 작성

* 영상처리를 위해 'cv2' 모듈을 추가한다.
* 운영체제(OS)에서 제공하는 기본적인 기능을 사용하기 위해 'os' 모듈을 추가한다.
* 시간 지연을 위해 'time' 모듈을 추가한다.

```
import os
import cv2
import time
```

* 카메라 영상을 사용하기 위해 'PyCamera' 모듈을 추가한다
* 인공지능 학습에 필요한 파이썬 모듈이 설치된 'bready' 모듈 줄 객체감지에 필요한 'objectDetector' 모듈을 추가한다.

```
import bready.camera_utils.PyCamera as PyCamera
from bready.object_detection_tools import ObjectDetector
```

* 화면에 위겟을 사용하기 위해 'widgets' 모듈을 추가한다.
* 현재 화면에 표시하기 위해 'IPython.display' 모듈을 추가한다.

3) 실행 및 결과



