---
title: "python_tips"
date: 2020-05-07 11:23 -0400
categories: jekyll update
---

Jupyter Notebook 기준으로 작성하여 차이가 있을 수 있음.

1. 패키지 설치

cmd> pip install _packagename_

2. 여러 개 output을 한 번에 보는 방법

```python
from IPython.core.interactiveshell import InteractiveShell
InteractiveShell.ast_node_interactivity = "all"
```

3. 커서 여러 개 만들기

Ctrl + 원하는 위치 클릭
* spyder에서는 적용되지 않음

4. Jupyter Notebook pdf 저장

MikTex를 설치하고, 추가 패키지들까지 설치했는데도 불구하고 <br>
File - Download as - PDF via LaTex(.pdf)에서 오류가 발생할 때 pdf로 저장하는 방법 <br>
"nbconvert failed: PDF creating failed, captured latex output: <br>
 Failed to run "xelatex .\notebook.tex -quiet" command:" <br>
 
 1) File - Download as - HTML(.html)로 저장하고 HTML 파일을 연다
 2) '메뉴 - 인쇄' 혹은 ' Ctrl + P'로 인쇄창을 띄운다
 3) '대상'에서 'PDF로 저장'으로 선택하고 저장하면 완료!
