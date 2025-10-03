---
title: 인증서 관리
description: 인증서를 가져오거나 내보내는 방법과 신뢰 설정을 편집하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1fe0e7b4-6109-4f7a-8858-8237a1c5c93b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '646'
ht-degree: 100%

---

# 인증서 관리 {#managing-certificates}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

Trust Store 관리를 사용하면 디지털 서명의 유효성 검사와 인증서 인증을 위해 서버에서 신뢰하는 인증서를 가져오고, 편집하고, 삭제할 수 있습니다. 인증서를 원하는 수만큼 가져오고 내보낼 수 있습니다. 인증서를 가져온 후에는 신뢰 설정과 Trust Store 유형을 편집할 수 있습니다. Trust Store 유형을 결합할 때 다음 옵션을 고려하십시오.

* **CA를 통한 인증서 인증에 대한 신뢰:** CRL 유효성 검사를 위해 ID에 대한 신뢰도 선택합니다.
* **ICA를 통한 인증서 인증에 대한 신뢰:** ID에 대한 신뢰만 선택합니다. ICA는 인증서 인증을 위해 신뢰해서는 안 됩니다. 인증서 인증을 위해 ICA를 신뢰하는 경우 ICA는 경로 구축을 위한 CA가 됩니다. 인증서 인증과 ID 모두에 대해 ICA를 신뢰할 수 있는 경우 ICA가 CA가 되므로 CA 공급업체 인증서는 무시됩니다.
* **HTTPS를 통한 OCSP 서버에 대한 신뢰:** OSCP 응답 서버가 HTTPS 위치에 있는 경우 SSL 연결에 대한 신뢰도 선택해야 합니다. OSCP 응답자가 CRL 유효성 검사를 요구하는 경우 ID에 대한 신뢰도 선택해야 합니다.
* **Adobe Root:** SSL 연결이나 OCSP 서버 Trust Store 유형을 선택하지 마십시오. Adobe Root는 SSL 연결 및 OCSP 서버에서 신뢰할 수 없습니다. Adobe는 OCSP 및 SSL 인증서를 발급하지 않습니다. Adobe Root는 별칭 이름=&quot;ADOBEROOT&quot;로 암묵적으로 신뢰됩니다.

X509v3 인증서만 지원됩니다. 이 인증서 유형은 이진 DER 인코딩 파일(.cer 파일) 또는 동일한 DER 인코딩 인증서의 Base64 인코딩 버전(PEM(Privacy Enhanced Mail) 형식의 X509 인증서 포함)이 포함된 텍스트 파일로 제공될 수 있습니다.

서명 유효성 검사를 완료하는 데 필요한 인증서는 동일한 저장소(HSM 또는 데이터베이스)에 있어야 합니다.

신뢰 관리자 API를 사용하여 인증서를 가져오고 삭제할 수도 있습니다. 자세한 내용은 [AEM Forms를 사용한 프로그래밍](https://www.adobe.com/go/learn_aemforms_programming_63)의 &#39;신뢰 관리자 API를 사용하여 인증서 가져오기&#39; 및 &#39;신뢰 관리자 API를 사용하여 인증서 삭제&#39;를 참조하십시오.

## 인증서 가져오기 {#import-a-certificate}

1. 관리 콘솔에서 **[!UICONTROL 설정 > Trust Store 관리 > 인증서]**&#x200B;를 클릭합니다.
1. 가져오기를 클릭하고 Trust Store 유형에서 다음 옵션 중 하나를 선택합니다.

   * **SSL 연결에 대한 신뢰:** AEM Forms가 인증서를 사용하여 SSL을 통해 외부 시스템에 연결할 수 있도록 지정합니다.
   * **서명 인증에 대한 신뢰:** 작성자 디지털 서명을 인증하기 위한 문서 서명 작업에서 인증서를 신뢰할 수 있도록 지정합니다.
   * **서명에 대한 신뢰:** 비작성자 디지털 서명을 인증하기 위한 문서 서명 작업에서 인증서를 신뢰할 수 있도록 지정합니다.
   * **인증서 인증에 대한 신뢰:** AEM Forms가 인증서 또는 스마트 카드 인증을 사용하여 사용자를 인증하기 위해 인증서를 사용하도록 지정합니다.
   * **OCSP 서버에 대한 신뢰:** AEM Forms가 인증서를 사용하여 외부 OCSP 응답자에 연결할 수 있도록 지정합니다.
   * **ID에 대한 신뢰:** 인증서를 사용하여 위에 지정된 유형 이외의 정보를 신뢰할 수 있도록 지정합니다.

   >[!NOTE]
   >
   >Trust Store는 인증서 인증, 서명, 서명 인증, ID에 대해 Adobe Root 인증서를 암묵적으로 신뢰합니다.

1. 별칭 상자에 인증서 식별자를 입력합니다.
1. **[!UICONTROL 찾아보기]** 를 클릭하여 인증서를 찾은 후 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

## 인증서 내보내기 {#export-a-certificate}

1. 관리 콘솔에서 **[!UICONTROL 설정 > Trust Store 관리 > 인증서]**&#x200B;를 클릭합니다.
1. 내보낼 인증서의 별칭 이름을 클릭합니다. **[!UICONTROL 인증서 세부 정보]** 페이지가 표시됩니다.
1. **[!UICONTROL 내보내기]**&#x200B;를 클릭하고 지침에 따라 인증서를 내보낸 후 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

## 인증서의 신뢰 설정 및 Trust Store 유형 편집 {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. 관리 콘솔에서 **[!UICONTROL 설정 > Trust Store 관리 > 인증서]**&#x200B;를 클릭합니다.
1. 편집할 인증서의 별칭 이름을 클릭합니다.
1. **[!UICONTROL 인증서 업데이트]**&#x200B;를 클릭합니다.
1. 인증서의 별칭 이름을 변경하려면 별칭 상자에 새 이름을 입력합니다.
1. 인증서의 Trust Store 유형을 업데이트하려면 해당 Trust Store 유형을 선택합니다.
1. 정책 제한 사항을 업데이트하려면 인증서 정책 상자에 정책 정보를 입력한 후 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

## 인증서 삭제 {#delete-a-certificate}

1. 관리 콘솔에서 **[!UICONTROL 설정 > Trust Store 관리 > 인증서]**&#x200B;를 클릭합니다.
1. 삭제할 인증서의 확인란을 선택하고 **[!UICONTROL 삭제]**&#x200B;를 클릭한 후 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.
