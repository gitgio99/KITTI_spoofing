# KITTI_spoofing — README (한국어)

이 저장소는 KITTI 데이터셋의 LiDAR/카메라 데이터를 변조(spoofing)하는 연구용 Jupyter 노트북과 유틸리티를 제공합니다.  
빈 박스 생성, 객체 복사-붙여넣기, RGB-Depth 정합 등 다양한 공격/실험 시나리오를 다룹니다.

## 1. 사용 환경
- 권장 Python 버전: 3.7–3.10  
- 가상환경(Anaconda/Miniconda) 권장
```bash
conda create -n kitti-spoof python=3.9 -y
conda activate kitti-spoof
pip install -r requirements_kitti_spoofing.txt
```

## 2. 데이터셋 구조
KITTI object 데이터셋은 다음 구조를 가집니다:
```
<KITTI_ROOT>/
  └─ training/
      ├─ image_2/    # 좌측 카메라 이미지
      ├─ velodyne/   # LiDAR 포인트클라우드(.bin)
      ├─ calib/      # 캘리브레이션(.txt)
      └─ label_2/    # 라벨 파일(.txt)
```
환경변수 `KITTI_ROOT`를 설정해 경로를 통일하세요.

## 3. 노트북 설명
- `bilateral_filter_org_png.ipynb`: Bilateral 필터링 실험
- `kitti_image_lidar_compare.ipynb`: LiDAR-이미지 투영 비교
- `kitti_image_RGB_5channel.ipynb`: 5채널(RGB+Depth+Intensity) 이미지 생성
- `RGB_depth_matching_system.ipynb`: RGB–Depth 매칭 시스템
- `final_empty_box_file.ipynb`: 박스 내부 포인트 제거
- `final_copy_paste_file.ipynb`: 박스 복사-붙여넣기 스푸핑
- `spoof_each_box_file.ipynb`, `spoof_each_box_test_with_img.ipynb`: 박스 단위 유틸 및 테스트

## 4. 실행 방법
Jupyter Notebook 실행:
```bash
jupyter notebook
```
`code/` 폴더 내 원하는 노트북을 열고 셀을 위에서부터 실행하세요.

## 5. 권장 사항
- 하드코딩된 절대경로 대신 환경변수 사용
- Depth/Intensity 정규화 후 저장
- 대용량 데이터(.bin, .npy)는 Git LFS로 관리

## 6. 참고 자료
- [KITTI 데이터셋](https://www.cvlibs.net/datasets/kitti/)
- [OpenCV Bilateral Filter](https://docs.opencv.org/4.x/d4/d86/group__imgproc__filter.html)
- [Open3D 문서](https://www.open3d.org/docs/release/)
