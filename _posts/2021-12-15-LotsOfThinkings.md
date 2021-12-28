---
title: "요즘 드는 정리되지 않은 생각들 마구잡이로 적기"
excerpt: "Sparring Partner, Racist NN, Fashion AI"

categories:
   - deep-learning
tags:
   - VTON
---

## What Should I do?

CVPR 2022 submission이 드디어 끝났다. 기말고사도 끝났다. 나는 이제 다음 학기부터 박사 과정에 들어간다.. 소름.. 블로그도 팽겨치다가 이제 몇 글자 써본다. 

아래부터는 정리되지 않은, 그냥 생각나는 대로 써보는 글이다. 

---

### 1. Utilizing Sparring Partner in Deep Learning? 

알파고 보다 더 뛰어난 성능을 보였던 **AlphaGo Zero** 는 기존 AlphaGo 모델 두 개가 처음 학습할 때부터 서로 대결하게 하여 서로를 강화시키는 모델이다. 이렇게 두 개의 넷트워크 를 서로 경쟁시켜 모델의 성능을 높이는 것은 딥러닝에 많이들 사용한다. 
 * 가장 대표적인게 역시 GAN 모델이다. Discriminator 와 Generator 두 네트워크가 서로가 서로를 속이도록 학습되었고, 기존 VAE 모델보다 훨씬 뛰어난 성능을 보였다. 
 * Adversarial Attack and Defense (PGD): 뉴럴 네트워크에 아주 적은, 사람 눈으로는 인지할 수 없는 noise를 넣어서 네트워크를 속이는 모델이다. 그런데 이런 공격 방법에 대한 방어를 할 때도 Sparring Parter 같은 개념을 쓴다. 특정 iteration을 반복해서 모델을 속일 수 있는 noise를 만들면, 그 noise가 씌인 이미지에 대해 올바른 label을 집어넣어 다시 네트워크가 제대로 학습할 수 있도록 하는 구조다. 
 * 이렇게 Sparring Partnership 을 다른 딥러닝 분야에서 활용한다면 성능을 더 높일 수 있지 않을까?
---

### 2. Racist NN 

훌륭한 걸 넘어 미친 성능을 보여주는 OpenAI의 CLIP 모델. 기존 ICLR 처럼 Contrastive Learning 을 사용해서 Vision 과 text 를 이어준 multi modality network 라고 할 수 있다. 그런데 https://openai.com/blog/multimodal-neurons/ 이 글을 보다가 재미있는 내용을 발견했다. <br>

> 우리 모델은, 인터넷에서 조심해서 긁어모은 데이터로 학습했는데도 불구하고, 꽤 많은 바이어스 와 연관성을 그대로 답습했다. CLIP이 가진 연관성은 특정 개인이나 집단을 비하 하는 등의 결과로 이어질 수 있다. 

사람이 가진 데이터로 학습된 인공지능은 사회적 bias도 함께 답습할 수 밖에 없다는 것이다. 예를 들어서 CLIP 의 #1895 뉴런은 "Middle East" 와 "terrorism" 에 대해 동시에 반응했다. #1257 뉴런은 "Dark-skinned People" 과 "Gorillas" 에 대해 동시에 발현했고 #395 뉴런은 "immigration"과 "Latin America" 를 동시에 인식했다. 

<img src="https://allenedgarpoe.github.io/assets/images/channel-1895.png" width="180">
<img src="https://allenedgarpoe.github.io/assets/images/channel-1257.png" width="180">
<img src="https://allenedgarpoe.github.io/assets/images/channel-395.png" width="180">
      <br>*왼쪽부터 #1895, #1257, #395*
<br>

Zero-shot으로 학습시켰든, fine-tuning 을 하든 이렇게 딥러닝이 인간이 가진 편견을 답습하지 못하게 막는건 힘들다. 데이터를 아무리 정제시켜도 이러한 Challenge를 극복하는데는 한계가 있다. 이게 생각보다 좀 심각한 문제인게, 인공지능을 상품화 해서 실생활에 쓰일 때 사람은 '편견' 이 '편견' 이라는 것을 인지하고 있지만, 인공지능은 이 '편견' 또한 귀중한 정보이기 때문에 이를 활용할 것이기 때문이다. 예를 들어서, Face App 중에 메이크업을 해주는 어플이 있는데 백인, 황인은 제대로 사람으로 인식하지만 흑인은 다른 동물로 분류된다면? 혹은 인종, 성별 등의 차이로 어떤 집단에는 서비스가 제대로 제공되지 않는다면? 그냥 기분 나빠서를 넘어서서 데이터 에 따라서 아예 활용방안이 달라질 수 있는 것이다. 

생각해보니 NN Attack 중에도 **Hidden Trigger Backdoor Attacks** (https://arxiv.org/pdf/1910.00033.pdf) 라고 하는 비슷한 어택이 있다. 이건 인위적으로 뉴럴 네트워크에 Corrupted Data 를 넣거나 혹은 잘못 Label 이 된 데이터를 넣어서 뉴럴 네트워크 학습에 전체적으로 영향을 미치는 것이다. 사실 이번 CVPR 2022 에 제출했던 논문도 이 아이디어 사용해서 여러 실험 해보다가 얻어걸린건데, 시간이 허락한다면 꼭 실험을 다시 해보고 싶다. 

---

### 3. Fashion A.I.
https://github.com/ayushidalmia/awesome-fashion-ai

https://github.com/minar09/awesome-virtual-try-on

와 진짜 옛날부터 하고 싶었던 연구 이제서야 찾았다. 어떻게든 패션이랑 A.I.랑 엮어서 실제 산업에 사용할 수 있도록 만들고 싶었는데 이제서야..! 관련 분야를 찾았음. 특히 저 Virtual Try On 이란 분야가 CVPR 2018 때 처음 발표된 태스크 인데 사람 얼굴이랑 옷 을 보여주면 그 사람이 해당 옷을 입고 있도록 하는 태스크다. 지금 보니까 비디오, 텍스트 에서도 쓰이고 또 3D image reconstruction 에서도 쓰이는 거 같다. 차후에 이쪽 더 논문 보고 싶다. 