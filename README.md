# ModernKoreanSubword
한국어 형태소 분석기([kiwi](https://github.com/bab2min/kiwipiepy))에서 제공하는 서브워드(subword) 학습 함수를 활용해 1920~40년에 출간된 조선/동아일보 약 190만건의 기사를 학습 후 만든 근대 한국어 토크나이저.  
예시 코드(ModernKoreansubword.ipynb)와 토크나이저 json 파일(ModernKoreanSubword.json)을 활용해 토크나이징이 가능하다.

```
from kiwipiepy import Kiwi
kiwi = Kiwi()
from kiwipiepy.sw_tokenizer import SwTokenizer
from kiwipiepy.sw_tokenizer import SwTokenizerConfig

tokenizer = SwTokenizer('./ModernKoreanSubword.json', kiwi=kiwi)

tokenizer.encode('國民新報時代에政合邦說을提唱하야日韓聯邦하기로主論하기도經하얏고')
vocab_list = tokenizer.encode('國民新報時代에政合邦說을提唱하야日韓聯邦하기로主論하기도經하얏고')
[tokenizer.id2vocab[i] for i in vocab_list]
```
