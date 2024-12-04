# ModernKoreanSubword: 근대 국한문혼용체 서브워드 토크나이저

이 레포지토리는 1900-1940년대 한국의 근대 신문과 잡지 자료를 활용하여 학습된 서브워드 기반 형태소 분석기를 제공합니다. kiwipiepy의 sw_tokenizer를 활용하여 국한문혼용체 텍스트를 효과적으로 분석할 수 있도록 설계되었습니다.

## 주요 특징

- 한국사데이터베이스의 근현대잡지자료, 조선일보, 동아일보 등 약 230만건의 텍스트로 학습
- 한자어와 옛한글이 혼재된 근대 텍스트에 최적화
- vocab_size 32000/48000/64000 세 가지 버전의 토크나이저 제공

## 데이터

- `paragraph_list.pkl.bz2`: 학습에 사용된 전체 텍스트 데이터 (압축파일). 용량 문제로 [링크](https://drive.google.com/file/d/1LzD9zL2p93sMGTnT-sK9fiMgqhsyzTeE/view?usp=sharing)에서 다운 가능.
- `chosun_1920_1945_sample.xlsx`: 조선일보 데이터 샘플

## 사용 방법

주요 노트북 파일:
- `ModernKoreanSubword.ipynb`: 토크나이저 사용 예시와 성능 평가
- `ModernKoreanSubword_Train.ipynb`: 전체 학습 과정
- `ModernKoreanSubword_Train_Sample.ipynb`: 샘플 데이터를 활용한 학습 예시

## 학습된 토크나이저

`tokenizer` 디렉토리에서 다음 세 가지 버전의 토크나이저를 제공합니다:
- vo32000_tokenizer.json
- vo48000_tokenizer.json  
- vo64000_tokenizer.json

## 참고 문헌

본 연구와 관련된 논문: "(발간예정) 근대 국한문혼용체 자료 서브워드 기반 형태소 분석기의 설계와 적용"

```
from kiwipiepy import Kiwi
kiwi = Kiwi()
from kiwipiepy.sw_tokenizer import SwTokenizer
from kiwipiepy.sw_tokenizer import SwTokenizerConfig

tokenizer = SwTokenizer('./ModernKoreanSubword/tokenizer/241112_vo32000_tokenizer.json', kiwi=kiwi)

# 국민신보시대(國民新報時代)에정합방설(政合邦說)을제창(提唱)하야일한연방(日韓聯邦)하기로주론(主論)하기도경(經)하얏고
tokenizer.encode('國民新報時代에政合邦說을提唱하야日韓聯邦하기로主論하기도經하얏고')

# 토크나이징 함수 정의
def tokenize(sentence):
  vocab_list = tokenizer.encode(sentence)
  return [tokenizer.id2vocab[i].lstrip('##') for i in vocab_list] # 서브워드 표기('##') 제거

tokenize('國民新報時代에政合邦說을提唱하야日韓聯邦하기로主論하기도經하얏고')

```
