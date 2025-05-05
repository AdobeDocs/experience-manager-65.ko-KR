---
title: 적응형 양식 데이터를 Microsoft&reg; Power Automate에 연결하고 전송하는 방법
description: 적응형 양식 데이터를 Microsoft&reg; Power Automate에 연결하고 전송하는 단계별 안내서입니다.
keywords: 적응형 Forms Microsoft Power Automate, Microsoft Power Automate에 적응형 Forms 데이터 제출
feature: Adaptive Forms,Foundation Components
exl-id: 3fd26ddb-d247-462f-a0f6-8af6166516c1
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
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

적응형 양식 편집기는 **Microsoft® Power Automate 흐름 호출** 제출 액션을 제공하여 적응형 양식 데이터, 첨부 파일 및 기록 문서를 Power Automate Cloud Flow로 전송합니다. 제출 액션을 사용하여 캡처된 데이터를 Microsoft® Power Automate로 보내려면 [AEM Forms 작성자 인스턴스를 Microsoft® Power Automate에 연결] (#connect-your-aem-forms-instance-with-microsoft&reg;-power-automate)합니다

## 사전 요구 사항

적응형 양식과 Microsoft® Power Automate를 연결하려면 다음이 필요합니다.

* Microsoft® Power Automate Premium 라이센스
* 적응형 양식 제출 데이터를 수락하기 위한 `When an HTTP request is received` 트리거를 사용하는 Microsoft® [Power Automate 흐름](https://docs.microsoft.com/en-us/power-automate/create-flow-solution)
* [Forms 작성자](/help/forms/using/forms-groups-privileges-tasks.md) 및 [Forms 관리자](/help/forms/using/forms-groups-privileges-tasks.md) 권한을 가진 Experience Manager 사용자
* Microsoft® Power Automate에 연결하는 데 사용되는 계정은 적응형 양식에서 데이터를 받도록 구성된 Power Automate 흐름의 소유자입니다


## AEM Forms 인스턴스와 Microsoft® Power Automate 연결 {#connect-forms-server-with-power-automate}

다음 작업을 수행하여 AEM Forms 작성자 인스턴스를 Microsoft® Power Automate에 연결합니다.

1. [Microsoft 만들기](#ms-power-automate-application)
1. [Microsoft 만들기](#microsoft-power-automate-dataverse-cloud-configuration)
1. [Microsoft 만들기](#create-microsoft-power-automate-flow-cloud-configuration)
1. [Publish Microsoft](#publish-microsoft-power-automate-dataverse-cloud-configuration)

### Microsoft® Azure Active Directory 응용 프로그램 만들기 {#ms-power-automate-application}

1. [Azure 포털](https://portal.azure.com/)에 로그인합니다.
1. 왼쪽 탐색에서 [!UICONTROL Azure Active Directory]를 선택합니다.
1. 기본 디렉터리 페이지의 왼쪽 패널에서 [!UICONTROL 앱 등록]을 선택합니다.
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
1. API 권한 페이지에서 권한 추가를 클릭합니다. 내 조직에서 사용하는 API를 선택하고 `DataVerse`을(를) 검색합니다.
1. user_impersonation을 활성화하고 권한 추가를 클릭합니다.
1. (선택 사항) 인증서 및 암호 페이지에서 새 클라이언트 암호를 클릭합니다. 클라이언트 암호 추가 화면에서 암호가 만료될 수 있는 설명 및 기간을 입력하고 추가를 클릭합니다. 비밀 문자열이 생성됩니다.
1. 조직별 [Dynamics 환경 URL](https://docs.microsoft.com/en-us/power-automate/web-api#compose-http-requests)을(를) 메모해 두십시오.

### Microsoft® Power Automate Dataverse 클라우드 구성 만들기 {#microsoft-power-automate-dataverse-cloud-configuration}

1. AEM Forms 작성자 인스턴스에서 **[!UICONTROL 도구]** ![hammer](assets/hammer.png) > **[!UICONTROL 일반]** > **[!UICONTROL 구성 브라우저]**&#x200B;로 이동합니다.
1. **[!UICONTROL 구성 브라우저]** 페이지에서 **[!UICONTROL 만들기]**&#x200B;를 선택합니다.
1. **[!UICONTROL 구성 만들기]** 대화 상자에서 구성에 대한 **[!UICONTROL 제목]**&#x200B;을 지정하고 **[!UICONTROL 클라우드 구성]**&#x200B;을 사용하도록 설정하고 **[!UICONTROL 만들기]**&#x200B;를 선택합니다. 이를 통해 Cloud Service를 저장하는 구성 컨테이너가 생성됩니다. 폴더 이름에는 공백이 없어야 합니다.
1. **[!UICONTROL 도구]** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft®® Power Automate Dataverse]**(으)로 이동하여 이전 단계에서 만든 구성 컨테이너를 엽니다.

   >[!NOTE]
   >
   >적응형 양식을 만들 때 **[!UICONTROL 구성 컨테이너]** 필드에 컨테이너 이름을 지정하십시오.

1. 구성 페이지에서 **[!UICONTROL 만들기]**&#x200B;를 선택하여 AEM Forms에서 [!DNL Microsoft®® Power Automate Flow Service] 구성을 만듭니다.
1. **[!UICONTROL Microsoft®® Power Automate에 대한 Dataverse 서비스 구성]** 페이지에서 **[!UICONTROL 클라이언트 ID]**(응용 프로그램 ID라고도 함), **[!UICONTROL 클라이언트 암호]**, **[!UICONTROL OAuth URL]** 및 **[!UICONTROL 동적 환경 URL]**&#x200B;을 지정합니다. 이전 섹션에서 만든 [Microsoft® Azure Active Directory 응용 프로그램](#ms-power-automate-application)의 클라이언트 ID, 클라이언트 암호, OAuth URL 및 동적 환경 URL을 사용합니다. Microsoft® Azure Active Directory 애플리케이션 UI의 끝점 옵션을 사용하여 OAuth URL 찾기

   ![Microsoft Power Automate 응용 프로그램 UI의 끝점 옵션을 사용하여 OAuth URL 찾기](assets/endpoints.png)

1. **[!UICONTROL 연결]** 을 선택합니다. 메시지가 표시되면 Microsoft® Azure 계정에 로그인합니다. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

### Microsoft® Power Automate 플로우 서비스 클라우드 구성 생성 {#create-microsoft-power-automate-flow-cloud-configuration}

1. **[!UICONTROL 도구]** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft®® Power Automate 흐름 서비스]**(으)로 이동하여 이전 섹션에서 만든 구성 컨테이너를 엽니다.

   >[!NOTE]
   >
   >적응형 양식을 만들 때 **[!UICONTROL 구성 컨테이너]** 필드에 컨테이너 이름을 지정하십시오.
1. 구성 페이지에서 **[!UICONTROL 만들기]**&#x200B;를 선택하여 AEM Forms에서 [!DNL Microsoft®® Power Automate Flow Service] 구성을 만듭니다.
1. **[!UICONTROL Microsoft®® Power Automate에 대한 Dataverse 구성]** 페이지에서 **[!UICONTROL 클라이언트 ID]**(응용 프로그램 ID라고도 함), **[!UICONTROL 클라이언트 암호]**, **[!UICONTROL OAuth URL]** 및 **[!UICONTROL 동적 환경 URL]**&#x200B;을 지정합니다. 클라이언트 ID, 클라이언트 암호, OAuth URL 및 Dynamics 환경 ID를 사용합니다. Microsoft® Azure Active Directory 응용 프로그램 UI의 끝점 옵션을 사용하여 OAuth URL을 찾습니다. [내 흐름](https://us.flow.microsoft.com) 링크를 열고 [내 흐름]을 선택합니다. URL에 나열된 ID를 Dynamics 환경 ID로 사용합니다.
1. **[!UICONTROL 연결]**&#x200B;을 선택합니다. 메시지가 표시되면 Microsoft® Azure 계정에 로그인합니다. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

### Publish Microsoft® Power Automate Dataverse 및 Microsoft® Power Automate Flow Service 클라우드 구성 모두 {#publish-microsoft-power-automate-dataverse-cloud-configuration}

1. **[!UICONTROL 도구]** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft®® Power Automate Dataverse]**(으)로 이동하여 이전 [Microsoft 만들기® Power Automate Dataverse 클라우드 구성](#microsoft-power-automate-dataverse-cloud-configuration) 섹션에서 만든 구성 컨테이너를 엽니다.
1. `dataverse` 구성을 선택하고 **[!UICONTROL Publish]**&#x200B;을(를) 선택합니다.
1. Publish 페이지에서 **[!UICONTROL 모든 구성]**&#x200B;을 선택하고 **[!UICONTROL Publish]**&#x200B;을 선택합니다. Publish Power Automate Dataverse 및 Power Automate Flow Service 클라우드 구성 모두

이제 AEM Forms 작성자 인스턴스가 Microsoft® Power Automate에 연결됩니다. 이제 적응형 Forms 데이터를 Power Automate 흐름에 보낼 수 있습니다.

## Microsoft 호출® Power Automate 플로우 제출 액션을 사용하여 Power Automate 플로우에 데이터 전송 {#use-the-invoke-microsoft-power-automate-flow-submit-action}

[AEM Forms 작성자 인스턴스와 Microsoft® Power Automate를 연결](#connect-forms-server-with-power-automate)한 후 다음 작업을 수행하여 캡처된 데이터를 양식 제출 시 Microsoft® 플로우로 전송하도록 적응형 양식을 구성하십시오.

1. 작성자 인스턴스에 로그인하고 적응형 양식을 선택한 다음 **[!UICONTROL 속성]**&#x200B;을 클릭합니다.
1. 구성 컨테이너에서 [Microsoft 만들기® Power Automate Dataverse 클라우드 구성](#microsoft-power-automate-dataverse-cloud-configuration) 섹션에서 만든 컨테이너를 찾아 선택한 다음 **[!UICONTROL 저장 및 닫기]**&#x200B;를 선택합니다.
1. 편집할 적응형 양식을 열고 적응형 양식 컨테이너 속성의 **[!UICONTROL 제출]** 섹션으로 이동합니다.
1. 속성 컨테이너에서 **[!UICONTROL 작업 제출]**&#x200B;에 대해 **[!UICONTROL Power Automate 흐름 호출]** 옵션을 선택합니다. **[!UICONTROL Power Automate 흐름]** 옵션에서 사용 가능한 Power Automate 흐름 목록을 사용할 수 있습니다. 필요한 플로우를 선택하면 적응형 Forms 데이터가 제출 시 해당 플로우에 제출됩니다.

   ![제출 액션 구성](assets/submission.png)

>[!NOTE]
>
> 적응형 양식을 제출하기 전에 아래 JSON 스키마를 사용하는 `When an HTTP Request is received` 트리거가 Power Automate 흐름에 추가되었는지 확인하십시오.

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
