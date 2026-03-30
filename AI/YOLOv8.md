---
layout: default
title: 23.5 YOLOv8
parent: 23. AI
description: ""
permalink: /yolov8/
---

## 1. Khái niệm

- YOLOv8 = You Only Look Once -> Ý tưởng: dự đoán object trực tiếp từ ảnh trong 1 lần forward pass
- YOLOv8 là phiên bản mới, cải tiến từ YOLOv5/7, tập trung vào: nhanh (real-time), chính xác hơn, dễ dùng hơn (API gọn)

## 2. Pipeline tổng thể

- YOLOv8 = 3 phần chính:

1. Backbone - trích xuất đặc trưng -> CNN học ra feature từ ảnh

    - input: ảnh (640x640)
    - output: feature map (ảnh đã encode)
    - VD: cạnh -> góc -> hình dạng -> object

2. Neck - gom thông tin đa scale -> YOLOv8 dùng kiểu FPN/PAN

    - Mục tiêu detect object nhỏ + lớn cùng lúc
    - VD: mặt người xa -> small feature, xe ô tô gần -> large feature

3. Head - dự đoán -> đây là phần quan trọng nhất

    - YOLOv8 dùng Anchor-free head (khác YOLOv5)
    - Nó dự đoán: bounding box (x, y, w, h), class, confidence

## 3. Điểm khác biệt của YOLOv8 so với YOLOv5

1. Anchor-free

- YOLOv5 phải định nghĩa anchor box
- YOLOv8 không cần anchor, dự đoán trực tiếp
- YOLOv8 ưu điểm: dễ train hơn, ít hyperparameter hơn

2. Decoupled head

- YOLOv8 tách: classification, regression (bbox)
- giúp: học ổn định hơn, chính xác hơn

3. Loss function cải tiến

- YOLOv8 dùng: CloD/DFL (Distribution Focal Loss)
- giúp: bbox chính xác hơn, giảm lệch vị trí

4. Task đa dạng

- YOLOv8 không chỉ detect: detection, segmentation, classification, pose (keypoint)

## 4. Cách model hiểu object

- Step 1: Pixel -> Feature: CNN học cạnh, texture, pattern
- Step 2: Feature -> Object: VD: hình tròn + 2 mắt -> face
- Step 3: Predict box: model output đa dạng `[x_center, y_center, width, height, confidence, class_probs...]`

## 5. NMS

- Sau khi predict xong sẽ có nhiều box trùng nhau -> dùng **None-Max Suppression (NMS)**: giữ box có confidence cao nhất, loại box overlap

## 6. Augmentation

- Mosaic: ghép 4 ảnh thành 1 giúp detect object nhỏ tốt hơn, đa dạng context
- MixUp: trọn 2 ảnh lại giúp giảm overfit, học robust hơn

## 7. Vì sao model detect kém

- YOLOv8 fail thường do:

1. Data kém: ít ảnh, label sai, thiếu đa dạng
2. Augmentation sai: mosaic quá mạnh -> mất realism, mixup nhiều -> nhiễu
3. Overfit: train loss ↓, val loss ↑
4. Scale object: object quá nhỏ -> cần mosaic + resize

## 8. Tóm tắt

- YOLOv8 = CNN (backbone) + multi-scale fusion (neck) + anchor-free head + NMS
