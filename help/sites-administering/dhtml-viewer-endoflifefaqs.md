---
title: DHTML 뷰어 지원 중단 FAQ
seo-title: DHTML 뷰어 지원 중단 FAQ
description: 2014년 1월 31일부터 Scene7의 DHTML 뷰어 플랫폼은 공식적으로 사용이 종료됩니다. 이 알림은 FAQ에 대한 답변을 제공하므로 새로운 HTML5 뷰어 플랫폼으로 전환될 준비를 할 수 있습니다.
seo-description: 2014년 1월 31일부터 Scene7의 DHTML 뷰어 플랫폼은 공식적으로 사용이 종료됩니다. 이 알림은 FAQ에 대한 답변을 제공하므로 새로운 HTML5 뷰어 플랫폼으로 전환될 준비를 할 수 있습니다.
uuid: a78c03b3-6513-42e1-881f-6a9551659769
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d94244ac-a5f6-4c95-ab8c-26b41d25863f
translation-type: tm+mt
source-git-commit: 283802809d665cd979e2f1a4fa969b6ddc491ed6
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 0%

---


# DHTML 뷰어 지원 중단 FAQ{#dhtml-viewer-end-of-life-faqs}

2014년 1월 31일부터 Scene7의 DHTML 뷰어 플랫폼은 공식적으로 사용이 종료됩니다. 이 알림은 FAQ에 대한 답변을 제공하므로 새로운 HTML5 뷰어 플랫폼으로 전환될 준비를 할 수 있습니다.

**변경 사항이 무엇입니까?**

2014년 1월 31일부터 DHTML 뷰어 플랫폼에 대한 지원이 공식적으로 종료됩니다.

**삶의 종말은 무엇을 의미하는가?**

수명이 다하면 Scene7은 (1) 더 이상 DHTML 뷰어 플랫폼(2)에 기능 개선 사항을 추가하지 않으며, DHTML 뷰어 플랫폼에 대한 버그 수정을 출시하지 않으며, (3) 고객 지원 센터는 더 이상 DHTML 관련 뷰어 문제 또는 질문에 대한 문제 해결 또는 지원을 제공하지 않습니다.

**Scene7이 왜 이렇게 바뀌죠?**

웹 표준은 끊임없이 진화하고 있으며 DHTML은 HTML5로 신속하게 대체되는 이전 웹 개발 기술입니다. 플랫폼으로서 DHTML의 가장 큰 제한은 이제 HTML5가 브라우저 간에 일관되고 쉽게 지원할 수 있는 풍부한 경험을 만들 수 없다는 것입니다. 예를 들어 다음과 같은 제한 사항에는 브라우저 간 지원이 없습니다.

* 사용자 정의 커서
* 둥근 모서리
* 애니메이션(페이지 넘기기, 확대/축소 속도 등)
* 효과(그림자, 광선 등)
* 완벽한 글꼴 지원
* 플러그인 없는 비디오 재생

JSP 기반 솔루션과 Javascript API는 Scene7 DHTML 뷰어 플랫폼에서만 다중 터치 및 제스처 기능을 활용하는 모바일 장치에 최적화되지 않았습니다. 2011년/2012년 초에 출시된 DHTML 뷰어는 모바일에 맞게 최적화되었지만 유연한 SDK 구성 요소 기반 개발 프레임워크가 없어 사용자 정의 및 유지 관리가 어려웠습니다.

데스크탑 및 모바일에서 새로운 표준으로 자리매김한 HTML5와 HTML5에 대한 이러한 제약 때문에 Scene7은 HTML5 기반의 뷰어 플랫폼에 투자하기로 결정했습니다. 이러한 투자를 통해 고객은 데스크탑, iOS, Android 디바이스 등 다양한 화면에서 사용자에게 보다 풍부하고 매력적이며 인터랙티브한 뷰어를 구축할 수 있는 강력한 플랫폼을 제공할 수 있습니다.

**뷰어가 DHTML 플랫폼을 사용하고 있는지 어떻게 알 수 있습니까?**

회사에서 사용 중인 뷰어가 DHTML인지 여부를 확인하고 이러한 변경의 영향을 받으려면 다음 사항을 확인하십시오.

1. 회사에서 이 표에 나열된 &quot;뷰어 기술&quot;이 &quot;DHTML&quot;로 지정된 즉시 사용 가능한 Scene7 뷰어를 사용하고 있습니다.

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. 회사에서 이 표에서 &quot;뷰어 기술&quot;이 &quot;DHTML&quot;로 지정된 최신 Scene7 뷰어를 기반으로 새 사전 설정으로 만들어진 뷰어를 사용하고 있습니다.

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. 회사에서 JSP 기반 DHTML 솔루션에서 생성된 사용자 정의 뷰어를 사용하고 있습니다.

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference)

1. 회사에서 Javascript API에서 만든 사용자 정의 뷰어를 사용하고 있습니다.

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference)

1. 회사에서 DHTML 다중 화면 플라이아웃 API로 만든 사용자 정의 뷰어를 사용하고 있습니다.

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer)

1. 회사에서 DHTML 데스크탑 플라이아웃 API로 만든 사용자 정의 뷰어를 사용하고 있습니다.

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer)

1. 회사에서 DHTML 뷰어 패키지의 일부인 장치 감지 라이브러리를 사용하고 있습니다.

   코드에 &quot;sj_deviceDetect.js&quot;가 포함되어 있는 JS를 찾습니다.

   다음은 새로운 JS 장치 감지 코드로 대체되었습니다. [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers) .

**대체 뷰어 플랫폼이란 무엇입니까?**

DHTML을 대체할 수 있는 곳은 Scene7 HTML5 뷰어 플랫폼으로, 두 가지 모두로 구성됩니다.

* 기본 확대/축소, 플라이아웃 확대/축소, 이미지 세트, 견본 집합, 다차원 회전 및 혼합 미디어 등 다양한 뷰어 유형에서 모바일에 최적화된 상호 작용을 제공하는 HTML5 기본 뷰어입니다. 이러한 뷰어의 최신 예는 다음을 참조하십시오. [https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
* HTML5 지원 사이트 및 디바이스(예: iOS 및 Android)에 대한 Adobe Scene7 뷰어를 광범위한 사용자 정의할 수 있는 HTML5 뷰어 SDK를 사용하면 뷰어의 모양과 인터랙션을 브랜딩할 수 있는 유연성과 창의성을 최대한 향상시킬 수 있습니다. 재사용 가능한 성능 최적화 구성 요소의 이점은 뷰어 개발 비용을 줄이고 사용자 정의 개발을 가속화합니다.

**HTML5 뷰어 플랫폼은 언제 DHTML 뷰어 플랫폼에서 전환해야 하는 기능을 갖게 됩니까?**

Scene7은 2011년 가을 버전 5.5를 출시하여 첫 번째 HTML5 뷰어 SDK를 출시했습니다. 이후 다양한 기능을 플랫폼에 추가하고 더 많은 유형의 뷰어를 지원합니다. 대부분의 일반적인 뷰어 요구 사항의 경우, HTML5 뷰어 플랫폼에 지금 마이그레이션해야 하는 기능이 이미 포함되어 있을 수 있습니다. Adobe는 분기별로 릴리스되는 이 뷰어 플랫폼에 지속적으로 적극적으로 투자하고 있습니다.

HTML5 뷰어 플랫폼을 통해 뷰어 요구 사항을 충족할 수 있는지 확인하려면 다음 설명서를 참조하십시오.

[https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers) (특별 뷰어 기능 및 사용자 정의 기능)

[https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html) (SDK API 설명서에 액세스하려면)

HTML5 뷰어 SDK가 사용자의 요구 사항을 충족하는지 여부를 아직 확신할 수 없는 경우 Adobe 전문 서비스 팀과 문의하십시오.

**뷰어를 HTML5 플랫폼으로 전환하려면 어떻게 해야 합니까?**

뷰어를 HTML5 플랫폼으로 전환하기 위해 Scene7은 다음 옵션을 제공합니다.

1. Scene7의 기본 HTML5 뷰어 중 하나를 사용하십시오. HTML5 뷰어는 여기에서 찾을 수 있습니다. [https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
1. SPS 응용 프로그램 설정 아래에 기본 HTML5 뷰어 중 하나를 구성합니다. 이를 통해 뷰어 크기, 전환, 확대/축소 동작 등과 같은 특정 동작을 사용자 정의할 수 있습니다. [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html)
1. CSS를 수정하여 단추 아트워크, 배치, 투명도, 배경색 등과 같은 시각 디자인을 변경하여 Scene7의 기본 HTML5 뷰어의 모양과 느낌을 사용자 요구에 맞게 변경할 수 있습니다. [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers)
1. 여기에서 다운로드할 수 있는 SDK를 사용하여 처음부터 사용자 정의 HTML5 뷰어를 만듭니다. [https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html). 전문 서비스를 통해 사용자 정의 뷰어를 만들거나 웹 개발 팀에서 직접 만들 수 있습니다.

**HTML5를 지원하지 않는 브라우저는 어떻게 됩니까?**

HTML5는 많은 모바일 디바이스와 웹 브라우저에서 지원되며, 계속해서 주목을 받고 있습니다. 현재 Internet Explorer 8 이하에서는 HTML5가 지원되지 않지만 Adobe의 HTML5 뷰어 플랫폼을 혁신하여 IE 7 및 IE 8까지 지원을 확장했습니다. Scene7 HTML5 뷰어 플랫폼을 사용하면 단일 개발 플랫폼을 통해 데스크탑 및 모바일 사용자 모두의 절대 범위를 확대할 수 있습니다.

HTML5 SDK 버전 2.2.1의 현재 시스템 요구 사항은 다음과 같습니다.

* Microsoft® Windows® XP 이상, Macintosh® OS X 10.6 이상
* Firefox 17, Safari 5.1, Chrome 23, Internet Explorer 7 이상
* iOS 3.2.2 이상
* iPhone3 이상 및 iPad1 이상에서 인증(기본 브라우저)
* Android OS 2.2 이상

브라우저가 HTML5 뷰어 플랫폼과 호환되는지 확인하려면 다음 예제 뷰어를 실행하십시오.

[https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image](https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image)

마우스를 가져가거나 기본 이미지 위로 손가락을 드래그하여 확대된 이미지가 표시되는 경우 지원되는 브라우저/디바이스입니다.

**기존 DHTML 뷰어를 사용하여 프로덕션에서 라이브하기를 원하는 경우 어떤 옵션이 있습니까?**

DHTML 기반 뷰어를 사용하여 프로덕션에서 여전히 라이브할 수는 있지만 2014년 1월 31일 이후에는 개선 사항, 버그 수정 및 고객 지원 기능이 제공되지 않는다는 점을 유의해야 합니다. 따라서 모든 고객은 더욱 강력한 HTML5 뷰어 플랫폼으로 마이그레이션해야 합니다.. 그러나 비즈니스 상황에서 EOL 날짜까지 이러한 마이그레이션을 허용하지 않는 경우, 지원되는 유지 관리 기간을 연장하기 위해 전문 서비스와 계약을 체결할 수 있습니다. 자세한 내용은 계정 관리자에게 문의하십시오.

**자세한 내용은 누구에게 연락해야 합니까?**

이 FAQ가 귀하의 모든 질문에 답변하지 않은 경우 Admin Console을 [사용하여 지원 사례를](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) 만들거나 Adobe 계정 관리자에게 문의하십시오.
