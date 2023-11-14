---
title: "Modularization(모듈화)"
excerpt:
  "프로그래밍에서 모듈이란 소프트웨어 묶음을 만들고, 코드를 네임스페이스로써 구분하는 메커니즘입니다.
  그리고 프로그래밍 언어(자바 제외)에서는 모듈을 기능(함수)별로 나누거나 모아놓은 파일로써, 필요할 때마다 가져다 쓸 수 있도록 재사용하기 위한 것으로 정의합니다.
  보통 파이썬으로 데이터 분석 등의 업무나 대회를 참여하면 하나의 jupyter notebook으로 파일을 형성할텐데,
  오늘은 이러한 파일을 모듈화 후 패키징하는 과정을 포스팅해보도록 하겠습니다."

categories:
      - categories4

tags:
      - [Module, Modularization, Argparse]

Permarlink: /categories4/Parquet

toc: true
toc_sticky: true

date: 2023-10-17 
last_modified_at: 2023-10-17
---

![modularization_thumbnail](https://github.com/hoon-bari/hoon-bari.github.io/assets/121400054/fbe74f61-a92c-448f-96c5-f2940d52951d)

Github에 올라온 각종 코드들을 보면 (파이썬을 기준으로) jupyter 파일로 된 코드도 많지만,  
보통 py파일로 각 함수로 나눠진 모듈화된 파일들이 올려진 것을 볼 수 있습니다.  
이렇게 모듈화를 함으로써 여러 이점을 얻을 수 있는데, 오늘은 이러한 모듈화의 이점을 알아보고 동시에 모듈화를 하는 과정을 포스팅해보려 합니다.  
<br>

### 1. Module의 정의

---

일반적으로 모듈이란 보다 작고 이해할 수 있는 단위로 나누어진 것으로 본체에서 분리되어 작은 부분으로 유기적으로(기능별로) 구성되어 있다가,  
필요할 때 마다 본체에 합류하여 그 기능을 수행할 수 있는 것을 말합니다. 보통 그 자체로 완전한 기능을 수행할 수 있는 독립된 실체로 봅니다.  
이러한 모듈은 Unity(한 가지 일만 수행), Smallness(간단 명료), Simplicity(단순성), Independency(독립성) 등의 특성을 가집니다.

<br>

### 2. 모듈화를 하는 이유

---

모듈화는 거대한 문제를 작은 조각의 문제로(즉, 하나의 전체를 여러 모듈로) 나누어 다루기 쉽도록 하는 과정이며,  
이를 통해 수정이 용이하게 하고, 재사용성이 용이하게 하며, 유지관리가 쉽도록 합니다.  
이 때 모듈간 호환성을 고려할 필요가 있습니다. 즉, 표준화가 중요합니다.

<br>

### 3. 프로그래밍에서의 모듈

---

이러한 모듈과 모듈화를 프로그래밍의 관점에서 보면, 모듈은 소프트웨어 묶음을 만들고 코드를 네임스페이스로써 구분하는 메커니즘을 말합니다.  
좀 더 구체적으로 자바를 제외한 다른 프로그래밍 언어와 같은 관점에서 모듈은 기능(함수)별로 여럿을 하나로 정리/모으거나 분할하는 것을 의미합니다.  
(자바의 경우에는 패키지는 여러 클래스들의 모음이고 모듈은 여러 패키지들의 모음을 의미합니다.)  
이렇게 정리한 모듈을 파일 단위로 정의하여 두고, 이를 가져오는(import)방식을 통해 큰 기능(어플리케이션)을 구동합니다.

<br>

### 4. jupyter 파일 모듈화([Github 링크](https://github.com/hoon-bari/SKKU_KDT_2th_Mini_project6))

---

하나의 jupyter파일을 모듈화하였습니다. 이 파일은 약 50만개의 문장을 학습한 한영번역기 코드입니다. [notebook 코드 링크](<https://github.com/hoon-bari/SKKU_KDT_2th_Mini_project6/blob/main/notebook/Mini_Project_6_Make_Translator(seq2seq_with_attention%2C%20Kor%20to%20Eng).ipynb>)  
학습은 AI hub의 한국어-영어 번역 말뭉치 중 3개 파일(구어체(1), 구어체(2), 대화체) 총 50만 문장을 대상으로 했습니다.  
(학습 데이터는 바꿔주셔도 무방합니다.)

#### (1) Argparse

모듈화를 실행하기 전에, 우선 Argparse라는 모듈에 대해 알아보겠습니다. [공식문서 링크](https://docs.python.org/ko/3/library/argparse.html#module-argparse)  
Argparse는 파이썬 버전 3.2부터 추가된 모듈로,  
Command Line Interface(CLI)를 만들고 command line에서 script를 실행할 때 인자를 parsing하는데 사용되는 도구입니다.  
다시 말해서 python에서 명령어로 스크립트를 실행할 때, 스크립트에 전달되는 명령이나 값을 정리하고 분석할 수 있는 도구입니다.  
이 모듈을 활용하면 스크립트를 사용할 때 어떤 선택 사항을 사용할 지 정할 수 있고, 그 선택사항을 스크립트 내에서 활용할 수 있습니다.  
그를 통해 스크립트와 사용자 간 원활한 상호작용이 가능하며, 스크립트를 다양한 방식으로 실행할 수 있게 됩니다.  
Argparse를 사용하는 법은 공식 문서를 참고해주세요!

여기서는 번역기를 train하는 train mode, 그리고 번역을 실행하는 test mode로 나누도록 하겠습니다.  
tokenize할 때 필요한 batch_size와, train할 때 필요한 epoch를 argument로 추가하겠습니다.

```python
def get_args():
  parser = argparse.ArgumentParser(description='This program was made for translation Kor to Eng')

  parser.add_argument('--mode',
                help='train 또는 test mode를 지정해주세요',
                required=False,
                type=str,
                default='test')

  parser.add_argument('--batch-size',
                help='train 시에는 원하는 batch_size를 지정해주세요',
                required=False,
                type=int,
                default=256)

  parser.add_argument('--epochs',
                help='train 시에는 원하는 epochs를 지정해주세요',
                required=False,
                type=int,
                default=10)
```

<br>
mode가 train이면, 입력받은 batch size와 epoch를 통해 학습을 실행할 수 있도록 합니다.

```python
if opt.play_mode == 'train':
  BATCH_SIZE = opt.batch_size
  EPOCHS = opt.epochs
```

<br>

#### (2) configparser

위에서 설명한 argparse가 파일 시작시 명령행 인자를 처리하고 스크립트 동작을 제어하는데 사용된다면,  
configparser는 미리 정한 설정을 저장하고 읽어오는데 사용됩니다.  
보통 config.ini라는 파일을 만든 다음, 그 안에 파일 실행에 필요한 설정을 아래와 같이 미리 정해놓습니다.

```python
[Model]
hidden_dim = 256
embedding_dim = 128
```

<br>
그리고 이렇게 정한 설정을 불러오려면 아래와 같이 코드를 작성하면 됩니다.

```python
config = configparser.ConfigParser()
config.read('config.ini')

HIDDEN_DIM = config.getint('Model', 'hidden_dim')
EMBEDDING_DIM = config.getint('Model', 'embedding_dim')
```

<br>

#### (3) Directory

하나의 notebook 파일을 모듈화한다고 가정하면, 아래와 같은 Directory가 완성됩니다.

```python
Modularization
 ┣ Data
 ┃ ┣ 1_구어체(1).xlsx
 ┃ ┣ 1_구어체(2).xlsx
 ┃ ┣ 2_대화체.xlsx
 ┃ ┗ 한영번역_타켓문장.csv
 ┣ Model
 ┣ Modeling
 ┃ ┣ Modeling.py
 ┃ ┗ translate.py
 ┣ Preprocessing
 ┃ ┗ Preprocessing.py
 ┣ app.py
 ┗ config.ini
```

<br>
여기서 Data에는 학습 데이터 그리고 번역할 타겟 데이터가 들어가며, Preprocessing은 위 Data에 있는 파일을 정제할 모듈이 있는 부분입니다.  
그리고 Modeling은 train과 관련된 model 부분, 그리고 번역과 관련한 translate 모듈이 포함되며,  
Model에는 이렇게 학습한 모델이 저장됩니다. 나중에 학습을 안하고 번역만 할 경우에는 이 Model 폴더에서 모델을 불러오게 됩니다.  
(학습한 모델을 다시 학습하고 싶다면 코드를 살짝 수정해서 모델을 불러온 후 거기에 fine-tuning하면 됩니다.)  
github에는 용량 때문에 model 폴더만 만들고 안에 temp파일을 넣었습니다. 로컬이나 colab 등 환경에서 실행할때 만들어주세요.

preprocessing의 경우 데이터를 불러와서 모델에 맞게 전처리하는 부분을 모듈화하였으며,
Modeling.py의 경우는 번역에 Seq2Seq와,  
나중에 translate시 encoder, decoder input 및 output의 원활한 변경을 위해 Encoder, Decoder를 모듈화하였습니다.
그리고 translate.py는 notebook의 translate 함수 부분을 모듈화하였으며 이 모든 부분을 실행하기 위한 app.py(main.py)를 만들었습니다.
마지막에 번역된 문장과 bleu score가 나오도록 했는데, 여러분이 원하시는대로 바꾸시면 됩니다.

notebook 파일의 흐름을 따라가며 모듈화된 파일을 확인해본다면, 여러분의 파일도 잘 모듈화할 수 있을거라 생각합니다.

<br>

#### (4) if \_\_name\_\_ = "\_\_main\_\_"

추가로 app.py 파일을 보면 if \_\_name\_\_ = "\_\_main\_\_"이라는 부분이 있고 거기서 mode가 나눠지도록 해놨는데,  
이것은 모듈을 import한 경우가 아니라 interpreter에서 직접 실행한 경우만 if \_\_name\_\_ = "\_\_main\_\_"이하의 코드를 실행하라는 의미입니다.

파이썬 공식 문서에는 \_\_name\_\_ 내장변수를, "must be set to the fully-qualified name of the module.  
This name is used to uniquely identify the module in the import system."라고 정의하고 있습니다.  
즉, 모듈의 독자적인 이름을 담고 있습니다. 만약 아래와 같은 함수를 실행한다고 하면,

```python
//excuteThisModule.py
def func():
    print("function working")

if __name__ == "__main__":
    print("직접 실행")
    print(__name__)
else:
    print("임포트되어 사용됨")
    print(__name__)
```

<br>
직접 실행을 했을 때는 \_\_main\_\_이 출력되어 나올 것이고, import했다면 executeThisModule이 출력되어 나올겁니다.  
어떤 스크립트 파일이든 파이썬 interpreter가 최초로(직접) 실행한 스크립트 파일의 \_\_name\_\_ 에는 \_\_main\_\_이 들어갑니다.  
즉, 이는 파일의 시작점을 의미합니다.  
따라서, app.py에 if \_\_name\_\_ = "\_\_main\_\_"을 추가한 이유는 이 파일이 프로그램의 시작점이 맞는지를 판단하기 위해서입니다.  
다시 말해서, 파일이 메인 프로그램으로 사용될 때와 모듈로 사용될 때를 구분하기 위한 용도입니다.

<br>

### 5. 정리

---

이상으로 모듈화에 대한 설명과, 제가 과거에 수행했던 미니 프로젝트의 notebook 및 모듈화 파일도 함께 살펴보았습니다.  
보통 jupyter 파일 자체를 사용하지 않고 모듈화해서 실행하므로, 모듈화에 대해 잘 알아두어야합니다.  
그리고 argparse와 configparser도 매우 유용하므로 꼭 알아두시기 바랍니다.  
다만 모듈화에 정답은 없고, 업무를 수행하는 곳마다 방식이 다를 수 있으므로 어떻게 모듈화를 하는구나 정도만 알고 가면 좋을 듯 합니다.

<br>

#### Reference

[① http://www.ktword.co.kr/test/view/view.php?m_temp1=2226](http://www.ktword.co.kr/test/view/view.php?m_temp1=2226)  
[② https://github.com/Rndns](https://github.com/Rndns)  
[③ https://medium.com/@chullino/if-name-main-%EC%9D%80-%EC%99%9C-%ED%95%84%EC%9A%94%ED%95%A0%EA%B9%8C-bc48cba7f720](https://medium.com/@chullino/if-name-main-%EC%9D%80-%EC%99%9C-%ED%95%84%EC%9A%94%ED%95%A0%EA%B9%8C-bc48cba7f720)  
[④ https://velog.io/@mjk3136/if-name-main%EC%9D%80-%EC%99%9C-%ED%95%84%EC%9A%94%ED%95%9C%EC%A7%80%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90](https://velog.io/@mjk3136/if-name-main%EC%9D%80-%EC%99%9C-%ED%95%84%EC%9A%94%ED%95%9C%EC%A7%80%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90)
