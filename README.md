# YOLOv10m과 YOLOv8-seg를 이용한 커스텀 객체 탐지

기존의 YOLOv5 모델에서 성능을 높이기 위해 최신 YOLOv10m 모델로 교체하여 객체 탐지 프로젝트를 진행했습니다. 다음은 프로젝트의 단계와 결과입니다:

## 데이터 준비 및 증강

테스트를 위해 약 100장의 라벨링된 이미지를 시작으로, 데이터 증강 기법인 그레이스케일 변환 및 회전을 적용하여 데이터셋을 확장했습니다. 이로 인해 총 240장의 라벨링된 데이터셋이 준비되었습니다.

## 모델 학습

증강된 데이터셋을 이용하여 YOLOv10m 모델을 학습시켰습니다. 학습 과정은 총 150번의 에폭을 통해 진행되었으며, 다음과 같은 성능을 얻었습니다:

![성능 플롯](readme%20img/yolov10%20plot.png)

## 바운딩 박스 탐지

모델의 바운딩 박스 탐지 성능을 테스트하고 시각화한 결과는 다음과 같습니다:

![바운딩 박스 예시](readme%20img/yolov10%20boundingbox.png)

## YOLOv8-seg를 이용한 세그멘테이션

프로젝트 진행 중 YOLO 모델 중 세그멘테이션 기능을 제공하는 모델이 있다는 것을 알게 되었습니다. 하지만 YOLOv9-seg와 YOLOv10-seg 모델은 아직 출시되지 않아, YOLOv8-seg 모델을 사용하기로 결정했습니다. 학습된 이미지는 다음과 같습니다:

![세그멘테이션 플롯](readme%20img/yolov8-plot.png)

## 세그멘테이션 결과

세그멘테이션을 적용한 결과는 다음과 같습니다:

![세그멘테이션 예시](readme%20img/yolov8-seg.png)

이와 같은 과정을 통해 YOLOv10m 모델과 YOLOv8-seg 모델을 활용한 커스텀 객체 탐지를 성공적으로 수행하였습니다. 앞으로 더 다양한 데이터와 최신 모델을 활용하여 성능을 더욱 향상시킬 계획입니다.

GitHub 주소: [https://github.com/wahoman/yolov10m.git](https://github.com/wahoman/yolov10m.git)