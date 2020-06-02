---
# layout: 'single_math'
#post
title: Youtube 파일 다운로드
date: 2020-03-15
categories: 업무자동화
tag: Python
#AWS,Computer,Crawl,Docker,Python,Math,Django,Javascript,Jupyter,Excel,Etc,Matplotlib
slug:  
---
## 요구사항
- Youtube의 파일을 다운로드 함.
- https://github.com/nficano/pytube 참고

## 코드

```python

from pytube import YouTube
yt = YouTube('유튜브 주소') # 유튜브 영상 URL 입력
# yt.streams \ # 해당 URL의 영상 스트림을 리스트로 가져온다
#     .filter(progressive=True, file_extension='mp4') \ # 프로그레시브 방식의 인코딩, 파일 포맷은 MP4
#     .order_by('resolution') \ # 영상 해상도 순으로 정렬
#     .desc() \ # 내림차순 정렬
#     .first() \ # 가장 첫 번째 스트림(가장 고화질)
#     .download() # 다운로드, 매개변수로 다운로드 경로를 지정할 수 있음

# print(yt.streams)

print(yt.streams.filter(progressive=True, file_extension='mp4').order_by('resolution').desc())

yt.streams.filter(progressive=True, file_extension='mp4').order_by('resolution').desc().first().download()
```

