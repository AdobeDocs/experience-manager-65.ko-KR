---
title: 분석 요청 스크립트
seo-title: Request Analysis Script
description: 요청 분석 스크립트는 나중에 처리할 수 있도록 읽기 가능한 보고서를 생성하는 access.log 파일의 분석을 용이하게 하기 위해 작성됩니다
seo-description: The request analysis script is made to ease the analysis of the access.log files producing a readable report for later processing
uuid: 24eff3c6-5748-46f3-a30c-4a3a6427ce1d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 1b5e0ccf-4157-45e3-8caf-1d6739d7d9d2
exl-id: e14a9cda-890f-46b7-9433-1b52eb91eae3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 6%

---

# 분석 요청 스크립트{#request-analysis-script}

## 다운로드 {#download}

이 스크립트는 `access.log` 나중에 처리할 수 있도록 읽기 가능한 보고서를 생성하는 파일입니다.

[파일 가져오기](assets/analyse-access.sh)

## 설명 {#description}

이 스크립트는 `access.log` 나중에 처리할 수 있도록 읽기 가능한 보고서를 생성하는 파일입니다.

전체 요청 수, GET 및 POST, 시간에 따른 요청 분포 등을 생성합니다.

출력은 Markdown 구문으로 되어 있으므로 pandoc과 같은 도구를 사용하여 PDF으로 변환하거나 Markdown 뷰어와 같은 플러그인을 사용하여 브라우저에 표시하는 것이 더 쉽습니다.

명령줄에 제공된 사용자 지정 경로를 분석할 수 있습니다.

실행 방법을 알려 주는 파일 내의 주석을 가져옵니다.

CQ 분석 `access.log` 다양한 정보 외삽하고 의 Markdown 출력 생성 `stdout`.

## 사용 {#usage}

`./analyse-access.sh access.log.2013-&ast;`

명령줄에서 분석할 추가 사용자 지정 경로를 제공할 수 있습니다

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

간단한 파이핑으로 출력을 저장할 수 있습니다

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
