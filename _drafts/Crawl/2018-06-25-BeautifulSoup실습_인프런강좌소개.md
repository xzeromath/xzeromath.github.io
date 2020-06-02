---
# layout: "post"
title: "BeautifulSoup 예제 (인프런 사진 제목 다운로드)"
slug: BeauS1_image2
# categories: Crawl
tag: Crawl
header:
  teaser: /assets/images/7.png
---
## 인프런 추천강좌의 사진과 제목을 저장


  <div class="input_area" markdown="1">

```python
from bs4 import BeautifulSoup
import urllib.request as req
import urllib.parse as rep
import os
```

  </div>


  <div class="input_area" markdown="1">

```python
base = "https://www.inflearn.com/"

quote = rep.quote_plus("추천-강좌")
url = base + quote
print(url)
```

  </div>

  {:.output_stream}
  ```
  https://www.inflearn.com/%EC%B6%94%EC%B2%9C-%EA%B0%95%EC%A2%8C

  ```


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

soup = BeautifulSoup(res, "html.parser")

img_list = soup.select("ul.slides")[0]

print("test", img_list)
```

  </div>

  {:.output_stream}
  ```
  test <ul class="slides"><li><div class="block courseitem" data-id="126956"><div class="block_media"><a href="https://www.inflearn.com/course/ios-%ed%94%84%eb%a1%9c%ea%b7%b8%eb%9e%98%eb%b0%8d/"><img alt="iOS 프로그래밍" class="attachment-small size-small wp-post-image" height="202" sizes="(max-width: 310px) 100vw, 310px" src="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/iOS_yagom-310x202.jpg" srcset="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/iOS_yagom-310x202.jpg 310w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/iOS_yagom-460x299.jpg 460w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/iOS_yagom-120x78.jpg 120w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/iOS_yagom.jpg 768w" width="310"/></a></div><div class="block_content"><h4 class="block_title"><a href="https://www.inflearn.com/course/ios-%ed%94%84%eb%a1%9c%ea%b7%b8%eb%9e%98%eb%b0%8d/" title="야곰의 iOS 프로그래밍">야곰의 iOS 프로그래밍</a></h4><div class="star-rating"><strong class="course-star-rating">
<i class="hide">5</i><small class="bp_blank_stars"><small class="bp_filled_stars" style="width:100%;"></small></small></strong></div><div class="pricing_course">
<div class="result"><span>가격 옵션 +</span></div>
<div class="drop"><label data-value="https://www.inflearn.com/product/%ec%95%bc%ea%b3%b0%ec%9d%98-ios-%ed%94%84%eb%a1%9c%ea%b7%b8%eb%9e%98%eb%b0%8d_%ec%a1%b0%ec%84%b1%ea%b7%9c/?redirect"><span class="font-text"><strong><del><span class="woocommerce-Price-amount amount"><span class="woocommerce-Price-currencySymbol">₩</span>55,000</span></del> <ins><span class="woocommerce-Price-amount amount"><span class="woocommerce-Price-currencySymbol">₩</span>38,500</span></ins></strong></span></label><label data-value="?error=login"><span class="font-text"><strong>50 000 런</strong></span></label></div>
</div><span class="clear"></span><strong><i class="fa fa-users"></i> 70</strong></div></div></li><li><div class="block courseitem" data-id="152712"><div class="block_media"><a href="https://www.inflearn.com/course/%ec%95%88%eb%93%9c%eb%a1%9c%ec%9d%b4%eb%93%9c-%eb%b3%b4%ec%95%88/"><img alt="안드로이드 보안" class="attachment-small size-small wp-post-image" height="202" sizes="(max-width: 310px) 100vw, 310px" src="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/i2sec_android-310x202.jpg" srcset="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/i2sec_android-310x202.jpg 310w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/i2sec_android-460x299.jpg 460w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/i2sec_android-120x78.jpg 120w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/i2sec_android.jpg 768w" width="310"/></a></div><div class="block_content"><h4 class="block_title"><a href="https://www.inflearn.com/course/%ec%95%88%eb%93%9c%eb%a1%9c%ec%9d%b4%eb%93%9c-%eb%b3%b4%ec%95%88/" title="안드로이드 취약점 진단">안드로이드 취약점 진단</a></h4><div class="star-rating"><strong class="course-star-rating">
<i class="hide"></i><small class="bp_blank_stars"><small class="bp_filled_stars" style="width:0%;"></small></small></strong></div><div class="pricing_course">
<div class="result"><span>가격 옵션 +</span></div>
<div class="drop"><label data-value="https://www.inflearn.com/product/%ec%95%88%eb%93%9c%eb%a1%9c%ec%9d%b4%eb%93%9c-%ec%b7%a8%ec%95%bd%ec%a0%90-%ec%a7%84%eb%8b%a8/?redirect"><span class="font-text"><strong><span class="woocommerce-Price-amount amount"><span class="woocommerce-Price-currencySymbol">₩</span>99,000</span></strong></span></label><label data-value="?error=login"><span class="font-text"><strong>90 000 런</strong></span></label></div>
</div><span class="clear"></span><strong><i class="fa fa-users"></i> 5</strong></div></div></li><li><div class="block courseitem" data-id="152856"><div class="block_media"><a href="https://www.inflearn.com/course/ios-%ec%95%b1-%ec%b7%a8%ec%95%bd%ec%a0%90-%ec%a7%84%eb%8b%a8/"><img alt="IOS 앱 취약점 진단" class="attachment-small size-small wp-post-image" height="202" sizes="(max-width: 310px) 100vw, 310px" src="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/i2sec_iOS-310x202.jpg" srcset="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/i2sec_iOS-310x202.jpg 310w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/i2sec_iOS-460x299.jpg 460w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/i2sec_iOS-120x78.jpg 120w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/i2sec_iOS.jpg 768w" width="310"/></a></div><div class="block_content"><h4 class="block_title"><a href="https://www.inflearn.com/course/ios-%ec%95%b1-%ec%b7%a8%ec%95%bd%ec%a0%90-%ec%a7%84%eb%8b%a8/" title="생초보도 하는 IOS 앱 취약점 진단">생초보도 하는 IOS 앱 취약점 진단</a></h4><div class="star-rating"><strong class="course-star-rating">
<i class="hide"></i><small class="bp_blank_stars"><small class="bp_filled_stars" style="width:0%;"></small></small></strong></div><div class="pricing_course">
<div class="result"><span>가격 옵션 +</span></div>
<div class="drop"><label data-value="https://www.inflearn.com/product/%ec%83%9d%ec%b4%88%eb%b3%b4%eb%8f%84-%ed%95%98%eb%8a%94-ios-%ec%95%b1-%ec%b7%a8%ec%95%bd%ec%a0%90-%ec%a7%84%eb%8b%a8/?redirect"><span class="font-text"><strong><span class="woocommerce-Price-amount amount"><span class="woocommerce-Price-currencySymbol">₩</span>138,600</span></strong></span></label><label data-value="?error=login"><span class="font-text"><strong>126 000 런</strong></span></label></div>
</div><span class="clear"></span><strong><i class="fa fa-users"></i> 3</strong></div></div></li><li><div class="block courseitem" data-id="151934"><div class="block_media"><a href="https://www.inflearn.com/course/tdd-%ea%b2%ac%ea%b3%a0%ed%95%9c-%ec%86%8c%ed%94%84%ed%8a%b8%ec%9b%a8%ec%96%b4-%eb%a7%8c%eb%93%a4%ea%b8%b0/"><img alt="TDD" class="attachment-small size-small wp-post-image" height="202" sizes="(max-width: 310px) 100vw, 310px" src="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/software-1-310x202.jpg" srcset="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/software-1-310x202.jpg 310w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/software-1-460x299.jpg 460w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/software-1-120x78.jpg 120w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/software-1.jpg 768w" width="310"/></a></div><div class="block_content"><h4 class="block_title"><a href="https://www.inflearn.com/course/tdd-%ea%b2%ac%ea%b3%a0%ed%95%9c-%ec%86%8c%ed%94%84%ed%8a%b8%ec%9b%a8%ec%96%b4-%eb%a7%8c%eb%93%a4%ea%b8%b0/" title="견고한 소프트웨어 만들기">견고한 소프트웨어 만들기</a></h4><div class="star-rating"><strong class="course-star-rating">
<i class="hide">5</i><small class="bp_blank_stars"><small class="bp_filled_stars" style="width:100%;"></small></small></strong></div><div class="pricing_course">
<div class="result"><span>가격 옵션 +</span></div>
<div class="drop"><label data-value="https://www.inflearn.com/product/%ea%b2%ac%ea%b3%a0%ed%95%9c-%ec%86%8c%ed%94%84%ed%8a%b8%ec%9b%a8%ec%96%b4-%eb%a7%8c%eb%93%a4%ea%b8%b0_%ea%b9%80%ec%a0%95%ed%99%98/?redirect"><span class="font-text"><strong><span class="woocommerce-Price-amount amount"><span class="woocommerce-Price-currencySymbol">₩</span>27,500</span></strong></span></label><label data-value="?error=login"><span class="font-text"><strong>25 000 런</strong></span></label></div>
</div><span class="clear"></span><strong><i class="fa fa-users"></i> 96</strong></div></div></li><li><div class="block courseitem" data-id="152163"><div class="block_media"><a href="https://www.inflearn.com/course/ecmascript-6-flow/"><img alt="es6 강좌" class="attachment-small size-small wp-post-image" height="202" sizes="(max-width: 310px) 100vw, 310px" src="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/es6-310x202.jpg" srcset="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/es6-310x202.jpg 310w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/es6-460x299.jpg 460w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/es6-120x78.jpg 120w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/es6.jpg 768w" width="310"/></a></div><div class="block_content"><h4 class="block_title"><a href="https://www.inflearn.com/course/ecmascript-6-flow/" title="개념을 제대로 알아보는 ECMAScript 6+ Flow">개념을 제대로 알아보는 ECMAScript 6+ Flow</a></h4><div class="star-rating"><strong class="course-star-rating">
<i class="hide">5</i><small class="bp_blank_stars"><small class="bp_filled_stars" style="width:100%;"></small></small></strong></div><div class="pricing_course">
<div class="result"><span>가격 옵션 +</span></div>
<div class="drop"><label data-value="https://www.inflearn.com/product/ecmascript-6-flow_%ec%a0%95%ec%9e%ac%eb%82%a8/?redirect"><span class="font-text"><strong><span class="woocommerce-Price-amount amount"><span class="woocommerce-Price-currencySymbol">₩</span>49,500</span></strong></span></label><label data-value="?error=login"><span class="font-text"><strong>45 000 런</strong></span></label></div>
</div><span class="clear"></span><strong><i class="fa fa-users"></i> 97</strong></div></div></li><li><div class="block courseitem" data-id="150560"><div class="block_media"><a href="https://www.inflearn.com/course/%eb%b8%94%eb%a1%9d%ec%b2%b4%ec%9d%b8-blockchain/"><img alt="블록체인" class="attachment-small size-small wp-post-image" height="202" sizes="(max-width: 310px) 100vw, 310px" src="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/blockchain-310x202.jpg" srcset="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/blockchain-310x202.jpg 310w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/blockchain-460x299.jpg 460w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/blockchain-120x78.jpg 120w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/blockchain.jpg 768w" width="310"/></a></div><div class="block_content"><h4 class="block_title"><a href="https://www.inflearn.com/course/%eb%b8%94%eb%a1%9d%ec%b2%b4%ec%9d%b8-blockchain/" title="블록체인과 솔리디티">블록체인과 솔리디티</a></h4><div class="star-rating"><strong class="course-star-rating">
<i class="hide">5</i><small class="bp_blank_stars"><small class="bp_filled_stars" style="width:100%;"></small></small></strong></div><strong>무료</strong><span class="clear"></span><strong><i class="fa fa-users"></i> 479</strong></div></div></li><li><div class="block courseitem" data-id="149801"><div class="block_media"><a href="https://www.inflearn.com/course/process-mining/"><img alt="process mining" class="attachment-small size-small wp-post-image" height="202" sizes="(max-width: 310px) 100vw, 310px" src="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/process-310x202.jpg" srcset="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/process-310x202.jpg 310w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/process-460x299.jpg 460w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/process-120x78.jpg 120w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/process.jpg 768w" width="310"/></a></div><div class="block_content"><h4 class="block_title"><a href="https://www.inflearn.com/course/process-mining/" title="모두를 위한 프로세스 마이닝">모두를 위한 프로세스 마이닝</a></h4><div class="star-rating"><strong class="course-star-rating">
<i class="hide">4.7</i><small class="bp_blank_stars"><small class="bp_filled_stars" style="width:94%;"></small></small></strong></div><strong>무료</strong><span class="clear"></span><strong><i class="fa fa-users"></i> 217</strong></div></div></li><li><div class="block courseitem" data-id="147672"><div class="block_media"><a href="https://www.inflearn.com/course/%ec%95%84%ec%9d%b4%ed%8f%b0-%ec%95%b1-%ea%b0%9c%eb%b0%9c-%ec%9e%85%eb%ac%b8-2%ed%8e%b8/"><img alt="아이폰 앱 개발 입문" class="attachment-small size-small wp-post-image" height="202" sizes="(max-width: 310px) 100vw, 310px" src="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/ios-happy2-310x202.jpg" srcset="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/ios-happy2-310x202.jpg 310w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/ios-happy2-460x299.jpg 460w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/ios-happy2-120x78.jpg 120w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/ios-happy2.jpg 768w" width="310"/></a></div><div class="block_content"><h4 class="block_title"><a href="https://www.inflearn.com/course/%ec%95%84%ec%9d%b4%ed%8f%b0-%ec%95%b1-%ea%b0%9c%eb%b0%9c-%ec%9e%85%eb%ac%b8-2%ed%8e%b8/" title="아이폰 앱 개발(Swift4 &amp; iOS11) 입문 2편">아이폰 앱 개발(Swift4 &amp; iOS11) 입문 2편</a></h4><div class="star-rating"><strong class="course-star-rating">
<i class="hide">5</i><small class="bp_blank_stars"><small class="bp_filled_stars" style="width:100%;"></small></small></strong></div><strong>무료</strong><span class="clear"></span><strong><i class="fa fa-users"></i> 155</strong></div></div></li><li><div class="block courseitem" data-id="143520"><div class="block_media"><a href="https://www.inflearn.com/course/asp-net-core/"><img alt="ASP.NET Core" class="attachment-small size-small wp-post-image" height="202" sizes="(max-width: 310px) 100vw, 310px" src="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/dotnetcore-1-310x202.jpg" srcset="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/dotnetcore-1-310x202.jpg 310w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/dotnetcore-1-460x299.jpg 460w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/dotnetcore-1-120x78.jpg 120w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/dotnetcore-1.jpg 768w" width="310"/></a></div><div class="block_content"><h4 class="block_title"><a href="https://www.inflearn.com/course/asp-net-core/" title="해외취업 ASP.NET Core 웹개발 기본 강좌">해외취업 ASP.NET Core 웹개발 기본 강좌</a></h4><div class="star-rating"><strong class="course-star-rating">
<i class="hide">5</i><small class="bp_blank_stars"><small class="bp_filled_stars" style="width:100%;"></small></small></strong></div><strong>무료</strong><span class="clear"></span><strong><i class="fa fa-users"></i> 292</strong></div></div></li><li><div class="block courseitem" data-id="142047"><div class="block_media"><a href="https://www.inflearn.com/course/firebase-android/"><img alt="firebase android" class="attachment-small size-small wp-post-image" height="202" sizes="(max-width: 310px) 100vw, 310px" src="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/android_firebase-310x202.jpg" srcset="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/android_firebase-310x202.jpg 310w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/android_firebase-460x299.jpg 460w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/android_firebase-120x78.jpg 120w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/android_firebase.jpg 768w" width="310"/></a></div><div class="block_content"><h4 class="block_title"><a href="https://www.inflearn.com/course/firebase-android/" title="Firebase 서버를 통한 Android앱 개발 지침서">Firebase 서버를 통한 Android앱 개발 지침서</a></h4><div class="star-rating"><strong class="course-star-rating">
<i class="hide">5</i><small class="bp_blank_stars"><small class="bp_filled_stars" style="width:100%;"></small></small></strong></div><strong>무료</strong><span class="clear"></span><strong><i class="fa fa-users"></i> 167</strong></div></div></li><li><div class="block courseitem" data-id="142548"><div class="block_media"><a href="https://www.inflearn.com/course/kotlin-android-firebase/"><img alt="" class="attachment-small size-small wp-post-image" height="202" sizes="(max-width: 310px) 100vw, 310px" src="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/Kotlin-310x202.jpg" srcset="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/Kotlin-310x202.jpg 310w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/Kotlin-460x299.jpg 460w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/Kotlin-120x78.jpg 120w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/Kotlin.jpg 768w" width="310"/></a></div><div class="block_content"><h4 class="block_title"><a href="https://www.inflearn.com/course/kotlin-android-firebase/" title="Kotlin 으로 Android 개발부터 Firebase 개발까지">Kotlin 으로 Android 개발부터 Firebase 개발까지</a></h4><div class="star-rating"><strong class="course-star-rating">
<i class="hide">5</i><small class="bp_blank_stars"><small class="bp_filled_stars" style="width:100%;"></small></small></strong></div><div class="pricing_course">
<div class="result"><span>가격 옵션 +</span></div>
<div class="drop"><label data-value="https://www.inflearn.com/product/kotlin-%ec%9c%bc%eb%a1%9c-android-%ea%b0%9c%eb%b0%9c%eb%b6%80%ed%84%b0-firebase-%ea%b0%9c%eb%b0%9c%ea%b9%8c%ec%a7%80/?redirect"><span class="font-text"><strong><span class="woocommerce-Price-amount amount"><span class="woocommerce-Price-currencySymbol">₩</span>49,500</span></strong></span></label><label data-value="?error=login"><span class="font-text"><strong>45 000 런</strong></span></label></div>
</div><span class="clear"></span><strong><i class="fa fa-users"></i> 49</strong></div></div></li><li><div class="block courseitem" data-id="140728"><div class="block_media"><a href="https://www.inflearn.com/course/%ec%9c%a0%eb%8b%88%ed%8b%b0-%ea%b2%8c%ec%9e%84-%ed%94%84%eb%a1%9c%ea%b7%b8%eb%9e%98%eb%b0%8d-%ec%97%90%ec%84%bc%ec%8a%a4/"><img alt="유니티 게임 개발 강좌" class="attachment-small size-small wp-post-image" height="202" sizes="(max-width: 310px) 100vw, 310px" src="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/retr0-310x202.png" srcset="https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/retr0-310x202.png 310w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/retr0-460x299.png 460w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/retr0-120x78.png 120w, https://d81pi4yofp37g.cloudfront.net/wp-content/uploads/retr0.png 768w" width="310"/></a></div><div class="block_content"><h4 class="block_title"><a href="https://www.inflearn.com/course/%ec%9c%a0%eb%8b%88%ed%8b%b0-%ea%b2%8c%ec%9e%84-%ed%94%84%eb%a1%9c%ea%b7%b8%eb%9e%98%eb%b0%8d-%ec%97%90%ec%84%bc%ec%8a%a4/" title="retr0의 유니티 게임 프로그래밍 에센스">retr0의 유니티 게임 프로그래밍 에센스</a></h4><div class="star-rating"><strong class="course-star-rating">
<i class="hide">5</i><small class="bp_blank_stars"><small class="bp_filled_stars" style="width:100%;"></small></small></strong></div><div class="pricing_course">
<div class="result"><span>가격 옵션 +</span></div>
<div class="drop"><label data-value="https://www.inflearn.com/product/retro-%ec%9c%a0%eb%8b%88%ed%8b%b0-%ed%94%84%eb%a1%9c%ea%b7%b8%eb%9e%98%eb%b0%8d-%ec%97%90%ec%84%bc%ec%8a%a4-%ec%9d%b4%ec%a0%9c%eb%af%bc/?redirect"><span class="font-text"><strong><span class="woocommerce-Price-amount amount"><span class="woocommerce-Price-currencySymbol">₩</span>49,500</span></strong></span></label><label data-value="?error=login"><span class="font-text"><strong>45 000 런</strong></span></label></div>
</div><span class="clear"></span><strong><i class="fa fa-users"></i> 89</strong></div></div></li></ul>

  ```

### urlretrieve을 통해 파일 저장


  <div class="input_area" markdown="1">

```python
for i, e in enumerate(img_list):
    with open(savePath+"text_"+str(i)+".txt","wt") as f:
        f.write(e.select_one("h4.block_title > a").string)
    fullFileName = os.path.join(savePath+str(i)+".png")
#     print(fullFileName)
    req.urlretrieve(e.select_one("div.block_media > a > img")["src"],fullFileName)
print("완료")
```

  </div>

  {:.output_stream}
  ```
  완료

  ```


  <div class="input_area" markdown="1">

```python

```

  </div>


  <div class="input_area" markdown="1">

```python

```

  </div>
