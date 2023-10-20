---
title: 웹 사이트 구조 설정
description: 만들 폴더를 포함하여 웹 사이트 구조를 설정하는 방법에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 1f60a0d4-a272-45e8-9742-4b706be8502e
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 1%

---

# 웹 사이트 구조 설정 {#setup-website-structure}

웹 사이트를 설정하려면 아래 지침에 따라 다음 위치에 만들 폴더에 대해 설명합니다.

* `/apps/an-scf-sandbox`

  사용자 정의 응용 프로그램 및 템플릿이 있는 위치입니다.

* `/etc/designs/an-scf-sandbox`

  여기에서 다운로드 가능한 디자인 요소가 있습니다.

* `/content/an-scf-sandbox`

  여기에서 다운로드 가능한 웹 페이지를 볼 수 있습니다.

이 자습서의 코드는 기본 폴더 이름이 애플리케이션, 디자인 및 컨텐츠에 대해 동일해야 합니다. 웹 사이트의 다른 이름을 선택하는 경우 항상 바꾸기 `an-scf-sandbox` 을 선택합니다.

>[!NOTE]
>
>이름 정보:
>
>* CRXDE에 표시되는 이름은 주소 지정 가능한 컨텐츠의 경로를 형성하는 노드 이름입니다.
>* 노드 이름에 공백이 포함될 수 있지만 URI에 사용할 경우 공백을 &#39;%20&#39; 또는 &#39;+&#39;로 인코딩해야 합니다.
>* 노드 이름에는 하이픈과 밑줄이 포함될 수 있지만 Java™ 파일 내에서 패키지 이름으로 참조되는 경우 인코딩해야 합니다. 하이픈과 밑줄은 모두 밑줄 다음에 유니코드 값이 오는 밑줄로 이스케이프됩니다.
>
* 하이픈이 &#39;_002d&#39;가 됨
* 밑줄이 &#39;_005f&#39;가 됨

## 애플리케이션 디렉터리(/apps) 설정 {#setup-the-application-directory-apps}

저장소의 /apps 디렉터리에는 /content 디렉터리에서 제공하는 페이지의 비헤이비어와 렌더링을 구현하는 코드가 들어 있습니다.

/apps 디렉토리는 보호되며 /content 및 /etc/designs 디렉토리처럼 공개적으로 액세스할 수 없습니다.

1. 만들기 `/apps/an-scf-sandbox` 폴더를 삭제합니다.

   사용 **[!UICONTROL CRXDE Lite]**, 탐색기 창

   1. 다음 항목 선택 `/apps` 폴더를 삭제합니다.
   1. 마우스 오른쪽 버튼 클릭 **[!UICONTROL 만들기]**... 또는 아래로 당기십시오. **[!UICONTROL 만들기...]** 메뉴 아래의 제품에서 사용할 수 있습니다.
   1. 선택 **[!UICONTROL 폴더 만들기...]**.
   1. 다음에서 **[!UICONTROL 폴더 만들기]** 대화 상자, 입력 `an-scf-sandbox`.
   1. **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

1. 만들기 **[!UICONTROL 구성 요소]** 하위 폴더.

   1. 다음 항목 선택 `/apps/an-scf-sandbox` 폴더를 삭제합니다.
   1. 클릭 **[!UICONTROL 만들기 > 폴더 만들기]**.
   1. 다음에서 **[!UICONTROL 폴더 만들기]** 대화 상자, 입력 **[!UICONTROL 구성 요소]**.
   1. **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

1. 만들기 **[!UICONTROL 템플릿]** 하위 폴더.

   1. 다음 항목 선택 `/apps/an-scf-sandbox` 폴더를 삭제합니다.
   1. 클릭 **[!UICONTROL 만들기 > 폴더 만들기]**.
   1. 다음에서 **[!UICONTROL 폴더 만들기]** 대화 상자, 입력 **[!UICONTROL 템플릿]**.
   1. **[!UICONTROL 확인]**&#x200B;을 클릭합니다.
   1. 다시 선택 `/apps/an-scf-sandbox`.
   1. 선택 **[!UICONTROL 모두 저장]**.

   다른 편집 프로세스와 마찬가지로 자주 저장해야 합니다. 데이터 입력 문제가 발생하는 경우 로그인 시간이 초과되었거나 이전 편집 내용을 저장해야 하기 때문일 수 있습니다.

1. 이제 CRXDE Lite의 탐색기 창에 있는 구조는 다음과 같습니다.

   ![crxde-template](assets/crxde-template.png)

## 디자인 디렉토리(/etc/designs) 설정 {#setup-the-design-directory-etc-designs}

/etc/designs 디렉토리에는 페이지 컨텐츠와 함께 다운로드할 이미지, 스크립트 및 스타일 시트가 포함되어 있습니다.

1. 클래식 UI에서 Designer 도구를 사용하려면 [https://&lt;server>:&lt;port>/miscadmin](http://localhost:4502/miscadmin).

   참고: CRXDE Lite을 사용하여 유형의 노드를 생성하는 경우 `cq:Page`, 액세스 제어 및 복제 가 페이지의 기본 설정으로 설정되지 않습니다.

1. 탐색기 창에서 **[!UICONTROL 디자인]** 폴더를 클릭한 다음 **[!UICONTROL 신규]** > **[!UICONTROL 새 페이지]**.

   다음을 입력합니다.

   * 제목: **[!UICONTROL SCF 샌드박스]**
   * 이름: **[!UICONTROL an-scf-sandbox]**
   * 선택 **[!UICONTROL 디자인 페이지 템플릿]**

   **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.

   ![design-template](assets/design-template.png)

1. &quot;SCF 샌드박스&quot; 폴더가 나타나지 않으면 탐색기 창을 새로 고칩니다.

1. CRXDE Lite(http:// localhost:4502/crx/de)로 돌아가서 /etc/designs를 확장하여 &quot;an-scf-sandbox&quot;라는 노드를 확인합니다.

   CRXDE의 오른쪽 아래 창에서 속성 탭, 액세스 제어 탭 및 복제 탭을 보고 디자인 페이지 템플릿을 사용하여 정의한 내용을 확인할 수 있습니다.

   ![crxde-configure-template](assets/crxde-configure-template.png)

## 콘텐츠 디렉터리(/content) 설정 {#setup-the-content-directory-content}

저장소의 /content 디렉토리는 웹 사이트 컨텐츠가 있는 위치입니다. /content 아래의 경로는 브라우저 요청에 대한 URL의 경로를 구성합니다.

*다음 이후* 다음 [페이지 템플릿](initial-app.md#createthepagetemplate) 는 초기 애플리케이션의 일부로 작성되며, 초기 페이지 콘텐츠는 템플릿을 기반으로 작성할 수 있습니다.... [**⇒**](initial-app.md)
