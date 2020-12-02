---
title: 배포용 라이선스 유형 업데이트
seo-title: 배포용 라이선스 유형 업데이트
description: 관리 콘솔의 라이선스 변경 페이지를 사용하여 배포용 라이선스 유형을 업데이트합니다.
seo-description: 관리 콘솔의 라이선스 변경 페이지를 사용하여 배포용 라이선스 유형을 업데이트합니다.
uuid: 0152635e-2c00-4944-b9b6-64b368589a91
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e4f31377-ccc9-4986-a3bf-ef2e83d12448
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---


# 배포 {#update-the-license-type-for-the-deployment} 라이선스 유형을 업데이트합니다.

AEM 양식 설치 프로세스의 일부로 Configuration Manager를 사용하여 필요한 AEM 양식 모듈을 구성하고 배포했습니다. 기본적으로 이러한 모듈은 60일 평가판 라이선스로 구성됩니다. 관리 콘솔의 라이선스 변경 페이지를 사용하여 배포에 대한 라이선스 유형을 변경합니다. 현재 배포된 모듈은 라이선스 변경 페이지에 표시됩니다.

라이센스 변경 페이지에는 라이센스에 대한 정보가 표시됩니다.

* 현재 라이선스 유형
* 라이선스가 마지막으로 업데이트된 날짜 및 시간
* 마지막 업데이트를 수행한 사람
* 라이센스의 현재 상태
* AEM 양식을 설치한 날짜
* 현재 라이선스가 만료되는 날짜

>[!NOTE]
>
>라이선스 변경은 배포된 모든 모듈에 적용됩니다. 라이선스 유형을 변경하기 전에 라이선스가 없는 모든 모듈의 배포를 취소합니다. 배포된 모듈 목록에 Adobe에서 구입한 모듈 외의 모듈이 포함되어 있는 경우에는 프로덕션 라이선스 유형을 선택하지 마십시오.

## 라이센스 유형 {#update-the-license-type} 업데이트

1. 관리 콘솔에서 라이센스를 클릭합니다.
1. AEM 양식 최종 사용자 사용권 계약을 읽고, 계약 내용에 동의하는 경우 동의함을 선택한 다음 다음을 클릭합니다.
1. 라이센스 변경 페이지에서 라이센스 유형을 선택합니다.

   * **EVAL:** 60일 평가판 라이선스
   * **DEV:** 영구 개발 라이선스
   * **NFR:** 2년 평가 라이선스
   * **IDEV: Adobe 개발자 프로그램** 1년 가입
   * **제작:** 영구 라이선스

1. 예, 라이선스 변경은 모든 배포된 모듈에 유효합니다.
1. 라이센스 변경 확인을 클릭합니다. 라이센스가 성공적으로 업데이트되었다는 메시지가 나타납니다.

