---
title: 웹 사이트 구조 설정
seo-title: 웹 사이트 구조 설정
description: 디렉토리 설정
seo-description: 디렉토리 설정
uuid: a31edcd5-dab8-4a42-953b-1d076c2182b2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d18c0ece-4c4f-499c-ac94-a9aaa7f883c4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 웹 사이트 구조 설정 {#setup-website-structure}

웹 사이트를 설정하려면 아래 지침에 따라 다음 위치에서 만들 폴더에 대해 설명합니다.

* `/apps/an-scf-sandbox`
사용자 정의 애플리케이션 및 템플릿이 상주하는 곳입니다

* `/etc/designs/an-scf-sandbox`
다운로드 가능한 디자인 요소가 있는 경우

* `/content/an-scf-sandbox`
다운로드 가능한 웹 페이지가 있는 위치

이 자습서의 코드는 애플리케이션, 디자인 및 컨텐츠에 대해 동일한 기본 폴더 이름을 사용합니다. 웹 사이트의 다른 이름을 선택한 경우 항상 선택한 이름으로 `an-scf-sandbox` 바꾸십시오.

>[!NOTE]
>
>이름 정보:
>
>* CRXDE에 표시되는 이름은 주소 지정 가능한 컨텐츠의 경로를 구성하는 노드 이름입니다.
>* 노드 이름에는 공백이 포함될 수 있지만 URI에서 사용할 경우 공백을 &#39;%20&#39; 또는 &#39;+&#39; 중 하나로 인코딩해야 합니다.
>* 노드 이름에는 하이픈 및 밑줄이 포함될 수 있지만 Java 파일 내에서 패키지 이름으로 참조할 때는 인코딩해야 합니다. 하이픈과 밑줄 모두 밑줄로 이스케이프되고 유니코드 값이 이어집니다.
>
>   * hyphen은 &#39;_002d&#39;가 됩니다.
>   * 밑줄이 &#39;_005f&#39;가 됩니다.

## 응용 프로그램 디렉토리(/apps) 설정 {#setup-the-application-directory-apps}

저장소의 /apps 디렉토리에는 /content 디렉토리에서 제공되는 페이지의 비헤이비어와 렌더링을 구현하는 코드가 포함되어 있습니다.

/apps 디렉토리는 보호되며 /content 및 /etc/designs 디렉토리에서처럼 공개적으로 액세스할 수 없습니다.

1. Create `/apps/an-scf-sandbox` folder.

   탐색기 **[!UICONTROL 창에서]** CRXDE Lite 사용

   1. 폴더 `/apps` 선택
   1. **[!UICONTROL 만들기...]**&#x200B;를 마우스 오른쪽 단추로&#x200B;**[!UICONTROL 클릭합니다.또는 만들기...]**&#x200B;를 아래로 끌어 옵니다.메뉴
   1. **[!UICONTROL 폴더]**&#x200B;만들기...를 선택합니다..
   1. 폴더 **[!UICONTROL 만들기]** 대화 상자에서 `an-scf-sandbox`
   1. **[!UICONTROL 확인]**&#x200B;을 클릭합니다

1. 구성 **[!UICONTROL 요소]** 하위 폴더를 만듭니다.

   1. 폴더 `/apps/an-scf-sandbox` 선택
   1. 만들기 **[!UICONTROL > 폴더 만들기를 클릭합니다.]**
   1. 폴더 **[!UICONTROL 만들기 대화]** 상자에서 **[!UICONTROL 구성 요소를 입력합니다.]**
   1. **[!UICONTROL 확인]**&#x200B;을 클릭합니다

1. 템플릿 **하위 폴더를 만듭니다&#x200B;**.

   1. 폴더 `/apps/an-scf-sandbox` 선택
   1. 만들기 **[!UICONTROL > 폴더 만들기를 클릭합니다.]**
   1. 폴더 **[!UICONTROL 만들기 대화]** 상자에서 **[!UICONTROL 템플릿을 입력합니다.]**
   1. **[!UICONTROL 확인]**&#x200B;을 클릭합니다
   1. 다시 선택 `/apps/an-scf-sandbox`
   1. 모두 **[!UICONTROL 저장을 선택합니다.]**
   모든 편집 프로세스와 마찬가지로 종종 비용을 절감할 수 있습니다. 데이터 입력 시 문제가 발생하면 로그인 시간이 초과되었거나 이전 편집 내용을 저장해야 할 수 있습니다.

1. CRXDE Lite의 탐색기 창에 있는 구조는 다음과 같이 표시됩니다.

   ![chlimage_1-44](assets/chlimage_1-44.png)

## 디자인 디렉토리 설정(/etc/designs) {#setup-the-design-directory-etc-designs}

/etc/designs 디렉토리에는 페이지 컨텐츠와 함께 다운로드할 이미지, 스크립트 및 스타일시트가 포함되어 있습니다.

1. 클래식 UI에서 디자이너 도구를 사용하려면 https://&lt;server>:&lt; [port>/miscadmin으로 이동합니다](http://localhost:4502/miscadmin).

   참고:CRXDE Lite를 사용하여 노드 유형을 만드는 `cq:Page`경우 액세스 제어 및 복제는 페이지에 대한 기본 설정으로 설정되지 않습니다.

1. 탐색기 창에서 디자인 **[!UICONTROL 폴더를 선택한]** 다음 새로 만들기 > **[!UICONTROL 새 페이지를 클릭합니다]**.

   Enter:

   * 제목:SCF **샌드박스**
   * 이름: **an-scf-sandbox**
   * 디자인 **페이지 템플릿 선택**
   **[!UICONTROL 만들기]**&#x200B;를 클릭합니다

   ![chlimage_1-45](assets/chlimage_1-45.png)

1. &quot;SCF 샌드박스&quot; 폴더가 나타나지 않으면 탐색기 창을 새로 고칩니다.

1. CRXDE Lite(http:// localhost:4502/crx/de)로 돌아가서 /etc/designs를 확장하여 &quot;an-scf-sandbox&quot;라는 노드를 확인합니다.

   CRXDE의 오른쪽 아래 창에서 속성 탭, 액세스 제어 탭 및 복제 탭을 보고 디자인 페이지 템플릿을 사용하여 정의된 내용을 볼 수 있습니다.

   ![chlimage_1-46](assets/chlimage_1-46.png)

## 콘텐트 디렉토리(/content) 설정 {#setup-the-content-directory-content}

응답의 /content 디렉토리는 웹 사이트 컨텐츠가 있는 곳입니다. /content 아래의 경로는 브라우저 요청에 대한 URL의 경로를 구성합니다.

*초기* 응용 프로그램의 일부로 [페이지 템플릿을](initial-app.md#createthepagetemplate) 만든 후, 템플릿을 기반으로 초기 페이지 컨텐츠를 만들 수 있습니다.... [**⇒**](initial-app.md)