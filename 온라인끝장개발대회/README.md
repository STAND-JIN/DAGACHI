# DAGACHI Font Recognition Project

광주인공지능사관학교 2기 온라인 끝장개발 대회 - 2021-10-12~2021-10-13

다가치 팀은 사용자의 손글씨를 인식하여 학습된 폰트들 중 가장 비슷한 폰트를 찾아주는 프로젝트를 진행했다.

### Used Libraries
```
cv2
keras == 2.3.1
tensorflow == 2.2.0
pandas
numpy
sklearn
shutil
matplotlib
```

### Train Data
손글씨와 비슷한 느낌을 주는 폰트와의 비교를 위해 네이버 클로바 나눔손글씨 폰트 중 일부를 학습데이터로 활용하였다.

Link : https://clova.ai/handwriting/list.html

### Test Data
직접 작성한 손글씨 데이터를 opencv를 이용하여 가공한 후 인식 테스트를 진행했다.

### Training Model
한정된 시간으로 데이터 수집에 많은 시간을 할애하기가 어려웠고, 손글씨 특성 상 크기와 각도가 다양하기 때문에 ImageDataGenerator를 통하여 학습데이터를 증폭하여 학습을 진행했다.
이외 딥러닝 모델 구성은 다음과 같다.
```
model = Sequential()
model.add(Conv2D(64, kernel_size=(3,3), padding='same', input_shape=(28,28,3), activation='relu'))
model.add(MaxPooling2D(pool_size=(2,2)))
model.add(Dropout(0.2))

model.add(Conv2D(128, kernel_size=(3,3),padding='same', activation='relu'))
model.add(MaxPooling2D(pool_size=(2,2)))
model.add(Dropout(0.2))

model.add(Conv2D(256, kernel_size=(3,3), padding='same', activation='relu'))
model.add(MaxPooling2D(pool_size=(2,2)))
model.add(Dropout(0.2))

model.add(Flatten())
model.add(Dense(256, activation='relu'))
model.add(Dropout(0.2))
model.add(Dense(10, activation='softmax'))
```

### Result
학습 결과를 토대로 테스트를 진행한 글자와 해당 글자에 가까운 모양의 폰트명이 함께 출력된다.
