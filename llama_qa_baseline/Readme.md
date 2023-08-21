# Lora llama

제가 예전에 데이콘 할 때 llama를 가져와 finetuning 하여 썼을 때의 코드입니다. 기본적으로 데이터셋은 바꿔야 합니다:D

제가 올려드리는 코드는 그냥 peft로 Lora 학습을 할 때 가독성이 편하다는 것 이외에는 큰 장점은 없고 레퍼런스랑 크게 다른 점도 없으니, 

자세한 사항은 레퍼런스 코드를 참고하시면 될 것 같습니다!!

이 코드에서 바꿔야 할 부분 :

* 모델 : 모델은 한국어 llama2-7b 모델을 갖고와서 사용하셔야 합니다.
* 데이터 : 한국어 QA 데이터셋을 사용하셔야 합니다.

## 권장드리는 workflow

1) 파인튜닝 없이 QA 돌려보기
2) 파인튜닝 이후에 QA 돌려보기
3) 결과 비교 해보기
   
Generative QA에서 사용하는 metric은 보통 BLEU, ROGUE-L, SMS, METEOR, BERTscore 등이 있습니다. 다만 BERTscore는 성능은 좋지만 자원이 모자랄 가능성이 큽니다. 유의하시길 바랍니다.

## Reference

[PEFT_llama_training](https://www.mlexpert.io/machine-learning/tutorials/alpaca-fine-tuning)

[llama_inference](https://www.mlexpert.io/machine-learning/tutorials/alpaca-and-llama-inference)


