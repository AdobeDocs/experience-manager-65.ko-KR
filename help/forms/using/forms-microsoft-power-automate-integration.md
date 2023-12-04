---
title: 적응형 양식 데이터를 Microsoft&reg; Power Automate에 연결하고 보내는 방법
description: 적응형 양식 데이터를 Microsoft&reg; Power Automate에 연결하고 전송하는 단계별 안내서입니다.
keywords: 적응형 Forms Microsoft Power Automate, Microsoft Power Automate에 적응형 Forms 데이터 제출
exl-id: a059627b-df12-454d-9e2c-cc56986b7de6
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 15%

---


# Microsoft® Power Automate에 적응형 양식 데이터 연결 및 제출 {#connect-adaptive-form-with-power-automate}

제출 시 Microsoft® Power Automate Cloud Flow를 실행하도록 적응형 양식을 구성할 수 있습니다. 구성된 적응형 양식은 캡처된 데이터, 첨부 파일 및 기록 문서를 처리를 위해 Power Automate Cloud Flow로 전송합니다. 이렇게 하면 Microsoft® Power Automate의 강력한 기능을 활용하면서 사용자 정의 데이터 캡처 환경을 빌드하여 캡처된 데이터를 중심으로 비즈니스 논리를 빌드하고 고객 워크플로를 자동화할 수 있습니다. 다음은 적응형 양식을 Microsoft® Power Automate와 통합한 후 수행할 수 있는 작업에 대한 몇 가지 예입니다.

* Power Automate 비즈니스 프로세스에서 적응형 양식 데이터 사용
* Power Automate를 사용하여 캡처된 데이터를 500개 이상의 데이터 소스 또는 공개적으로 사용 가능한 API로 전송
* 캡처된 데이터에 대해 복잡한 계산 수행
* 미리 정의된 일정에 따라 적응형 양식 데이터를 스토리지 시스템에 저장

적응형 양식 편집기는 **Microsoft® Power Automate 흐름 호출** 제출 액션을 제공하여 적응형 양식 데이터, 첨부 파일 및 기록 문서를 Power Automate Cloud Flow로 전송합니다. 제출 액션을 사용하여 캡처된 데이터를 Microsoft® Power Automate로 보내려면 [AEM Forms 작성자 인스턴스와 Microsoft® Power Automate 연결](#connect-your-aem-forms-instance-with-microsoft&reg;-power-automate)

## 사전 요구 사항

적응형 양식과 Microsoft® Power Automate를 연결하려면 다음이 필요합니다.

* Microsoft® Power Automate Premium 라이센스
* Microsoft® [전원 자동화 플로우](https://docs.microsoft.com/en-us/power-automate/create-flow-solution) (으)로 `When an HTTP request is received` 적응형 양식 제출 데이터 수락 트리거
* 다음을 보유한 Experience Manager 사용자 [Forms 작성자](/help/forms/using/forms-groups-privileges-tasks.md) 및 [Forms 관리자](/help/forms/using/forms-groups-privileges-tasks.md) 권한
* Microsoft® Power Automate에 연결하는 데 사용되는 계정은 적응형 양식에서 데이터를 받도록 구성된 Power Automate 흐름의 소유자입니다


## AEM Forms 인스턴스와 Microsoft® Power Automate 연결 {#connect-forms-server-with-power-automate}

다음 작업을 수행하여 AEM Forms 작성자 인스턴스를 Microsoft® Power Automate에 연결합니다.

1. [Microsoft 만들기](#ms-power-automate-application)
1. [Microsoft 만들기](#microsoft-power-automate-dataverse-cloud-configuration)
1. [Microsoft 만들기](#create-microsoft-power-automate-flow-cloud-configuration)
1. [Microsoft 게시](#publish-microsoft-power-automate-dataverse-cloud-configuration)

### Microsoft® Azure Active Directory 응용 프로그램 만들기 {#ms-power-automate-application}

1. 에 로그인 [Azure 포털](https://portal.azure.com/).
1. 선택 [!UICONTROL Azure Active Directory] 왼쪽 탐색에서.
1. 기본 디렉토리 페이지에서 다음을 선택합니다. [!UICONTROL 앱 등록] 왼쪽 패널에서 가져옵니다.
1. 앱 등록 페이지에서 새 등록을 클릭합니다.
1. 페이지에서 이름, 지원되는 계정 유형 및 리디렉션 URI를 지정합니다. 리디렉션 URI에서 다음을 지정하고 저장을 클릭합니다.
   * `https://[AEM Forms Author instance]/libs/fd/powerautomate/content/dataverse/config.html`
   * `https://[AEM Forms Author instance]/libs/fd/powerautomate/content/flowservice/config.html`

   ![Azure Active Directory 응용 프로그램 등록](assets/power-automate-application.png)

   >[!NOTE]
   >필요한 경우 인증 페이지에서 추가 리디렉션 URI를 지정할 수도 있습니다.
   > 지원되는 계정 유형의 경우 사용 사례에 따라 단일 테넌트, 여러 테넌트 또는 개인 Microsoft® 계정을 선택하십시오


1. 인증 페이지에서 다음 옵션을 활성화하고 저장을 클릭합니다.


   * 액세스 토큰(암시적 흐름에 사용됨)
   * ID 토큰(암시적 흐름과 하이브리드 흐름에 사용)

1. API 권한 페이지에서 권한 추가를 클릭합니다.
1. Microsoft® API에서 흐름 서비스를 선택하고 다음 권한을 선택합니다.
   * Flows.Manage.All
   * Flows.Read.All

   권한 추가 를 클릭하여 권한을 저장합니다.
1. API 권한 페이지에서 권한 추가를 클릭합니다. 내 조직에서 사용하고 있는 API 선택 및 검색 `DataVerse`.
1. user_impersonation을 활성화하고 권한 추가를 클릭합니다.
1. (선택 사항) 인증서 및 암호 페이지에서 새 클라이언트 암호를 클릭합니다. 클라이언트 암호 추가 화면에서 암호가 만료될 수 있는 설명 및 기간을 입력하고 추가를 클릭합니다. 비밀 문자열이 생성됩니다.
1. 조직별 메모 유지 [Dynamics 환경 URL](https://docs.microsoft.com/en-us/power-automate/web-api#compose-http-requests).

### Microsoft® Power Automate Dataverse 클라우드 구성 만들기 {#microsoft-power-automate-dataverse-cloud-configuration}

1. AEM Forms 작성자 인스턴스에서 **[!UICONTROL 도구]** ![망치](assets/hammer.png) > **[!UICONTROL 일반]** > **[!UICONTROL 구성 브라우저]**.
1. 다음에서 **[!UICONTROL 구성 브라우저]** 페이지, 선택 **[!UICONTROL 만들기]**.
1. 다음에서 **[!UICONTROL 구성 만들기]** 대화 상자, 지정 **[!UICONTROL 제목]** 구성의 경우 활성화 **[!UICONTROL 클라우드 구성]**, 및 선택 **[!UICONTROL 만들기]**. 이를 통해 Cloud Service를 저장하는 구성 컨테이너가 생성됩니다. 폴더 이름에는 공백이 없어야 합니다.
1. 다음으로 이동 **[!UICONTROL 도구]** ![망치](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft®® Power Automate Dataverse]** 이전 단계에서 생성한 구성 컨테이너를 엽니다.

   >[!NOTE]
   >
   적응형 양식을 만들 때에서 컨테이너 이름을 지정합니다 **[!UICONTROL 구성 컨테이너]** 필드.

1. 구성 페이지에서 을 선택합니다 **[!UICONTROL 만들기]** 만들려면 [!DNL Microsoft®® Power Automate Flow Service] AEM Forms의 구성
1. 다음에서 **[!UICONTROL Microsoft®® Power Automate용 Dataverse 서비스 구성]** 페이지, 지정 **[!UICONTROL 클라이언트 ID]** (애플리케이션 ID라고도 함), **[!UICONTROL 클라이언트 암호]**, **[!UICONTROL OAuth URL]** 및 **[!UICONTROL 동적 환경 URL]**. 의 클라이언트 ID, 클라이언트 암호, OAuth URL 및 동적 환경 URL 사용 [Microsoft® Azure Active Directory 응용 프로그램](#ms-power-automate-application) 이전 섹션에서 을(를) 만들었습니다. Microsoft® Azure Active Directory 애플리케이션 UI의 끝점 옵션을 사용하여 OAuth URL 찾기

   ![Microsoft Power Automate 애플리케이션 UI의 엔드포인트 옵션을 사용하여 OAuth URL 찾기](assets/endpoints.png)

1. 선택 **[!UICONTROL 연결]** . 메시지가 표시되면 Microsoft® Azure 계정에 로그인합니다. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

### Microsoft® Power Automate 플로우 서비스 클라우드 구성 생성 {#create-microsoft-power-automate-flow-cloud-configuration}

1. 다음으로 이동 **[!UICONTROL 도구]** ![망치](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft®® Power Automate 플로우 서비스]** 이전 섹션에서 만든 구성 컨테이너를 엽니다.

   >[!NOTE]
   >
   적응형 양식을 만들 때에서 컨테이너 이름을 지정합니다 **[!UICONTROL 구성 컨테이너]** 필드.
1. 구성 페이지에서 을 선택합니다 **[!UICONTROL 만들기]** 만들려면 [!DNL Microsoft®® Power Automate Flow Service] AEM Forms의 구성
1. 다음에서 **[!UICONTROL Microsoft®® Power Automate용 Dataverse 구성]** 페이지, 지정 **[!UICONTROL 클라이언트 ID]** (애플리케이션 ID라고도 함), **[!UICONTROL 클라이언트 암호]**, **[!UICONTROL OAuth URL]** 및 **[!UICONTROL 동적 환경 URL]**. 클라이언트 ID, 클라이언트 암호, OAuth URL 및 Dynamics 환경 ID를 사용합니다. Microsoft® Azure Active Directory 응용 프로그램 UI의 끝점 옵션을 사용하여 OAuth URL을 찾습니다. 를 엽니다. [내 흐름](https://us.flow.microsoft.com) 내 플로우 를 연결하고 선택합니다. URL에 나열된 ID를 Dynamics 환경 ID로 사용합니다.
1. 선택 **[!UICONTROL 연결]**. 메시지가 표시되면 Microsoft® Azure 계정에 로그인합니다. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

### Microsoft® Power Automate Dataverse 및 Microsoft® Power Automate Flow Service 클라우드 구성 모두 게시 {#publish-microsoft-power-automate-dataverse-cloud-configuration}

1. 다음으로 이동 **[!UICONTROL 도구]** ![망치](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft®® Power Automate Dataverse]** 이전에 만든 구성 컨테이너를 엽니다. [Microsoft® Power Automate Dataverse 클라우드 구성 만들기](#microsoft-power-automate-dataverse-cloud-configuration) 섹션.
1. 다음 항목 선택 `dataverse` 구성 및 선택 **[!UICONTROL 게시]**.
1. 게시 페이지에서 을 선택합니다. **[!UICONTROL 모든 구성]** 및 선택 **[!UICONTROL 게시]**. Power Automate Dataverse 및 Power Automate Flow Service 클라우드 구성을 모두 게시합니다.

이제 AEM Forms 작성자 인스턴스가 Microsoft® Power Automate에 연결됩니다. 이제 적응형 Forms 데이터를 Power Automate 흐름에 보낼 수 있습니다.

## Microsoft 호출® Power Automate 플로우 제출 액션을 사용하여 Power Automate 플로우에 데이터 전송 {#use-the-invoke-microsoft-power-automate-flow-submit-action}

이후 [AEM Forms 작성자 인스턴스와 Microsoft® Power Automate 연결](#connect-forms-server-with-power-automate)를 클릭하고, 다음 작업을 수행하여 캡처된 데이터를 양식 제출 시 Microsoft® 플로우로 전송하도록 적응형 양식을 구성합니다.

1. 작성자 인스턴스에 로그인하고 적응형 양식을 선택한 다음 를 클릭합니다. **[!UICONTROL 속성]**.
1. 구성 컨테이너에서 섹션에서 만든 컨테이너를 찾아 선택합니다 [Microsoft® Power Automate Dataverse 클라우드 구성 만들기](#microsoft-power-automate-dataverse-cloud-configuration), 및 선택 **[!UICONTROL 저장 및 닫기]**.
1. 편집할 적응형 양식을 열고 다음으로 이동합니다. **[!UICONTROL 제출]** 섹션에 있는 섹션을 참조하십시오.
1. 속성 컨테이너에서 **[!UICONTROL 작업 제출]** 선택 **[!UICONTROL Power Automate 플로우 호출]** 옵션을 선택합니다. 사용 가능한 Power Automate 플로우 목록은 **[!UICONTROL 전원 자동화 플로우]** 옵션을 선택합니다. 필요한 플로우를 선택하면 적응형 Forms 데이터가 제출 시 해당 플로우에 제출됩니다.

   ![제출 액션 구성](assets/submission.png)

>[!NOTE]
>
적응형 양식을 제출하기 전에 `When an HTTP Request is received` 아래 JSON 스키마로 트리거가 Power Automate 흐름에 추가됩니다.

```
        {
            "type": "object",
            "properties": {
                "attachments": {
                    "type": "array",
                    "items": {
                        "type": "object",
                        "properties": {
                            "filename": {
                                "type": "string"
                            },
                            "data": {
                                "type": "string"
                            },
                            "contentType": {
                                "type": "string"
                            },
                            "size": {
                                "type": "integer"
                            }
                        },
                        "required": [
                            "filename",
                            "data",
                            "contentType",
                            "size"
                        ]
                    }
                },
                "templateId": {
                    "type": "string"
                },
                "templateType": {
                    "type": "string"
                },
                "data": {
                    "type": "string"
                },
                "document": {
                    "type": "object",
                    "properties": {
                        "filename": {
                            "type": "string"
                        },
                        "data": {
                            "type": "string"
                        },
                        "contentType": {
                            "type": "string"
                        },
                        "size": {
                            "type": "integer"
                        }
                    }
                }
            }
        }
```

## 다음을 참조하십시오.

* [적응형 양식 만들기](create-an-adaptive-form-core-components.md)
* [제출 액션 구성](configuring-submit-actions.md)
* [Microsoft® Power Automate용 Adobe Experience Manager 커넥터](https://learn.microsoft.com/en-us/connectors/adobeexperiencemanag/)

