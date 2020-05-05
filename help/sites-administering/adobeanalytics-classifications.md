---
title: Adobe 분류
seo-title: Adobe 분류
description: Adobe 분류에 대해 자세히 알아보십시오.
seo-description: Adobe 분류에 대해 자세히 알아보십시오.
uuid: 57fb59f4-da90-4fe7-a5b1-c3bd51159a16
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6787511a-2ce0-421a-bcfb-90d5f32ad35e
translation-type: tm+mt
source-git-commit: 4456b5366387c27810c407d6ac9e6c17fc290269

---


# Adobe Classifications{#adobe-classifications}

Adobe Classifications는 분류 데이터를 [Adobe Analytics](/help/sites-administering/adobeanalytics.md) 로 예약된 방식으로 내보냅니다. 내보내기 프로그램은 com.adobe.cq.scheeded.exporter. **Exporter의 구현입니다**.

이를 구성하려면:

1. [ **도구**], [ **클라우드 서비스**]를 선택한 다음 **레거시****Cloud 서비스]를**&#x200B;선택합니다.
1. Adobe **Analytics로** 스크롤하고 구성 **표시를 선택합니다**.
1. Adobe Analytics 구성 옆에 있는 **[+]** 링크를 클릭합니다.

1. 프레임워크 **만들기** 대화 상자에서 다음을 수행합니다.

   * 제목을 **지정합니다**.
   * 원할 경우, 저장소에 프레임워크 세부 **정보를 저장하는 노드에**&#x200B;대해 이름을 지정할 수 있습니다.
   * Adobe **Analytics 분류 선택**
   만들기를 **클릭합니다**.

   ![프레임워크 만들기 대화 상자](assets/aa-25.png)

1. [분류 **설정** ] 대화 상자가 열려 편집을 위해 표시됩니다.

   ![분류 설정 대화 상자](assets/aa-classifications-settings.png)

   속성은 다음과 같습니다.

   | **필드** | **설명** |
   |---|---|
   | 활성화됨 | 예 **를** 선택하여 Adobe 분류 설정을 활성화합니다. |
   | 충돌 시 덮어쓰기 | 데이터 충돌 **을** 덮어쓰려면 예를 선택합니다. 기본적으로 [아니요]로 **설정됩니다**. |
   | 삭제가 처리되었습니다 | [예]로 **설정된**&#x200B;경우 내보낸 노드를 삭제합니다. 기본값은 **False입니다**. |
   | 작업 내보내기 설명 | Adobe 분류 작업에 대한 설명을 입력합니다. |
   | 알림 이메일 | Adobe 분류 알림의 이메일 주소를 입력합니다. |
   | 보고서 세트 | 가져오기 작업을 실행할 보고서 세트를 입력합니다. |
   | 데이터 세트 | 가져오기 작업을 실행할 데이터 집합 관계 ID를 입력합니다. |
   | 변환자 | 드롭다운 메뉴에서 변환기 구현을 선택합니다. |
   | 데이터 소스 | 데이터 컨테이너의 경로로 이동합니다. |
   | 일정 내보내기 | 내보내기 일정을 선택합니다. 기본값은 30분마다 있습니다. |

1. Click **OK** to save your settings.

## 페이지 크기 수정 {#modifying-page-size}

레코드는 페이지에서 처리됩니다. 기본적으로 Adobe 분류는 페이지 크기가 1000인 페이지를 만듭니다.

페이지 크기는 Adobe 분류에서 정의당 최대 25,000개이며 펠릭스 콘솔에서 수정할 수 있습니다. 내보내는 동안 Adobe 분류는 소스 노드를 잠가 동시 수정을 방지합니다. 노드가 내보내기 후, 오류 발생 시 또는 세션이 닫히면 잠금 해제됩니다.

페이지 크기를 변경하려면 다음을 수행하십시오.

1. https://&lt;호스트>:&lt;포트>/system/console/configMgr의 OSGI 콘솔로 **이동하고** Adobe AEM 분류 내보내기 **옵션을 선택합니다**.

   ![aa-26](assets/aa-26.png)

1. 필요에 따라 **내보내기 페이지 크기를** 업데이트한 다음 저장을 **클릭합니다**.

## SAINTDefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>Adobe 분류는 이전에 SAINT Exporter라고 알려져 있었습니다.

Exporter는 Transformer를 사용하여 내보내기 데이터를 특정 형식으로 변형할 수 있습니다. Adobe Classifications의 경우 Transformer 인터페이스를 `SAINTTransformer<String[]>` 구현하는 하위 인터페이스가 제공됩니다. 이 인터페이스는 SAINT API에서 사용되는 데이터 유형을 제한하고 마커 인터페이스를 사용하여 선택 `String[]` 에 필요한 서비스를 찾습니다.

기본 구현 SAINTDefaultTransformer에서 내보내기 소스의 자식 리소스는 속성 이름이 있는 레코드로 처리되고 속성 값이 값으로 처리됩니다. Key **** 열은 첫 번째 열로 자동으로 추가되며 값은 노드 이름입니다. 지정된 속성(포함 `:`)은 무시됩니다.

*노드 구조:*

* id-classification `nt:unstructured`

   * 1 `nt:unstructured`

      * 제품 = 내 제품 이름(문자열)
      * 가격 = 120.90(문자열)
      * 크기 = M(문자열)
      * 색상 = 검정(문자열)
      * 색상^코드 = 101(문자열)

**SAINT 헤더 및 레코드:**

| **키** | **제품** | **가격** | **크기** | **색상** | **색상^코드** |
|---|---|---|---|---|---|
| 1 | 내 제품 이름 | 120.90 | M | black | 101 |

속성은 다음과 같습니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성 경로</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>변환기</td>
   <td>SAINTrans전 구현의 클래스 이름</td>
  </tr>
  <tr>
   <td>이메일</td>
   <td>알림 이메일 주소입니다.</td>
  </tr>
  <tr>
   <td>reportsuite</td>
   <td>보고서 세트 ID를 사용하여 가져오기 작업을 실행합니다. </td>
  </tr>
  <tr>
   <td>데이터 집합</td>
   <td>가져오기 작업을 실행할 데이터 집합 관계 ID입니다. </td>
  </tr>
  <tr>
   <td>설명</td>
   <td>작업 설명입니다. <br /> </td>
  </tr>
  <tr>
   <td>덮어쓰기</td>
   <td>데이터 충돌을 덮어쓸 플래그. 기본값은 <strong>false입니다</strong>.</td>
  </tr>
  <tr>
   <td>체크분할</td>
   <td>호환성이 있는지 보고서 세트를 확인하는 플래그. Default is <strong>true</strong>.</td>
  </tr>
  <tr>
   <td>삭제 처리됨</td>
   <td>내보내기 후 처리된 노드를 삭제하는 플래그. 기본값은 <strong>false입니다</strong>.</td>
  </tr>
 </tbody>
</table>

## Adobe 분류 내보내기 자동화 {#automating-adobe-classifications-export}

고유한 워크플로우를 만들면 새 가져오기가 작업 과정을 시작하여 Adobe 분류로 내보낼 수 있도록 적절하게 구조화된 데이터를 **/var/export/에서 올바르게** 만들 수 있습니다.
