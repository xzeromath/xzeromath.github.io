---
# layout: "post"
title: "BeautifulSoup 예제 (사진 다운로드)"
slug: BeauS1_image
# categories: Crawl
tag: Crawl
header:
  teaser: /assets/images/6.png
---

## 네이버에서 검색 사진을 일괄 다운로드


  <div class="input_area" markdown="1">

```python
from bs4 import BeautifulSoup
import urllib.request as req
import urllib.parse as rep
import os
```

  </div>

### quote_plus를 통해 주소를 얻는다.


  <div class="input_area" markdown="1">

```python
base = "https://search.naver.com/search.naver?where=image&sm=tab_jum&query="

quote = rep.quote_plus("아이유")
url = base + quote
print(url)
```

  </div>

  {:.output_stream}
  ```
  https://search.naver.com/search.naver?where=image&sm=tab_jum&query=%EC%95%84%EC%9D%B4%EC%9C%A0

  ```

### 폴더를 만든다. 폴더를 만드는 일반적인 루틴


  <div class="input_area" markdown="1">

```python
res = req.urlopen(url)
savePath = "./imagdown/"

try:
    if not (os.path.isdir(savePath)):
        os.makedirs(os.path.join(savePath))
except OSError as e:
    if e.errno != errno.EEXIST:
        print("폴더만들기 실패")
        raise
```

  </div>


  <div class="input_area" markdown="1">

```python
print(os.path.join(savePath))
```

  </div>


  <div class="input_area" markdown="1">

```python
soup = BeautifulSoup(res, "html.parser")

img_list = soup.select("div.img_area > a.thumb._thumb > img")

print("test", img_list)
```

  </div>

  {:.output_stream}
  ```
  test [<img alt="아이유 일본잡지 인터뷰 사진 | 카페" class="_img" data-height="493" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fcafefiles.naver.net%2F20110723_205%2Feldhel111_1311416057275CMeng_jpg%2F_dsc1592copy_eldhel111.jpg&amp;type=b400" data-width="740" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="16세 샛별 아이유(IU) “나와 너 하나되는 무대와 노래가 마냥 좋아요” (인터뷰) | 포토뉴스" class="_img" data-height="628" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5033%2F2008%2F09%2F24%2F200809221633171001_1.jpg&amp;type=b400" data-width="450" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="[HD포토] 아이유(IU), '우유빛 피부' (나의아저씨) | 포토뉴스" class="_img" data-height="1920" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5353%2F2018%2F04%2F11%2F0000326331_001_20180411174226242.jpg&amp;type=b400" data-width="1200" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="아이유 바탕화면 사진화보★ | 포스트" class="_img" data-height="1080" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fpost.phinf.naver.net%2F20150413_281%2Fkpop6627_1428915331653dLxuq_JPEG%2Fmug_obj_142891518972929787.jpg&amp;type=b400" data-width="1920" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="세해 기념 사진 투척 !!!! | 카페" class="_img" data-height="493" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fcafefiles.naver.net%2F20121231_201%2Fkyungso7_1356957992189TQ2cp_JPEG%2F2012-10-20_23%253B16%253B38.jpg&amp;type=b400" data-width="597" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="아이유 화보 모음 | 블로그" class="_img" data-height="403" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fblogfiles1.naver.net%2F20110106_283%2Fgowjyoung_1294289763489krtL7_JPEG%2F38.jpeg&amp;type=b400" data-width="304" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="아이유 금일자 인스타. | 카페" class="_img" data-height="740" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fcafefiles.naver.net%2FMjAxODAyMTdfMjUx%2FMDAxNTE4ODc2ODEzODE2.r_XPh2vRLduejB40YGKbH0gdNTGDJg5YSrDEbRwrhKQg.0pNuiY73BOy7JqhPVqderGmcqbiK8jcXqDAUmRa1OEUg.JPEG.gone1125%2F27878303_536881553364589_6231958105811320832_n.jpg&amp;type=b400" data-width="740" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="[HD포토] 아이유, '어디선가 꽃향기가 나는 느낌' (가온차트 K-POP어워즈) | 포토뉴스" class="_img" data-height="1920" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5353%2F2018%2F02%2F15%2F0000298883_002_20180215033941339.jpg&amp;type=b400" data-width="1200" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="[HD포토] 아이유(IU), ‘소주잔을 높이 들고~’ (아이유 이슬로 페스티벌2) | 포토뉴스" class="_img" data-height="864" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5353%2F2015%2F12%2F23%2F540__1450868955-46-org_99_20151224095604.jpg&amp;type=b400" data-width="540" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="[★포토]아이유, '눈에 띄는 인형 몸매' | 포토뉴스" class="_img" data-height="985" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F108%2F2017%2F12%2F02%2F0002664582_001_20171202182919286.jpg&amp;type=b400" data-width="560" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="아이유, 양갈래 머리 고등학생 화보 공개 '순수해' | 포토뉴스" class="_img" data-height="500" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F111%2F2011%2F01%2F06%2F1294274630568_1.jpg&amp;type=b400" data-width="333" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="[HD포토] 아이유(IU), '나의 라임 무선 이어폰' | 포토뉴스" class="_img" data-height="1920" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5353%2F2018%2F05%2F23%2F0000347326_001_20180523130035180.jpg&amp;type=b400" data-width="1200" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="아이유 2집 화보 | 블로그" class="_img" data-height="567" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fblogfiles3.naver.net%2F20111129_172%2Fflowerfine_1322537687895hhL78_JPEG%2FiPhone_2.jpg&amp;type=b400" data-width="850" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt='아이유, 식스팬 근육 몸매…"마초맨 아이유?" | 포토뉴스' class="_img" data-height="387" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F311%2F2011%2F04%2F14%2F1302787640216.jpg&amp;type=b400" data-width="530" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="참이슬 메이킹+ 화보!! | 카페" class="_img" data-height="900" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fcafefiles.naver.net%2FMjAxODA1MTZfOTQg%2FMDAxNTI2NDU5ODc0OTMz.IjHK_jvIwm5QnZZYXcz0fvG6D5EeKJrv8LZtwtVzXWAg.a2Djqf7Vq397H8M0HzgQuOhd5u6jaz67ZzWEYt90pf4g.JPEG.hyoda31%2FexternalFile.jpeg&amp;type=b400" data-width="600" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="각선미소녀 아이유 | 블로그" class="_img" data-height="1200" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fblogfiles1.naver.net%2F20110530_127%2Fkjutaeng3_1306691743643ar3uq_JPEG%2F1306649508_IMG_4361.jpg&amp;type=b400" data-width="800" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="[TD포토] 아이유 '한뼘 핫팬츠입고 핫한 각선미 자랑' | 포토뉴스" class="_img" data-height="839" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5129%2F2012%2F08%2F03%2F1343971713_367592.jpg&amp;type=b400" data-width="540" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt='아이유, "꿈 많은 20대, 그래도 음악이 1순위죠" | 포토뉴스' class="_img" data-height="347" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F213%2F2011%2F11%2F29%2F20111129_1322509514_12208300_1.jpg&amp;type=b400" data-width="520" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="아이유 패션/ 효리네 민박 알바 패션 | 포스트" class="_img" data-height="207" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fpost.phinf.naver.net%2FMjAxNzA3MTBfNTgg%2FMDAxNDk5NjI1ODA0MDI4.B4qLV7ccnDKlHERiDZ7Hl__lDyTv7199QKCtMfigZmIg.njzsti-DYtYaBYvRdGvKE-V7lVqLNloWNyKWcWD5h-Ug.JPEG%2FI6UXedfC391d4DcJudTB33UmGJwg.jpg&amp;type=b400" data-width="400" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="예스비와 함께한 아이유 2011 F/W 화보 | 포토뉴스" class="_img" data-height="600" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F003%2F2011%2F09%2F30%2FNISI20110930_0005223312_web.jpg&amp;type=b400" data-width="450" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt='[가온차트] 아이유, "늘씬한 각선미" | 포토뉴스' class="_img" data-height="637" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5052%2F2012%2F02%2F23%2FVi_1329987741.jpg&amp;type=b400" data-width="400" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="[HD포토] 아이유(IU), '예쁨·도도·큐트' | 포토뉴스" class="_img" data-height="1920" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5353%2F2018%2F05%2F23%2F0000347313_001_20180523125235641.jpg&amp;type=b400" data-width="1200" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="아이유 (IU) 예스비 카달로그 촬영 현장 각선미 직찍 | 블로그" class="_img" data-height="825" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fblogfiles7.naver.net%2F20110511_94%2Fpjh34091_13051154372399tDfE_JPEG%2F%25BE%25C6%25C0%25CC%25C0%25AF_%2528IU%2529_%25BF%25B9%25BD%25BA%25BA%25F1_%25C4%25AB%25B4%25DE%25B7%25CE%25B1%25D7_%25C3%25D4%25BF%25B5_%25C7%25F6%25C0%25E5_%25B0%25A2%25BC%25B1%25B9%25CC_%25C1%25F7%25C2%25EF_2.jpg&amp;type=b400" data-width="550" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="[090908] 양재 ::: KBS 제3라디오 공개방송 (직찍) | 카페" class="_img" data-height="456" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fcafefiles.naver.net%2F20090912_3%2Fmaru_kamel_1252686374786JGjyA_jpg%2F%25BE%25E7%25C0%25E7_%25BE%25C6%25C0%25CC%25C0%25AF_3_maru_kamel.jpg&amp;type=b400" data-width="684" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="아이유 | 카페" class="_img" data-height="319" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fcafefiles.naver.net%2F20120301_53%2F2167420_1330528422402Fk3fk_JPEG%2Fdownloadfile-39.jpeg&amp;type=b400" data-width="480" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="[사진]아이유,'깜찍한 자태를 뽐내며' | 포토뉴스" class="_img" data-height="1098" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F109%2F2011%2F11%2F24%2F201111241923778777_1.jpg&amp;type=b400" data-width="500" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="아이유 몸매 고민 | 블로그" class="_img" data-height="485" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fblogfiles13.naver.net%2F20111227_15%2F5v5x9kj8_1324944491206WzDPT_JPEG%2F435345.jpg&amp;type=b400" data-width="380" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="머 이쁘니까 ㅋ | 카페" class="_img" data-height="905" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fcafefiles.naver.net%2F20101219_11%2Fdongheun01_12927458405013lubN_jpeg%2F%25BE%25C6%25C0%25CC%25C0%25AF%2528iu%2529_349_dongheun01.jpeg&amp;type=b400" data-width="516" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="아이유 화보, 성숙미 물씬 ‘언제 이렇게 컸어?’[포토엔] | 포토뉴스" class="_img" data-height="704" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5033%2F2011%2F09%2F20%2F201109192335531002_1.jpg&amp;type=b400" data-width="500" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="아이유한테 꽂주고 성덕 인증한 트와이스 나연 | 포스트" class="_img" data-height="960" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fpost.phinf.naver.net%2FMjAxODA1MjhfNCAg%2FMDAxNTI3NDk4MDEzODAy.xujWrOEbBTA22i0NM627Zzc6pjXl1FanbOYjvPR9vUgg.U2fcW2JDcU5mkBCMlwNIugnTXIptsmH3krxJ9hmZ3FIg.JPEG%2FIvvOzFXpQpOyoipAOjOan9zeZl4U.jpg&amp;type=b400" data-width="960" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="[포토] 아이유, 동안의 정석 | 포토뉴스" class="_img" data-height="900" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5359%2F2018%2F05%2F23%2F0000252246_001_20180523113635817.jpg&amp;type=b400" data-width="600" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="[S포토] 아이유, '지은이의 미소' (소니) | 포토뉴스" class="_img" data-height="1921" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5401%2F2018%2F05%2F23%2F0000138670_001_20180523113041224.jpg&amp;type=b400" data-width="1200" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="'나의 아저씨' 이지은(아이유), 넘치는 팬사랑 인증…'팬질할 맛 난다' | 포토뉴스" class="_img" data-height="999" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5353%2F2018%2F04%2F19%2F0000329820_001_20180419082027227.jpg&amp;type=b400" data-width="1000" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="[포토] 아이유 '날아갈 듯한 워킹' | 포토뉴스" class="_img" data-height="1020" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F241%2F2018%2F05%2F23%2F0002789764_001_20180523115514441.jpeg&amp;type=b400" data-width="530" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="오나라·아이유·이선균 등, '나의 아저씨' 회식 현장…&quot;딱새우 까기&quot; | 포토뉴스" class="_img" data-height="748" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5353%2F2018%2F06%2F04%2F0000353974_003_20180604173442072.jpg&amp;type=b400" data-width="1000" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="아이유 수수한 셀카! 화장기 없이 가죽 잠바 입고 미모 자랑 `나의 아저씨` 흔적없이 사라진 지안 | 포토뉴스" class="_img" data-height="1199" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5469%2F2018%2F05%2F10%2F0000039737_001_20180510162643647.jpg&amp;type=b400" data-width="900" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="[포토] 아이유 '함께 들어요' | 포토뉴스" class="_img" data-height="900" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5359%2F2018%2F05%2F23%2F0000252244_001_20180523112035641.jpg&amp;type=b400" data-width="600" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="'무법변호사' 이준기, '미소만발' 아이유 간식차 인증해…&quot;달의 연인으로 맺어진 인연&quot; | 포토뉴스" class="_img" data-height="1000" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5353%2F2018%2F05%2F29%2F0000350627_001_20180529093438849.jpg&amp;type=b400" data-width="1000" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="[S포토] 아이유, '우리의 아이유' (2018 가온차트 K-POP 어워드) | 포토뉴스" class="_img" data-height="1067" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5401%2F2018%2F02%2F14%2F0000125784_001_20180214235417707.jpg&amp;type=b400" data-width="600" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="`나의 아저씨` 아이유 귀요미 셀카! 깻잎 머리가 깜찍..지안 혼자가 아님 깨닫고 새 삶 시작 | 포토뉴스" class="_img" data-height="640" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5469%2F2018%2F05%2F18%2F0000041055_001_20180518180445927.jpg&amp;type=b400" data-width="480" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="[S포토] 아이유, '터지는 미모에 심장도 터져' (소니) | 포토뉴스" class="_img" data-height="1823" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5401%2F2018%2F05%2F23%2F0000138671_001_20180523113050467.jpg&amp;type=b400" data-width="1300" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt='"친절한 지은씨" 아이유, 긴머리 미녀 | 포토뉴스' class="_img" data-height="520" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F213%2F2018%2F05%2F13%2F0001035943_002_20180513002111869.jpg&amp;type=b400" data-width="520" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="'해투' 하동균 &quot;과거 아이유 노래 '구리다' 독설, 3단고음 내 영향&quot; | 포토뉴스" class="_img" data-height="662" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F109%2F2018%2F06%2F07%2F0003798240_001_20180607080514929.jpg&amp;type=b400" data-width="530" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt='아이유, 악의적 악플러들 고소…"선처 없이 강경 대응 할 것" | 포토뉴스' class="_img" data-height="546" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5359%2F2018%2F05%2F21%2F0000251995_001_20180521144635062.jpg&amp;type=b400" data-width="597" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="[포토S] 아이유, '이 미모 실화냐' | 포토뉴스" class="_img" data-height="1350" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5453%2F2017%2F06%2F27%2F0000026998_001_20170627201701631.jpg&amp;type=b400" data-width="900" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="[포토] 아이유, ‘상큼함이 터진다’ | 포토뉴스" class="_img" data-height="900" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5540%2F2018%2F05%2F23%2F0000016974_001_20180523105457267.jpg&amp;type=b400" data-width="600" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="[포토엔HD] 아이유 ‘팬들에게 인사 빼놓지 않고’ | 포토뉴스" class="_img" data-height="799" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5033%2F2017%2F11%2F24%2F0001544464_001_20171124091740300.jpg&amp;type=b400" data-width="540" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt='아이유 악플러에 다시 뽑은 칼..."처벌할 건 해야한다" 소신 | 포토뉴스' class="_img" data-height="473" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F030%2F2018%2F04%2F21%2F0002701003_001_20180421142903274.jpg&amp;type=b400" data-width="710" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt="오나라·아이유·이선균 등, '나의 아저씨' 회식 현장…&quot;딱새우 까기&quot; | 포토뉴스" class="_img" data-height="749" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F5353%2F2018%2F06%2F04%2F0000353974_002_20180604173442053.jpg&amp;type=b400" data-width="1000" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>, <img alt='[현장포토] "헝클어도 청순"…아이유, 소녀의 감성 | 포토뉴스' class="_img" data-height="1085" data-source="https://search.pstatic.net/common/?src=http%3A%2F%2Fimgnews.naver.com%2Fimage%2F433%2F2016%2F12%2F15%2F20161215132635_lhj_5920_99_20161215133004.jpg&amp;type=b400" data-width="550" onerror="var we=$Element(this); we.addClass('bg_nimg'); we.attr('alt','이미지준비중'); we.attr('src','data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7');" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7"/>]

  ```


  <div class="input_area" markdown="1">

```python
for i, img_lis in enumerate(img_list):
#     print(img_lis['data-source'])
    fullFileName = os.path.join(savePath+str(i)+".jpg")
#     print(fullFileName)
    req.urlretrieve(img_lis['data-source'],fullFileName)
print("완료")
```

  </div>


  {:.output_traceback_line}
  ```
  ---------------------------------------------------------------------------
  ```

  {:.output_traceback_line}
  ```
  gaierror                                  Traceback (most recent call last)
  ```

  {:.output_traceback_line}
  ```
  /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/urllib/request.py in do_open(self, http_class, req, **http_conn_args)
   1317                 h.request(req.get_method(), req.selector, req.data, headers,
-> 1318                           encode_chunked=req.has_header('Transfer-encoding'))
   1319             except OSError as err: # timeout error

  ```

  {:.output_traceback_line}
  ```
  /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/http/client.py in request(self, method, url, body, headers, encode_chunked)
   1238         """Send a complete request to the server."""
-> 1239         self._send_request(method, url, body, headers, encode_chunked)
   1240

  ```

  {:.output_traceback_line}
  ```
  /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/http/client.py in _send_request(self, method, url, body, headers, encode_chunked)
   1284             body = _encode(body, 'body')
-> 1285         self.endheaders(body, encode_chunked=encode_chunked)
   1286

  ```

  {:.output_traceback_line}
  ```
  /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/http/client.py in endheaders(self, message_body, encode_chunked)
   1233             raise CannotSendHeader()
-> 1234         self._send_output(message_body, encode_chunked=encode_chunked)
   1235

  ```

  {:.output_traceback_line}
  ```
  /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/http/client.py in _send_output(self, message_body, encode_chunked)
   1025         del self._buffer[:]
-> 1026         self.send(msg)
   1027

  ```

  {:.output_traceback_line}
  ```
  /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/http/client.py in send(self, data)
    963             if self.auto_open:
--> 964                 self.connect()
    965             else:

  ```

  {:.output_traceback_line}
  ```
  /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/http/client.py in connect(self)
   1391
-> 1392             super().connect()
   1393

  ```

  {:.output_traceback_line}
  ```
  /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/http/client.py in connect(self)
    935         self.sock = self._create_connection(
--> 936             (self.host,self.port), self.timeout, self.source_address)
    937         self.sock.setsockopt(socket.IPPROTO_TCP, socket.TCP_NODELAY, 1)

  ```

  {:.output_traceback_line}
  ```
  /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/socket.py in create_connection(address, timeout, source_address)
    703     err = None
--> 704     for res in getaddrinfo(host, port, 0, SOCK_STREAM):
    705         af, socktype, proto, canonname, sa = res

  ```

  {:.output_traceback_line}
  ```
  /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/socket.py in getaddrinfo(host, port, family, type, proto, flags)
    742     addrlist = []
--> 743     for res in _socket.getaddrinfo(host, port, family, type, proto, flags):
    744         af, socktype, proto, canonname, sa = res

  ```

  {:.output_traceback_line}
  ```
  gaierror: [Errno 8] nodename nor servname provided, or not known
  ```

  {:.output_traceback_line}
  ```

During handling of the above exception, another exception occurred:

  ```

  {:.output_traceback_line}
  ```
  URLError                                  Traceback (most recent call last)
  ```

  {:.output_traceback_line}
  ```
  <ipython-input-54-37e0d183963d> in <module>()
      3     fullFileName = os.path.join(savePath+str(i)+".jpg")
      4 #     print(fullFileName)
----> 5     req.urlretrieve(img_lis['data-source'],fullFileName)
      6 print("완료")

  ```

  {:.output_traceback_line}
  ```
  /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/urllib/request.py in urlretrieve(url, filename, reporthook, data)
    246     url_type, path = splittype(url)
    247
--> 248     with contextlib.closing(urlopen(url, data)) as fp:
    249         headers = fp.info()
    250

  ```

  {:.output_traceback_line}
  ```
  /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/urllib/request.py in urlopen(url, data, timeout, cafile, capath, cadefault, context)
    221     else:
    222         opener = _opener
--> 223     return opener.open(url, data, timeout)
    224
    225 def install_opener(opener):

  ```

  {:.output_traceback_line}
  ```
  /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/urllib/request.py in open(self, fullurl, data, timeout)
    524             req = meth(req)
    525
--> 526         response = self._open(req, data)
    527
    528         # post-process response

  ```

  {:.output_traceback_line}
  ```
  /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/urllib/request.py in _open(self, req, data)
    542         protocol = req.type
    543         result = self._call_chain(self.handle_open, protocol, protocol +
--> 544                                   '_open', req)
    545         if result:
    546             return result

  ```

  {:.output_traceback_line}
  ```
  /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/urllib/request.py in _call_chain(self, chain, kind, meth_name, *args)
    502         for handler in handlers:
    503             func = getattr(handler, meth_name)
--> 504             result = func(*args)
    505             if result is not None:
    506                 return result

  ```

  {:.output_traceback_line}
  ```
  /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/urllib/request.py in https_open(self, req)
   1359         def https_open(self, req):
   1360             return self.do_open(http.client.HTTPSConnection, req,
-> 1361                 context=self._context, check_hostname=self._check_hostname)
   1362
   1363         https_request = AbstractHTTPHandler.do_request_

  ```

  {:.output_traceback_line}
  ```
  /Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/urllib/request.py in do_open(self, http_class, req, **http_conn_args)
   1318                           encode_chunked=req.has_header('Transfer-encoding'))
   1319             except OSError as err: # timeout error
-> 1320                 raise URLError(err)
   1321             r = h.getresponse()
   1322         except:

  ```

  {:.output_traceback_line}
  ```
  URLError: <urlopen error [Errno 8] nodename nor servname provided, or not known>
  ```



  <div class="input_area" markdown="1">

```python

```

  </div>


  <div class="input_area" markdown="1">

```python

```

  </div>
