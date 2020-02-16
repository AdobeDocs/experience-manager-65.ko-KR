---
title: 요청 분석 스크립트
seo-title: 요청 분석 스크립트
description: 요청 분석 스크립트는 나중에 처리할 수 있도록 읽을 수 있는 보고서를 생성하는 access.log 파일의 분석을 용이하게 하기 위해 수행됩니다
seo-description: 요청 분석 스크립트는 나중에 처리할 수 있도록 읽을 수 있는 보고서를 생성하는 access.log 파일의 분석을 용이하게 하기 위해 수행됩니다
uuid: 24eff3c6-5748-46f3-a30c-4a3a6427ce1d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 1b5e0ccf-4157-45e3-8caf-1d6739d7d9d2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 요청 분석 스크립트{#request-analysis-script}

## 다운로드 {#download}

이 스크립트는 나중에 처리할 수 있도록 읽을 수 있는 보고서를 생성하는 `access.log` 파일의 분석을 용이하게 하기 위해 만들어졌습니다.

[파일 가져오기](assets/analyse-access.sh)

## 설명 {#description}

이 스크립트는 나중에 처리할 수 있도록 읽을 수 있는 보고서를 생성하는 `access.log` 파일의 분석을 용이하게 하기 위해 만들어졌습니다.

전체 요청 번호, GET과 POST, 시간에 따른 요청 배포 등이 생성됩니다.

출력 내용이 마크다운 구문으로 제공되므로 pandoc와 같은 툴이나 Markdown 뷰어와 같은 플러그인이 있는 브라우저에서 표시하면 PDF로 손쉽게 변환할 수 있습니다.

명령줄에서 제공된 사용자 지정 경로를 분석할 수 있습니다.

파일 내 댓글에서 실행 방법을 알려주는 다음 작업을 수행합니다.

다양한 정보를 `access.log` 추출하고 마케팅 출력을 생성할 수 있는 CQ를 `stdout`분석합니다.

## 사용량 {#usage}

`./analyse-access.sh access.log.2013-&ast;`

명령줄에서 분석할 추가 사용자 지정 경로를 제공할 수 있습니다.

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

단순 파이핑으로 출력을 저장할 수 있습니다

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
