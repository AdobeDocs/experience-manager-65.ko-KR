---
title: 편지 PDF 미리 보기의 사용자 지정 워터마크
description: 편지 PDF 미리 보기에서 사용자 지정 워터마크를 만드는 방법을 알아봅니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: 7d90fade-1ca4-41d8-bbf9-45490465784a
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 1%

---

# 편지 PDF 미리 보기의 사용자 지정 워터마크{#custom-watermark-in-letter-pdf-preview}

## 개요 {#overview}

서신 만들기 UI에서 에이전트 사용자는 전자 메일 또는 인쇄와 같은 사후 처리로 전송되는 최종 모양으로 서신을 미리 봅니다.

이 데이터의 무단 사용을 방지하기 위해 조직은 미리보기 PDF에 워터마크를 적용할 수 있습니다. 기본 워터마크는 &quot;PREVIEW&quot;이며 PDF 전체에 나타납니다.

미리 보기 PDF에서 워터마크를 사용하려면 https://&#39;[server]:[port]&#39;/system/console/configMgr의 **[!UICONTROL 서신 관리 구성]**&#x200B;에서 **[!UICONTROL 미리 보기 중에 워터마크 적용]** 옵션을 선택하십시오.

![기본 워터마크](assets/default-watermark.png)

다음 단계를 사용하여 워터마크의 텍스트와 모양을 사용자 정의할 수 있습니다.

## 서신 만들기 UI의 PDF 미리 보기에서 워터마크 맞춤화 {#customizewatermark-}

1. `https://'[server]:[port]'/[ContextPath]/crx/de`(으)로 이동하여 관리자로 로그인합니다.
1. 앱 폴더에서 경로/구조가 libs 폴더의 previewwatermark 폴더와 유사한 **[!UICONTROL previewwatermark]** 폴더를 만듭니다.

   1. 다음 경로에서 **previewwatermark** 폴더를 마우스 오른쪽 단추로 클릭하고 **오버레이 노드**&#x200B;를 선택합니다.

      `/libs/fd/cm/configFiles/previewwatermark`

   1. 오버레이 노드 대화 상자에 다음 값이 있는지 확인합니다.

      **경로:** /libs/fd/cm/configFiles/previewwatermark

      **오버레이 위치:** /apps/

      **노드 유형 일치:** 선택됨

      >[!NOTE]
      >
      >/libs 분기를 변경하지 마십시오. 이 분기는 다음과 같은 경우 언제든지 변경될 수 있으므로 수행한 모든 변경 사항이 손실될 수 있습니다.
      >
      >    
      >    
      >    * 인스턴스에서 업그레이드
      >    * 핫픽스 적용
      >    * 기능 팩 설치
      >    
      >

   1. **확인**&#x200B;을 클릭한 다음 **모두 저장**&#x200B;을 클릭합니다. 지정한 경로에 **[!UICONTROL previewwatermark]** 폴더가 만들어집니다.

1. &quot;/libs/fd/cm/configFiles/previewwatermark&quot; 폴더에서 &quot;/apps/fd/cm/configFiles/previewwatermark&quot; 폴더로 ddx 파일을 복사하여 붙여 넣고 **[!UICONTROL 모두 저장]**&#x200B;을(를) 클릭합니다.
1. /apps/fd/cm/configFiles/previewwatermark/ 아래의 ddx 파일에서 원하는 대로 변경합니다.

   ```xml
   <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
    <PDF result="output.pdf">
     <PDF source="input.pdf"/>
           <Watermark opacity="15%" rotation="45">
            <StyledText>
                     <p font-family="Georgia" font-size="70pt" color="black" font-weight="bold">
                         PREVIEW
                    </p>
            </StyledText>
           </Watermark>
    </PDF>
   </DDX>
   ```

   워터마크 모양, 텍스트 및 맞춤 사용자 지정에 대한 자세한 내용은 [어셈블러 서비스 및 DDX 참조](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf) 문서에서 워터마크 및 배경 추가 및 제거를 참조하십시오.

   >[!NOTE]
   >
   >ddx 파일에서 결과 및 소스에 대한 참조는 output.pdf 및 input.pdf와 변경되지 않은 상태로 유지되어야 합니다. ddx 파일의 이름도 변경하면 안 됩니다.

1. **모두 저장**&#x200B;을 클릭합니다.
