---
title: CUDA 버전에 따라 Pytorch, pytorchvision 다운로드 하기
excerpt: 각자 cuda 드라이버 버전에 맞는 파이토치 다운로드 하기

categories:
    - Misc
tags:
    - pytorch
    - 삽질
  
comments: true
---

## CUDA 버전에 맞는 Pytorch, Pytorchvision 설치하기

대표적인 딥러닝 프레임워크에는 pytorch, tensorflow, keras 등이 있습니다. 그 중에서 주로 대학원 등 연구기관에서 쓰는 프레임워크는 파이토치가 가장 많죠. 그런데 파이토치를 무턱대고 설치하다 보면 설치할 때는 에러가 안 나도 막상 모델을 돌릴 때 에러가 날 때가 많습니다. 현재 컴퓨터의 그래픽카드 드라이버 버전과 맞지 않아서 이죠. 그렇기 때문에 Pytorch Organization 에서 공식적으로 설치하라는 버전을 따라야 합니다. 링크는 [Pytorch](https://pytorch.org/get-started/previous-versions/) 를 클릭하시면 previous version 으로 파이토치 설치하는 법이 나옵니다. 


## CUDA 버전 확인하기
 먼저 컴퓨터에 설치된 CUDA버전을 아래 커맨드 라인을 입력하여 확인합니다. 
```
 nvcc -V
```
![21](https://user-images.githubusercontent.com/43398106/130587868-47c86589-581c-4e2a-af6b-4f1920eac92d.png)

제 컴퓨터에서는 CUDA 11.2 버전을 사용하고 있습니다. 2021년 8월 기준 가장 최신 버전이기 때문에 파이토치도 최신 버전을 사용하면 됩니다. 하지만 cuda 11.0, 10.2, 10.1 ...등 이전 버전을 사용하는 경우 아래 커맨드를 입력하여 torch, torchvision을 설치하면 됩니다. 

```
# CUDA 9.2
conda install pytorch==1.7.1 torchvision==0.8.2 torchaudio==0.7.2 cudatoolkit=9.2 -c pytorch

# CUDA 10.1
conda install pytorch==1.7.1 torchvision==0.8.2 torchaudio==0.7.2 cudatoolkit=10.1 -c pytorch

# CUDA 10.2
conda install pytorch==1.7.1 torchvision==0.8.2 torchaudio==0.7.2 cudatoolkit=10.2 -c pytorch

# CUDA 11.0
conda install pytorch==1.7.1 torchvision==0.8.2 torchaudio==0.7.2 cudatoolkit=11.0 -c pytorch

# CPU Only
conda install pytorch==1.7.1 torchvision==0.8.2 torchaudio==0.7.2 cpuonly -c pytorch

```