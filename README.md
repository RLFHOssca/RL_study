# RL_study

안녕하세요!! RLHF 그룹 리드를 맡게 된 손기훈입니다.

## 선수 지식

저희의 목표는 LLama 모델의 저조한 한국어 성능을 개선해보는 것입니다 😄
LLama 모델의 학습 데이터에 한국어 데이터의 절대적인 양이 적기도 하지만, 양질의 한국어 데이터로 학습 시키더라도 만족스럽지 못한 성능을 보여왔습니다.
저는 이 문제를 RLHF를 통해 해결이 가능한지 확인해보고 싶습니다.

우선 저희 프로젝트를 진행하기에 앞서, 몇 가지 준비 사항이 필요합니다.

### 강화 학습 스터디

강화 학습은 기존의 인공지능 학습 방법론과는 다른 구조를 가지고 있습니다. 따라서, 저희가 프로젝트를 진행하기에 앞서 스터디가 필요하다고 판단됩니다.

학습 리소스는 아래와 같습니다.

[FreeCodeCamp Org - Reinforcement Learning](https://youtu.be/ELE2_Mftqoc)

[Stanford CS234 - Reinforcement Learning](https://youtu.be/FgzM3zpZ55o)

[pytorch tutorial - Reinforcement Learning](https://pytorch.org/tutorials/intermediate/reinforcement_q_learning.html)

[Hugging Face Course - Reinforcement Learning](https://huggingface.co/learn/deep-rl-course/unit0/introduction)

### PEFT

저희의 대상 모델은 llama2 - 7b, 13.5b 모델이 될 것입니다. 7b 모델의 경우 제일 작은 모델이지만 역시 단일 기기에서 전체 파라미터를 파인 튜닝하는 것은 불가능에 가깝습니다. (fp32일 경우 모델의 크기만 28Gib..) 
따라서 Lora를 통한 학습이 필수 불가결합니다. 저희는 허깅페이스의 PEFT 라이브러리를 사용할 예정입니다.

[Lora 논문리뷰](https://www.youtube.com/watch?v=BJqwmDpa0wM)

[PEFT 튜토리얼](https://huggingface.co/docs/peft/index)

### 한국어 llama2 모델

---
## 방법론
이 다음으로는 제가 생각하는 RLHF 방법론에 대한 아이디어를 말씀드리겠습니다. 이 부분 역시 자유롭게 얘기해주시면 좋겠습니다!

### 1. 매뉴얼한 방식
gradio를 통해 허깅페이스에 모델을 배포한 후 커뮤니티에 홍보하여 Ossca 참여하시는 분들의 도움을 받는 방법입니다.

a. llama2 모델의 생성 답변들 여러 개를 제시하고 그 중 가장 나은 답변을 평가자에게 선택하도록 함
b. 마음에 드는 답변이 없을 시, 직접 답변 제안.

### 2. Distil(?) 한 방식

openai의 chatgpt가 저희가 만든 모델의 답변을 평가하게 하여 그 답변과 평가를 토대로 RLFH 시도.

위의 두 가지 방식을 활용하여 RLHF를 진행하고자 합니다. 많은 의견 주시면 감사하겠습니다!

---
