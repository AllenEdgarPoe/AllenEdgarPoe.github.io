---
title: Flow-based Generative Model Explained
excerpt: flow-based 생성 모델 설명 (GLOW)

categories:
    - deep-learning
tags:
    - GLOW
    - flow-based-generative
  
comments: true
use_math: true
---

Generative Model 에는 크게 3가지가 있다. 1) GAN 2) VAE 3) Flow-based Generative model. 사실 1,2 는 꽤 알고 있었는데 (사실 2도 잘 모름ㅋ) 3은 거의 모르다가 요즘 들어서 흥미가 생겨서 공부하는 중. 

*참고: https://www.youtube.com/watch?v=u3vVyFVU_lI&t=2221s*

![image](https://user-images.githubusercontent.com/43398106/147528722-1eded8b1-1142-4dcc-9635-1942749cd921.png)

## Normalizing Flow
Normalizing Flow 는 **Invertible function 을 사용하는 Probabilistic mixture model 의 일종**이다. 
* PDF(probability density function)가 invertible 하기 때문에 latent vector와 x 사이 의미있는 관계가 생긴다. 즉, z에서 x를 생성할 수 있고 그 반대도 가능하다. (sampling 이 쉽다)
* Latent vector인 z가 의미를 가진다. GAN 에서는 이 latent vector를 통제하기가 어려워서 이 latent vector space 를 찾기 위해 아주 다양한 방법을 써야 했다. 하지만 GLOW에서 보여준 대로, latent vector가 어떤 x와 매핑되는지 찾기 쉽기 때문에 두 얼굴 데이터셋을 맘껏 linear하기 explore할 수 있다. 


## Invertibe Function
 우리가 보통 생성 모델을 만들 때, latent vector $z$ 를 random Gaussian Distribution 으로 가정하고 이 z에 대한 함수 f(x)가 x데이터의 분포와 유사해지도록 가중치를 업데이트한다. 앞선 두 모델 1,2 는 실제 x 의 데이터 분포인 p(x)를 학습하진 않지만 Flow-based generative model 에서는 normalizing flow 를 활용해서 이를 학습시키고자 한다. 만약 $z = f(x)$ 이고 $f$ 가 역연산이 가능한 함수일 때, $f^{-1}(z)$ 연산을 통해 x를 구할 수 있다. 이 아이디어를 활용해서 데이터 손실도 줄이고 분포 추정도 할 수 있다. 

## Change of Variable Theorem

 Flow based generative model 을 이해하기 위한 수학적 근간이 되는 배경이다. 만약에 랜덤 변수 z가 있고 이것의 probability density function $\pi(x)$ 를 알고 있다고 치자. 이때 Density 를 구하는 식은 
 $$\begin{aligned}p_x(x) = p_z(f(x))|det Df(x)| \end{aligned}$$


* Jacobian Determinant <br>
 : Jacobian 은 매트릭스 element 하나하나가 편미분으로 이루어진 것을 의미한다. 포인트 p에 대한 Jacobian Determinant는 function f 가 포인트 p를 얼마나 어떻