---
published: true
layout: post
title: Yolov8 train 중 보이는 SyntaxError - ‘fl_gamma‘ is not a valid YOLO argument.
description: >
  Yolov8 train 중 보였던 syntax error 해결한 내용입니다.
tags: [Project]
author: author1
canonical_url: https://halloweengemini.github.io/2024/03/28/Yolov8-train-중-보이는-SyntaxError_-fl_gamma-is-not-a-valid-YOLO-argument/
---

Wrist X-ray에서 골절을 검출하는 Research 중 Ultralytics에서 배포한 YOLOv8로 open dataset에서 학습 재현을 하려던 중 아래와 같은 오류에 부딪혔다. 

```
SyntaxError: ‘fl_gamma‘ is not a valid YOLO argument.
```

### 환경 : Pytorch 1.12.1 RTX3090

Ultralytics에서는 Pytorch를 2.0.0부터 쓰기를 권장하고 있지만, RTX3090에서 지원하는 CUDA version으로는 2.0.0 설치가 불가했다. (혹시 가능하다면 피드백 부탁드립니다..!) 


검색해도 뚜렷한 해결방법이 없던 중 중국 블로그의 글을 확인했다. 


> https://blog.csdn.net/2301_79519601/article/details/134618925

args.yaml나 train 관련 인자에서 해당 변수들이 없어 default.yaml에서 선언하는 것으로 해결했다.

결론은 ~~~/lib/python3.9/site-packages/ultralytics/cfg/default.yaml의 마지막에 세 줄을 추가하라는 것이다. 
``` python
v5loader: True
fl_gamma: 0.0
image_weights: False
```

수정했고, 이후로 학습은 정상적으로 진행되었다. 

오류 해결!

