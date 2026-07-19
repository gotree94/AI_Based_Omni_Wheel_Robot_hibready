## 2.3 실습하기

### 2.3.1 프로그램 파일 생성

(1) 로봇 접속을 위해 크롬 웹 브라우저에 아래와 같이 주소를 입력 한다.

```
# 유선접속
192.168.55.1:8888

# 무선접속
로봇IP:8888
```

(2) 실습용 폴도로 이동한다.


(3) 우측의 "New" 버튼을 눌러 "Python 3"를 선택한다.


(4) 상단 "Untitled"를 선택하여 실습 제목을 변경한다.

---

### 2.3.2 프로그램 작성

(1) 운영체제에서 제공하는 다양한 기능(파일/폴더 제어, 환경 변수 확인, 시스템 명령어 실행 등)을 파이썬 스크립트 내에서 직접 수행하기 위해 "os" 추가한다.
* 시간 지연을 위해 "time" 모듈을 추가한다.
* ROS 노드를 사용하기 위해 "rospy" 모듈을 추가한다.
* 영상처리를 위해 "cv2"모듈을 추가한다.

```
import os
import time
import rospy
import cv2
```

(2) 수학 계산을 위해 "numpy"모듈을 추가한다.
* 좌표 처리를 위해 "getmetry" 모듈 중 "Twist"를 추가한다.

```
import numpy ad np
from geometry_msg.msg import Twist
```

(3) 카메라 영상을 사용하기 위해 "PyCamera" 모듈을 추가한다.
* 인공지능 학습에 필요한 파이썬 모듈이 설치된 'bready' 모듈 중 객체감지에 필요한 'objectDetector' 모듈을 추가한다.

```
import bready.camera_utils.PyCamera as PyCamera
from bready.object_detection_tools import ObjectDetector
```

(4) 화면에 위젯을 사용하기 위해 'widgets'를 추가한다.
* 현재 화면에 표시하기 위해 'IPython.display' 모듈을 추가한다.

```
import ipywidgets.widgets as widgets
import IPython.display
```

(5) 'URLCamera()' 함수로 TCP 주소의 카메라 영상의 이미지 데이터를 받아 'camera' 객체로 선언한다.
* 'camrea_url'의 값은 카메라 URL address를 입력하고, 'live_thread'의 값을 "True"로 설정하여 영상을 연속하여 받아올 수 있도록 활성화 한다.

```
camera = PyCamera.URLCamera(
  camera_url = "tcp://127.0.0.1:5000:,
  live_thread = True
)
```

(6) 'Tester()' 함수로 객체감지의 최적화 모델과 클래스 파일의 갱로를 설정하여 'obj_model' 객체로 저장한다.

```
obj_model = ObjectDetector.Tester(
  'optimization',
  'detection_classes.txt',
  ["image_tensor"]
)
```

(7) 객체의 주점을 구하는 'norm()' 함수를 정의한다.
* 'sqrt() 함수를 이용하여 감지된 객체의 X,Y 좌표의 중점을 계산하여 반환한다.

```
def norm(vec):
  return np.sqrt(vec[0]**2 + vec[1]**2)
```

(8) 가장 가까운 거리의 감지 대상을 찾는 'closest_detection()' 함수를 정의한다.
* 가장 가까운 감지 대상 값을 저장하기 위한 변소 'closest_detection'을 초기화 한다.

```
def closest_detection(detections):
  closest_detection = None
```

* 감지된 대상의 수만큰 반복하여 감지된 객체에 대한 X,Y의 좌료를 구한 뒤'center'에 저장한다.

```
for det in detections:
  center = (det["detection_center_point_x"], det["detection_boxes"][2])
```

* 만약 'closest_detection'의 데이터가 없을 겨우

* 

---

### 2.3.3 실행과 결과

(1) 작성한 예제 코드를 실행하기 위해 "Restart" 버튼을 선택한다.

(2) 프로젝트가 실행되면 설정한 카메라의 정보가 표시된다.

(3) 객체추적의 추론 결과가 나타난다. 왼쪽은 객체감지의 결과이며, 오른쪽은 감지된 객체를 추가적하기 위해 원형 좌표가 표시된다.

(4) Jupyter의 우측 메뉴에서 터미널을 실행한다.


* 실습 시 주의 사항
   * 하드웨어 예제를 수행하면 장비가 급 동작을 할 수 있다.
   * 감지된 대상의 거리가 충족되면 즉시 동작하며 안전을 위해 트랙 또는 바닥에 장비를 두어 동작을 실행한다.

(5) 터미널이 실행되면 로봇 제어를 위해 다음 예제를 실행한다. (예제를 실행하기 전 카메라를 가리거나 장비를 바닥에 둔다.)

```
rosrun omniwheel_project Robot_Operate.py
```


(6) 터미널 창에서 하드웨어 예제가 정상적으로 실핸되는 것을 볼 수 있다.
ros의 통신으로 각종 센서, PSD, 베터리 등의 하드웨어 정보가 표시된다.


(7) 감지된 Class '사람'에 따라 객체 추적 동작을 진행한다.


(8) Jupyter 터미널에서 실행중인 'Operate.py' 예제와 'roscore' 동작을 정지한다.
터미널에서 동작을 정지하기 위해 '[Ctrl] + C' 키를 눌러 동작을 종료한다.

(9) Jupyter 동작을 종료하면 상단의 'Stop'버튼을 선택한다.



