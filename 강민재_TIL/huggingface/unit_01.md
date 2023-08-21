# Introduction

# Introduction to Deep Reinforcement Learning

## 강화학습이란 무엇인가?

Deep Reinforcement Learning은 agent가 environment 내에서 특정한 actions를 수행하고 결과를 확인하면서 어떤 behave를 할 지를 학습하는 기계학습의 한 분야이다.

`Stable-Baselines3` Libary

- https://stable-baselines3.readthedocs.io/en/master/

### 강화학습의 정의

> Reinforcement learning is a framework for solving control tasks (also called decision problems) by building agents that learn from the environment by interacting with it through trial and error and receiving rewards (positive or negative) as unique feedback.
> 

## 강화학습 프레임워크

### 강화학습 과정 (RL Process)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ad86317b-58a8-4f91-a177-180b198a664d/Untitled.png)

강화학습의 목표는 expected return라고 불리는 누적 보상(cumulative reward)을 최대화하는 것이다.

### 마르코프 속성

RL 과정은 마르코프 결정 과정(MDP)이라고 불린다. 이는 다음 행동을 결정할 때 과거의 모든 행동이 아닌, 현재의 상태만을 고려한다는 것이다.

### 관찰과 상태 (Observations/States)

상태(state)는 state of the world에 대한 완전한 설명을 의미한다. 반면 관찰(observation)은 state의 일부를 의미한다. 예를 들어, 체스 게임에서는 환경에 대한 state를 얻을 수 있다. 체스판 전부를 한 번에 볼 수 있기 때문이다. 반면 슈퍼 마리오 게임에서는 한 번에 얻을 수 있는 정보는 환경 전체가 아닌 그 일부이다.

### Action Space

환경 내에서 취할 수 있는 모든 가능한 행동을 의미한다. 이산적일 수도 있고, 연속적일 수도 있다. 슈퍼 마리오 게임에서는 좌, 우, 점프와 숙이기의 네 가지 행동만이 가능하다. 즉 유한(finite, discrete)한 행동만을 할 수 있다. 반면 자율 주행 에이전트의 경우 핸들을 몇 도를 틀 것인지 등에 대한 무한하고 연속적인 행동을 취할 수 있다.

### 보상과 할인

에이전트에게 주어지는 유일한 피드백인 보상은 RL의 근본이다. 보상 덕분에 에이전트는 행동이 좋은 것인지 나쁜 것인지를 결정할 수 있다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8a873176-686d-4535-8d60-5e147cae5345/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3d98b284-02c6-4b06-bbeb-937a14d6a015/Untitled.png)

현실에서는 위와 같이 보상을 계산할 수 없는데, 즉각적인 보상의 경우 장기적인 보상에 비해서 발생할 가능성이 높고 예측이 쉽기 때문이다. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c8bfc650-1dae-4844-85b7-b7df7b482482/Untitled.png)

위와 같은 상황을 생각해보자. 고양이 주변에 더 많은 치즈가 있지만, 쥐(agent)는 자신 근처에 있는 치즈를 선택할 것이다. 고양이 근처로 갈 수록 위험하기 때문에 보상에 할인(discount)가 적용된다. 할인율은 $\gamma$로 나타낸다. 감마가 클수록 할인은 작고, 이는 장기적인 보상에 더 많이 신경쓴다는 것을 의미한다. 감마가 작으면 할인이 크고 단기적인 보상에 더 큰 비중을 두겠다는 의미이다. 따라서 할인을 적용한 누적 보상은 위와 같이 나타낼 수 있다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c472dbe1-ab0d-45f7-8471-ddcd3bd841ac/Untitled.png)

## 태스크 종류

### Episodic task

이 경우 시작 지점과 끝나는 지점(terminal state)가 존재한다. 이는 하나의 에피소드(상태, 행동, 보상과 새로운 상태의 리스트)를 만든다. 

### Continuing task

종료 조건 없이 영원히 이어지는 경우도 있다. 이 경우 에이전트는 최선의 결정을 함과 동시에 환경과 상호작용을 해야 한다. 예를 들어 자동으로 주식을 매매하는 에이전트는, 시작과 종료 상태가 없다. 에이전트는 그저 우리가 그만하라고 할 때까지 계속해서 작동한다. 

## Exploration/Exploitation trade-off

Exploration은 임의의 행동을 하며 환경에 대한 정보를 얻는 것을 의미한다. Exploitation은 가지고 있는 정보를 바탕으로 보상을 최대화하기 위해 행동하는 것을 의미한다. RL의 목표는 누적 보상을 최대화하는 것인데, 여기서 우리는 흔히 함정에 빠지게 된다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f8de474e-ba96-4a85-a0a2-912be01b4d9a/Untitled.png)

위와 같은 환경의 게임에서 쥐(agent)는 작은 치즈를 무한히 얻을 수 있다. 하지만 미로의 꼭대기 부분에는 어마어마한 양의 치즈가 있다. 만약 exploitation에만 집중한다면, 에이전트는 거대한 치즈에 절대 도달하지 못한다. 비록 양은 적지만, 그 대신에 가까이 있는 보상만을 계속 선택할 것이다.

하지만 에이전트가 약간의 exploration을 한다면, 엄청난 보상을 발견할 것이다. 이를 exploration / exploitation trade-off라고 부른다. 얼마나 환경을 탐험할 것인지, 그리고 얼마나 알고 있는 정보를 바탕으로 행동을 취할 것인지에 대한 균형을 잘 맞춰야 한다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/336840eb-f3ed-4930-b37c-3dca930d9999/Untitled.png)

이해를 위해서 일상 생활의 에시를 한번 보자. 항상 가던, 적당히 맛있는 레스토랑을 갈 것인가? 아니면 새로 오픈한, 맛이 어떨지는 모르지만 굉장한 맛을 선사할 지도 모를 레스토랑에 갈 것인가? 항상 가던 곳에 간다면 엄청난 레스토랑을 알게 될 기회를 영영 놓치겠지만, 새로운 레스토랑에 갔다가 괜히 시간과 돈을 낭비할 위험을 감수해야 할 수도 있다!

## 강화학습 문제에 대한 두 가지 접근법

### 정책 $\pi$: 에이전트의 뇌

Policy $\pi$는 에이전트의 뇌이다. 이는 주어진 상태에 어떤 결정을 할 것인가에 대한 함수이다. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e2f1f735-11a7-4a3b-b5bd-c7db95328a7f/Untitled.png)

에이전트가 최적의 정책인 $\pi^{*}$를 찾게 하기 위한 두 가지 접근법이 있다.

- 직접적으로 어떤 행동을 취해야 할 지 알려주기, 정책 기반 방법(policy-based methods)
- 간접적으로 어떤 상태가 더욱 가치 있는지를 가르쳐주고 가치있는 상태에 이르는 행동을 취하게 하기, 가치 기반 방법(value-based methods)

### 정책 기반 방법

결정적(deterministic) 정책은 주어진 상태에 대해 항상 같은 행동을 취한다.

$$
a =\pi(s)
$$

확률적(stochastic) 정책은 행동에 대한 확률 분포를 내어놓는다.

$$
\pi(a|s)=P[A|s]
$$

### 가치 기반 방법

가치 함수는 그 상태와 기대되는 가치를 매핑한다. 상태의 가치(value of a state)는 해당 상태에서 시작해서, 정책대로 행동할 때 예상되는 할인된 결과(expected discounted return)이다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c5201214-5275-41c0-a882-cf494f0e7dc2/Untitled.png)

## 강화학습에서 “Deep”이 갖는 의미

강화학습 문제를 풀이하는 데, 심층 신경망 기술을 활용한다는 의미이다. 예를 들어 가치 기반 알고리즘은 Q-Learning과 Deep Q-Learning에 대해서 배우며 그 차이를 알 수 있다.