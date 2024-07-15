---
title: AEM 개발자를 위한 우수 사례
description: Adobe 엔지니어링 및 컨설팅 팀은 AEM 개발자를 위한 포괄적인 모범 사례 세트를 개발했습니다.
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 0a478e80-c1b2-46c1-a6be-794d78b85d69
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 4%

---

# 모범 사례{#best-practices}

## 개발자를 위한 우수 사례 - 시작하기 {#best-practices-for-developers-getting-started}

Adobe 엔지니어링 및 컨설팅 팀은 AEM 개발자를 위한 포괄적인 모범 사례 세트를 개발했습니다. Adobe 개발자는 고객 구현을 위한 핵심 AEM 제품 업데이트 및 고객 코드를 개발할 때 이러한 모범 사례를 준수합니다.

AEM 개발 프로젝트를 시작하기 전에 먼저 다음 모범 사례를 검토하십시오.

* [개발 사례](/help/sites-developing/development-practices.md)
* [콘텐츠 아키텍처](/help/sites-developing/content-architecture.md)
* [소프트웨어 아키텍처](/help/sites-developing/software-architecture.md)
* [코딩 팁](/help/sites-developing/coding-tips.md)
* [코드 함정](/help/sites-developing/code-pitfalls.md)
* [JCR 상호 작용](/help/sites-developing/jcr-integration.md)
* [OSGi 번들](/help/sites-developing/osgi-bundles.md)
* [Java API 모범 사례](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

### 추가 모범 사례 정보 {#additional-best-practices-information}

다음 영역에는 개발 모범 사례와 관련된 설명서가 있습니다.

* [Sites](#sites)
* [커뮤니티](/help/sites-developing/best-practices.md#communities)
* [도구/HTL](/help/sites-developing/best-practices.md#tooling-htl)

특정 문서는 다음에 나오는 표에 설명되어 있고 연결됩니다.

관리, 배포, 유지 관리 또는 작성에 대한 우수 사례는 다음 중 하나를 참조하십시오.

* [모범 사례 관리](/help/sites-administering/administer-best-practices.md)
* [작성 모범 사례](/help/sites-authoring/best-practices.md)
* [모범 사례 배포](/help/sites-deploying/best-practices.md)

## Sites {#sites}

웹 사이트 컨텐츠 관리 및 작성에는 다음과 같이 요약된 몇 가지 우수 사례가 있습니다.

<table>
 <tbody>
  <tr>
   <td>터치 기능이 지원되는 표준 UI에 대한 일부 이론입니다.</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">터치 지원 UI: 개념</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">터치 지원 UI: 구조</a></p> </td>
   <td>이러한 문서는 터치 지원 UI의 개념 및 구조에 대한 개요를 제공합니다.</td>
  </tr>
  <tr>
   <td>터치 지원 UI: 콘솔 사용자 지정 </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">터치 지원 UI 콘솔 사용자 지정</a></td>
   <td>이 문서에서는 터치 지원 UI의 콘솔을 확장하는 가장 좋은 방법에 대해 설명합니다.</td>
  </tr>
  <tr>
   <td>터치 지원 UI: 페이지 작성 사용자 지정</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">터치 지원 UI 페이지 작성 사용자 지정</a></td>
   <td>터치 사용 UI의 페이지 작성을 확장하는 방법을 설명합니다.</td>
  </tr>
  <tr>
   <td>워크플로</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">워크플로 개발 및 확장</a></td>
   <td><p>워크플로를 사용하면 AEM(Adobe Experience Manager) 활동을 자동화할 수 있으며 AEM 환경에서 발생하는 대량의 처리를 나타낼 수 있으므로 워크플로 구현을 신중하게 계획하는 것이 좋습니다.</p> </td>
  </tr>
 </tbody>
</table>

## 커뮤니티 {#communities}

[AEM Communities](/help/communities/overview.md)을(를) 사용하면 온-프레미스 커뮤니티를 만들고 관리할 수 있습니다.

커뮤니티에 대한 몇 가지 우수 사례가 여기에 설명되어 있습니다.

|  |  |  |
|---|---|---|
| 사용자 생성 콘텐츠 작업 우수 사례(UGC) | [코딩 지침](/help/communities/code-guide.md) | [소셜 구성 요소 프레임워크](/help/communities/scf.md)(SCF)에 대한 유연한 휴대용 코드 개발 지침입니다. |
| Communities 구성 요소의 사용 예 | [커뮤니티 구성 요소 안내서](/help/communities/components-guide.md) | 대화형 개발 도구. |

## 도구/HTL {#tooling-htl}

HTML 템플릿 언어(HTL)는 AEM 6.0과 함께 도입된 새로운 HTML 템플릿 시스템입니다. AEM의 기본 템플릿 시스템으로 JSP 및 ESP를 대체합니다.

|  |  |  |
|---|---|---|
| HTL 개요 | [HTL 개요 및 구문](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) | 이 문서에서는 HTL 정의, HTL로 이동하는 방법, 샘플 프로젝트, 구문, 표현식 및 문에 대해 설명합니다 |
| Java에서 API 사용 | [HTL Java Use-API](https://helpx.adobe.com/experience-manager/htl/using/use-api.html) | HTL Java Use-API를 사용하면 HTL 파일이 사용자 지정 Java 클래스의 도우미 메서드에 액세스할 수 있습니다. |

>[!NOTE]
>
>핵심 구성 요소, 편집 가능한 템플릿, 클라이언트 라이브러리 및 구성 요소 개발에 대해 자세히 설명하는 다중 파트 튜토리얼을 통해 새로운 AEM 프로젝트를 설정하는 것이 좋습니다.
>[AEM Sites 시작하기 - WKND 자습서](https://helpx.adobe.com/kr/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)
