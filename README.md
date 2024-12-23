# KITTI_spoofing

## Setup / 환경 설정: python 3.7버전 사용

### Data Requirements / 데이터 요구 사항:
```bash
/velodyne/       # .bin files (LiDAR point cloud data)
/label_2/        # Bounding box label files
/calib/          # Calibration files
/image_2/        # RGB images (for visualization)
```

### root file
```bash
Z:/media/ssd3/lab/sypark/KITTI/object/2d_object/data_object/
  ├── training/
  │     ├── image_2/                      # 원본 이미지 데이터
  │     ├── velodyne/                     # 원본 LiDAR 데이터
  │     ├── calib/                        # Calibration 파일
```

## File and Folder Descriptions / 파일 및 폴더 설명
### 1. bilateral_filter_org_png.ipynb
이 파일은 LiDAR 또는 RGB 데이터에 이중 필터(Bilateral Filter)를 적용한 결과를 확인할 수 있는 참조 이미지입니다.
포인트 클라우드 데이터의 노이즈를 줄이거나 RGB 채널에서 부드러운 결과를 얻는 데 사용됩니다.
데이터 전처리 과정에서 노이즈 감소의 효과를 설명하는 데 사용됩니다.

### 2.  final_empty_box_file
특정 바운딩 박스 내부의 포인트 클라우드 데이터를 제거하여 빈 상자를 생성하는 스크립트입니다.
LiDAR 데이터에서 객체가 없는 상태를 모사(spoofing)하기 위해 사용됩니다.

### 3.  final_copy_paste_file
바운딩 박스 내부의 포인트 클라우드 데이터를 복사한 후, 이동하거나 크기를 조정하여 새로운 스푸핑 데이터를 생성합니다.
특정 박스를 복제하고 임의의 위치로 이동시켜 LiDAR 데이터셋에 추가적인 객체를 삽입합니다.
scale 값을 활용하여 박스의 크기를 변경할 수 있습니다.

**해당 파일경로**
```bash
Z:/media/ssd3/lab/jojeon/KITTI/data_spoofing/
  └── velodyne/
        ├── train_add/                   # Spoofing: LiDAR 데이터 추가
        └── train_delete/                # Spoofing: LiDAR 데이터 삭제
```

### 4.  kitti_image_lidar_compare
KITTI 데이터셋에서 LiDAR 데이터와 RGB 이미지를 비교하는 스크립트입니다.
LiDAR 포인트 데이터를 RGB 이미지 평면에 투영하여 두 데이터의 정합성(Alignment)을 확인할 수 있습니다.

   
### 5.  kitti_image_RGB_5channel
RGB 이미지를 LiDAR 깊이(Depth)와 강도(Intensity) 데이터를 추가하여 5채널 형식으로 변환하는 스크립트입니다.
RGB (R, G, B) + Depth + Intensity로 구성된 이미지를 생성하여 시각 정보와 거리 정보를 통합합니다.

**해당 파일경로**
```bash
Z:/media/ssd3/lab/jojeon/KITTI/data_object/
  └── training/
        ├── rgb_depth_intensity/         # RGB, Depth, Intensity로 나눈 원본 데이터
        ├── rgb_depth_intensity_add/     # RGB, Depth, Intensity에 추가된 데이터
        └── rgb_depth_intensity_delete/  # RGB, Depth, Intensity에서 제거된 데이터
```


### 6.  RGB_depth_matching_system
RGB 이미지와 LiDAR 깊이 데이터를 매칭하여 두 데이터 간의 관계를 정렬(Alignment)하는 시스템을 구현합니다.
RGB 이미지의 픽셀과 LiDAR의 거리 데이터를 융합하여 센서 융합 기반의 데이터 처리를 가능하게 합니다.

### 7.  spoof_each_box_test_with_img
final_copy_paste_file와 유사하지만, 스푸핑된 결과를 RGB 이미지와 함께 테스트 및 시각화하는 스크립트입니다.
각 바운딩 박스를 복사하거나 수정한 후, LiDAR와 RGB 데이터를 동시에 확인할 수 있습니다.
Open3D와 같은 시각화 라이브러리를 사용하여 데이터의 효과를 확인할 수 있습니다.
