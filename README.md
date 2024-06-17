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

### 세그멘테이션 결과

세그멘테이션을 적용한 결과는 다음과 같습니다:

![세그멘테이션 예시](readme%20img/yolov8-seg.png)





ultralytics 경로설정
yaml 경로설정
test2.ipynb파일은 됨 . 물론 x-ray데이터  

근데 explosive 는 안됨 . 소량 데이터 다시 라벨링후 확인 필요 .


내일 뭐해ㅑㅇ 되ㅑㄴ면 , 폴리곤말고 네모로 바운딩박스 해서 안되는지 알아봐야함 

아니 똑같이 polygon 한ex-1데이터는 seg가 안되고 왜 x-ray2, a-1 데이터는 seg가 됨 ?

같은 데이터셋인데 augment 한거는 학습이 오류나고, 안한거는 또 되고. 


혹시 valid나 test의 라벨을 맞춰야 하는데 이 라벨이 train에 없는건 아닐까
그래서 오류가 뜨는거지 .


지금 sst랩 덷이터 train데이터 2571장만 instance segmantation 했는데 이건왜또되냐 -> 데이터설정할댸 instance segmentation 으로 해야됨

### Segmentation 모델을 위한 정교한 라벨링 필요성 발견

프로젝트 진행 중 YOLOv8-seg 모델을 사용하여 세그멘테이션을 학습하는 과정에서, 기존 라벨링된 데이터 중 일부는 성공적으로 동작했지만 일부는 실패하는 현상을 발견했습니다. 자세한 분석을 거쳐 Segmentation 모델을 제대로 활용하기 위해서는 단순한 Bounding Box가 아닌 정교한 polygon 형태의 라벨링이 필요하다는 결론을 얻었습니다.

- **Bounding Box 라벨링**: 실패했던 데이터는 단순한 사각형 형태의 Bounding Box로 라벨링되어 있었습니다.

![Bounding Box 예시](readme%20img/bad.png)

- **Polygon 라벨링**: 성공적으로 학습된 데이터는 객체의 경계를 따라 정확하게 그려진 polygon 형태로 라벨링되어 있었습니다.

![Polygon 예시](readme%20img/good.png)

### 데이터셋 변환 및 재학습

1. **Roboflow를 이용한 데이터셋 변환**: 기존 Bounding Box로만 라벨링된 데이터를 정교한 polygon 형태로 변환하기 위해 Roboflow를 사용했습니다.
   - Roboflow에 기존 데이터를 업로드하고, polygon 형태의 라벨링을 생성한 후 YOLOv8 형식으로 다시 다운로드했습니다.
