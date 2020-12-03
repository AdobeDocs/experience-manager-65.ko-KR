---
title: 분석 요청 스크립트
seo-title: 분석 요청 스크립트
description: 요청 분석 스크립트는 나중 처리를 위해 읽을 수 있는 보고서를 생성하는 access.log 파일의 분석을 용이하게 하기 위해 수행됩니다
seo-description: 요청 분석 스크립트는 나중 처리를 위해 읽을 수 있는 보고서를 생성하는 access.log 파일의 분석을 용이하게 하기 위해 수행됩니다
uuid: 24eff3c6-5748-46f3-a30c-4a3a6427ce1d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 1b5e0ccf-4157-45e3-8caf-1d6739d7d9d2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 7%

---


# 분석 요청 스크립트{#request-analysis-script}

## 다운로드 {#download}

이 스크립트는 나중에 처리할 수 있도록 읽을 수 있는 보고서를 생성하는 `access.log` 파일의 분석을 용이하게 하기 위해 만들어졌습니다.

[파일 가져오기](assets/analyse-access.sh)

## 설명 {#description}

이 스크립트는 나중에 처리할 수 있도록 읽을 수 있는 보고서를 생성하는 `access.log` 파일의 분석을 용이하게 하기 위해 만들어졌습니다.

전체 요청 번호, GET 및 POST, 시간에 따른 요청 배포 등을 생성합니다.

출력 내용이 마크다운 구문으로 되어 있으므로 Markdown 뷰어와 같은 플러그인이 있는 브라우저에서 PDF로 변환하거나 표시하는 것이 더 쉽습니다.

명령줄에서 제공된 사용자 지정 경로를 분석할 수 있습니다.

파일 내의 주석에서 실행 방법을 알려주는 다음 항목을 수행합니다.

다양한 정보를 추출하고 `stdout`에서 마크다운 출력을 생성하는 CQ `access.log`을 분석합니다.

## 사용량 {#usage}

`./analyse-access.sh access.log.2013-&ast;`

명령줄에서 분석할 추가 사용자 지정 경로를 제공할 수 있습니다.

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

단순 파이핑으로 출력을 저장할 수 있습니다

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
