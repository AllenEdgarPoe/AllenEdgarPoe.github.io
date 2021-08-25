---
title: 다른 환경에서 학습된 Pytorch Model 불러오기 
excerpt: gpu to cpu, single gpu to multi gpu 등 다양한 다른 환경에서 학습된 모델을 불러오자 

categories:
    - Misc
tags:
    - pytorch
    - 삽질
  
comments: true
---

파이토치를 사용한지 얼마 안 되었을 때 Gpu 설정 때문에 여러 가지로 문제를 많이 겪으실 겁니다. 특히 GPU에 대한 지식이 부족하다면 문제가 발생해도 어떻게 해결해야 할지 모르죠. 그 때 해결 방법을 알아봅시다. 

## 1. 다른 번호 GPU에서 학습된 Pytorch model을 불러오기

만약 cuda:0 에서 학습된 파이토치 모델을 cuda:1 에서 학습시키고 싶다면 map_location 을 통해 내가 학습시키고 싶은 cuda의 번호를 지정해주면 됩니다. <br>

\<예시\>

```python
PATH = "model.pth"
# save
torch.save(net.state_dict(), PATH)

# Load
net = Net().to(device)
net.load_state_dict(torch.load(PATH), map_location='cuda:1')
```


## 2. Single GPU에서 학습된 모델을 Multi Gpu 환경에서 불러오기
GPU를 더 확보하였을 경우 기존에 학습하던 모델을 불러와서 더 좋은 환경에서 학습시키고 싶을 수 있습니다. 그런데 막상 불러오려고 하니 load된 model의 data key point를 찾지 못한다는 에러가 납니다. 그럴 때에는 torch.module.load_state_dict를 사용하면 됩니다. 

\<예시\>
```python
PATH = "model.pth"

#Load
net = Net().to(device)
net.module.load_state_dict(torch.module.load(PATH))
```



