---
title: 인증서 관리
seo-title: 인증서 관리
description: 인증서를 가져오고 내보내고 신뢰 설정을 편집하는 방법을 알아봅니다.
seo-description: 인증서를 가져오고 내보내고 신뢰 설정을 편집하는 방법을 알아봅니다.
uuid: 46b1dbe5-517c-4294-bb52-cc6700a768e8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9fd531c0-5206-4be0-a450-13e0dc806068
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 인증서 관리 {#managing-certificates}

Trust Store Management를 사용하여 디지털 서명 및 인증서 인증의 유효성 검사를 위해 서버에서 신뢰하는 인증서를 가져오거나 편집 및 삭제할 수 있습니다. 인증서를 원하는 만큼 가져오거나 내보낼 수 있습니다. 인증서를 가져온 후 트러스트 설정 및 트러스트 저장소 유형을 편집할 수 있습니다. 트러스트 저장소 유형을 결합할 때는 다음 옵션을 고려하십시오.

* **** CA를 사용한 인증서 인증 신뢰:CRL 유효성 검사의 경우 ID에 대한 신뢰도 를 선택합니다.
* **** ICA를 통한 인증서 인증 신뢰:[ID에 대한 신뢰만]을 선택합니다. ICA는 인증서 인증을 신뢰할 수 없습니다. 인증서 인증을 위한 ICA를 신뢰하는 경우 ICA는 경로 작성을 위한 CA가 됩니다. ICA가 인증서 인증 및 ID에 대해 신뢰되는 경우 ICA가 CA가 되므로 CA 공급업체 인증서가 무시됩니다.
* **** HTTP를 사용하는 OCSP Server에 대한 신뢰:OSCP 응답 서버가 HTTP 위치에 있는 경우 SSL 연결에 대한 트러스트를 선택해야 합니다. OSCP 응답자에게 CRL 유효성 검사가 필요한 경우 ID에 대한 트러스트를 선택해야 합니다.
* **** Adobe 루트:[SSL 연결] 또는 [OCSP Server Trust Store 유형]을 선택하지 마십시오. Adobe 루트는 SSL 연결 및 OCSP Server에 대해 신뢰할 수 없습니다. Adobe는 OCSP 및 SSL 인증서를 발행하지 않습니다. Adobe Root는 암시적으로 별칭 이름=&quot;ADOBEROOT&quot;로 신뢰됩니다.

X509v3 인증서만 지원됩니다. 이 인증서 유형은 바이너리 DER 인코딩 파일(.cer 파일) 또는 동일한 DER 인코딩 인증서의 Base64로 인코딩된 버전(PEM(Privacy Enhanced Mail) 포맷의 X509 인증서 포함)을 포함하는 텍스트 파일로 제공할 수 있습니다.

서명 확인을 완료하는 데 필요한 인증서는 동일한 저장소(HSM 또는 데이터베이스)에 있어야 합니다.

Trust Manager API를 사용하여 인증서를 가져오고 삭제할 수도 있습니다. 자세한 내용은 AEM 양식을 [사용한 프로그래밍의 &quot;Trust Manager API를 사용하여 인증서 가져오기&quot; 및 &quot;Trust Manager API를 사용하여 인증서](https://www.adobe.com/go/learn_aemforms_programming_63)삭제&quot;를 참조하십시오.

## 인증서 가져오기 {#import-a-certificate}

1. 관리 콘솔에서 설정 > **[!UICONTROL 트러스트 저장소 관리 > 인증서를 클릭합니다]**.
1. [가져오기]를 클릭하고 [Trust Store 유형]에서 다음 옵션 중 하나를 선택합니다.

   * **** SSL 연결에 대한 신뢰:AEM 양식에서 인증서를 사용하여 SSL을 통해 외부 시스템에 연결할 수 있도록 지정합니다.
   * **** 서명 인증 신뢰:문서 서명 작업에서 작성자 디지털 서명을 인증하기 위해 인증서를 신뢰할 수 있도록 지정합니다.
   * **** 서명에 대한 신뢰:비작성자의 디지털 서명에 대한 문서 서명 작업에서 인증서를 신뢰할 수 있도록 지정합니다.
   * **** 인증서 인증에 대한 신뢰:인증서 또는 스마트 카드 인증을 사용하여 사용자를 인증하기 위해 AEM Forms에서 인증서를 사용하도록 지정합니다.
   * **** OCSP Server에 대한 신뢰:AEM 양식에서 인증서를 사용하여 외부 OCSP 응답자에 연결할 수 있도록 지정합니다.
   * **** ID에 대한 신뢰:위에서 지정한 유형 이외의 정보를 신뢰하는 데 인증서를 사용할 수 있도록 지정합니다.
   >[!NOTE]
   >
   >Trust Store는 인증서 인증, 서명, 인증 서명 및 ID를 위해 Adobe 루트 인증서를 묵시적으로 신뢰합니다.

1. 별칭 상자에 인증서의 식별자를 입력합니다.
1. 찾아보기를 **[!UICONTROL 클릭하여]** 인증서를 찾은 다음 확인을 **[!UICONTROL 클릭합니다]**.

## 인증서 내보내기 {#export-a-certificate}

1. 관리 콘솔에서 설정 > **[!UICONTROL 트러스트 저장소 관리 > 인증서를 클릭합니다]**.
1. 내보낼 인증서의 별칭 이름을 클릭합니다. 인증서 **[!UICONTROL 세부]** 사항 페이지가 표시됩니다.
1. 내보내기를 **[!UICONTROL 클릭하고]**, 지침에 따라 인증서를 내보낸 다음 확인을 **[!UICONTROL 클릭합니다]**.

## 인증서의 신뢰 설정 및 트러스트 저장소 유형 편집 {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. 관리 콘솔에서 설정 > **[!UICONTROL 트러스트 저장소 관리 > 인증서를 클릭합니다]**.
1. 편집할 인증서의 별칭 이름을 클릭합니다.
1. 인증서 **[!UICONTROL 업데이트를 클릭합니다]**.
1. 인증서의 별칭 이름을 변경하려면 별칭 상자에 새 이름을 입력합니다.
1. 인증서에 대한 트러스트 저장소 형식을 업데이트하려면 해당 트러스트 저장소 형식을 선택합니다.
1. 정책 제한을 업데이트하려면 인증서 정책 상자에 정책 정보를 입력한 다음 확인을 **[!UICONTROL 클릭합니다]**.

## 인증서 삭제 {#delete-a-certificate}

1. 관리 콘솔에서 설정 > **[!UICONTROL 트러스트 저장소 관리 > 인증서를 클릭합니다]**.
1. 삭제할 인증서의 확인란을 선택하고 [삭제] **[!UICONTROL 를]**&#x200B;클릭한 다음 [확인]을 **[!UICONTROL 클릭합니다]**.

