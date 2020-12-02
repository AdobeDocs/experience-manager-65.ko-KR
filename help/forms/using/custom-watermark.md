---
title: 문자 PDF 미리 보기의 사용자 정의 워터마크
seo-title: 문자 PDF 미리 보기의 사용자 정의 워터마크
description: PDF 미리 보기에서 사용자 정의 워터마크를 만드는 방법을 알아봅니다.
seo-description: PDF 미리 보기에서 사용자 정의 워터마크를 만드는 방법을 알아봅니다.
uuid: 5adfede3-9b38-4a12-bf14-6d80cfb0a05a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: adc7ec13-0675-4071-9c4c-e238202d9d85
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---


# 문자 PDF 미리 보기의 사용자 정의 워터마크{#custom-watermark-in-letter-pdf-preview}

## 개요 {#overview}

통신 만들기 UI에서 에이전트 사용자는 전자 우편 또는 인쇄와 같이 게시 프로세싱으로 보내지는 마지막 모양으로 메시지를 미리 봅니다.

조직에서 이 데이터의 무단 사용을 방지하기 위해 미리 보기 PDF에 워터마크를 적용할 수 있습니다. 기본 워터마크는 PDF에 표시되는 &quot;PREVIEW&quot;입니다.

미리 보기 PDF에서 워터마크를 활성화하려면 https://&#39;[server]포트[/>포트]/system/console/configMgr의 **[!UICONTROL 통신 관리 구성]**&#x200B;에서 **[!UICONTROL 워터마크 적용]** 미리 보기 옵션을 선택합니다.

![default-watermark](assets/default-watermark.png)

다음 단계에 따라 워터마크의 텍스트와 모양을 사용자 정의할 수 있습니다.

## 통신 UI 만들기 {#customizewatermark-}에서 PDF 미리 보기에서 워터마크 사용자 정의

1. `https://'[server]:[port]'/[ContextPath]/crx/de`으로 이동하고 관리자로 로그인합니다.
1. 앱 폴더에서 libs 폴더의 미리 보기 워터마크 폴더와 유사한 경로/구조를 가진 **[!UICONTROL previewwatermark]**&#x200B;라는 폴더를 만듭니다.

   1. 다음 경로에서 **previewwatermark** 폴더를 마우스 오른쪽 단추로 클릭하고 **Overlay Node**&#x200B;을 선택합니다.

      `/libs/fd/cm/configFiles/previewwatermark`

   1. [오버레이 노드] 대화 상자에 다음 값이 있는지 확인합니다.

      **경로:** /libs/fd/cm/configFiles/previewwatermark

      **오버레이 위치:** /apps/

      **일치 노드 유형:** 선택됨

      >[!NOTE]
      >
      >/libs 분기에서 변경하지 마십시오. 이 분기는 다음과 같이 언제든지 변경할 수 있으므로 변경 사항이 손실될 수 있습니다.
      >
      >    
      >    
      >    * 인스턴스 업그레이드
      >    * 핫픽스 적용
      >    * 기능 팩 설치


   1. **확인**&#x200B;을 클릭한 다음 **모두 저장**&#x200B;을 클릭합니다. **[!UICONTROL previewwatermark]** 폴더가 지정된 경로에 생성됩니다.



1. &quot;/libs/fd/cm/configFiles/previewwatermark&quot; 폴더에서 &quot;/apps/fd/cm/configFiles/previewwatermark&quot; 폴더로 dx 파일을 복사하여 붙여 넣고 **[!UICONTROL 모두 저장]**&#x200B;을 클릭합니다.
1. /apps/fd/cm/configFiles/previewwatermark/ 아래의 ddx 파일에서 원하는 변경 작업을 수행합니다.

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

   워터마크 모양, 텍스트 및 정렬 사용자 지정에 대한 자세한 내용은 [어셈블러 서비스 및 DDX 참조](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf) 문서에서 워터마크 및 배경 추가 및 제거를 참조하십시오.

   >[!NOTE]
   >
   >ddx 파일에서 결과 및 소스에 대한 참조는 output.pdf 및 input.pdf로 변경되지 않은 상태로 유지됩니다. 파일 대화 상자의 이름도 변경할 수 없습니다.

1. **모두 저장**&#x200B;을 클릭합니다.

