---
title: 배포에 대한 라이선스 유형 업데이트
seo-title: Update the license type for the deployment
description: 관리 콘솔에서 라이선스 변경 페이지를 사용하여 배포에 대한 라이선스 유형을 업데이트합니다.
seo-description: Update the license type for the deployment by using the Change License page in administration console.
uuid: 0152635e-2c00-4944-b9b6-64b368589a91
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e4f31377-ccc9-4986-a3bf-ef2e83d12448
exl-id: 6b975aa1-9270-4098-9af5-c5cc67cb7b5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# 배포에 대한 라이선스 유형 업데이트 {#update-the-license-type-for-the-deployment}

AEM Forms 설치 프로세스의 일부로 Configuration Manager를 사용하여 필요한 AEM Forms 모듈을 구성하고 배포했습니다. 기본적으로 이러한 모듈은 60일 평가 라이센스로 구성됩니다. 관리 콘솔에서 라이선스 변경 페이지를 사용하여 배포에 대한 라이선스 유형을 변경할 수 있습니다. 현재 배포된 모듈이 [라이센스 변경] 페이지에 표시됩니다.

라이센스 변경 페이지에는 라이센스에 대한 정보가 표시됩니다.

* 현재 라이선스 유형
* 라이센스가 마지막으로 업데이트된 날짜 및 시간입니다
* 마지막 업데이트를 수행한 사람
* 라이센스의 현재 상태입니다
* AEM Forms가 설치된 날짜입니다
* 현재 라이선스가 만료되는 날짜

>[!NOTE]
>
>라이센스 변경은 배포된 모든 모듈에 적용됩니다. 라이센스 유형을 변경하기 전에 라이센스가 없는 모듈의 배포를 취소합니다. 배포된 모듈 목록에 Adobe에서 구입한 모듈 이외의 모듈이 포함된 경우 프로덕션 라이센스 유형을 선택하지 마십시오.

## 라이센스 유형 업데이트 {#update-the-license-type}

1. 관리 콘솔에서 라이센스를 클릭합니다.
1. AEM Forms 최종 사용자 사용권 계약을 읽고, 계약 조건에 동의하는 경우 동의 를 선택한 후 다음을 클릭합니다.
1. 라이센스 변경 페이지에서 라이센스 유형을 선택합니다.

   * **EVAL:** 60일 평가판 라이선스
   * **개발:** 영구 개발 라이선스
   * **NFR:** 2년 평가 라이선스
   * **IDEV:** Adobe Developer 프로그램 1년 구독
   * **프로덕션:** 영구 라이선스

1. 예, 배포된 모든 모듈에 대해 라이센스 변경이 유효합니다.
1. 라이센스 변경 확인을 클릭합니다. 라이센스가 성공적으로 업데이트되었다는 메시지가 나타납니다.
