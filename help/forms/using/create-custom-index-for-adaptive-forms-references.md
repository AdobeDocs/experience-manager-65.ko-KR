---
title: 적응형 양식 참조를 위한 사용자 지정 인덱스 만들기
description: AEM Forms에서 적응형 양식 참조 쿼리에 대해 태그 지정된 Lucene 인덱스를 만들어 경험 조각을 게시할 때 트래버스 쿼리를 방지하는 방법을 알아봅니다.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, Developer
source-git-commit: 9240de61985dc32f17593f416e5d054cadb8a392
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 1%
---

# 적응형 양식 참조를 위한 사용자 지정 인덱스 만들기 {#create-custom-index-for-adaptive-forms-references}

Adobe Experience Manager(AEM) Forms에서 적응형 양식 참조를 확인할 때 순회 쿼리를 방지하기 위해 태그가 지정된 Lucene 인덱스를 만듭니다. 적절한 인덱스가 없으면 적응형 양식 참조가 포함된 경험 조각을 게시하면 로그에 `Traversal query (query without index)` 경고가 발생할 수 있습니다.

AEM Forms 6.5.24.0 이상에서는 참조 쿼리가 `aemformsAFReferences` 인덱스 태그를 사용합니다. 이러한 릴리스에는 쿼리 변경 사항이 포함되지만 해당 태그로 사용자 지정 색인을 만들어야 합니다. 이 문서에서는 색인을 정의하고 배포하는 방법을 보여 줍니다.

AEM Forms 6.5 LTS의 경우 [AEM Forms 6.5 LTS에서 적응형 양식 참조에 대한 사용자 지정 인덱스 만들기](https://experienceleague.adobe.com/en/docs/experience-manager-65-lts/content/forms/install-aem-forms/configure-aem-forms/create-custom-index-for-adaptive-forms-references)를 참조하십시오.

## 사전 요구 사항 {#prerequisites}

시작하기 전에 다음을 확인합니다.

* 해당 Forms 추가 기능이 설치된 AEM Forms 6.5.24.0 이상
* 작성자 인스턴스의 `/oak:index` 아래에 인덱스를 만들 수 있는 액세스 권한.
* 콘텐츠 패키지를 통해 인덱스를 배포하거나 개발 대안을 위해 CRXDE Lite에 액세스하는 경우 `ui.apps` 모듈이 있는 AEM 프로젝트.

프로덕션 환경에 배포하기 전에 개발 또는 스테이징 환경에서 인덱스를 테스트합니다. [큰 저장소에서 인덱스를 만드는 데 시간이 걸릴 수 있습니다](/help/sites-deploying/queries-and-indexing.md#configuring-the-indexes).

## 사용자 지정 인덱스 정의 {#define-the-custom-index}

`/oak:index/customAFReferenceLuceneIndex-1`에 인덱스를 만듭니다. 다른 인덱스 노드 이름을 선택할 수 있지만 Forms 참조 쿼리에서 인덱스를 선택할 수 있도록 `aemformsAFReferences` 태그를 변경하지 않고 유지합니다.

다음 정의를 사용하십시오. `/content` 아래의 `nt:unstructured` 노드에서 `sling:resourceType`을(를) 인덱싱합니다.

```json
{
  "jcr:primaryType": "oak:QueryIndexDefinition",
  "selectionPolicy": "tag",
  "compatVersion": 2,
  "includedPaths": ["/content"],
  "queryPaths": ["/content"],
  "tags": ["aemformsAFReferences"],
  "type": "lucene",
  "async": ["async"],
  "evaluatePathRestrictions": true,
  "reindex": false,
  "indexRules": {
    "jcr:primaryType": "nt:unstructured",
    "nt:unstructured": {
      "jcr:primaryType": "nt:unstructured",
      "properties": {
        "jcr:primaryType": "nt:unstructured",
        "resourceType": {
          "jcr:primaryType": "nt:unstructured",
          "propertyIndex": true,
          "name": "sling:resourceType"
        }
      }
    }
  }
}
```

`analyzed=true`을(를) 추가하지 마십시오. 참조 쿼리에서 전체 텍스트 `contains` 조건이 아닌 속성 제한을 사용하므로 설정이 필요하지 않습니다.

## 콘텐츠 패키지를 사용하여 인덱스 배포 {#deploy-the-index-with-a-content-package}

프로덕션 배포에 콘텐츠 패키지를 사용합니다.

1. AEM 프로젝트의 `ui.apps` 모듈에서 `ui.apps/src/main/content/jcr_root/_oak_index/customAFReferenceLuceneIndex-1/`을(를) 만듭니다.
1. 다음 정의를 사용하여 해당 디렉터리에 `.content.xml`을(를) 만듭니다.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:oak="http://jackrabbit.apache.org/oak/ns/1.0"
             xmlns:jcr="http://www.jcp.org/jcr/1.0"
             xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
             jcr:primaryType="oak:QueryIndexDefinition"
             async="[async]"
             compatVersion="{Long}2"
             evaluatePathRestrictions="{Boolean}true"
             includedPaths="[/content]"
             queryPaths="[/content]"
             reindex="{Boolean}false"
             selectionPolicy="tag"
             tags="[aemformsAFReferences]"
             type="lucene">
       <indexRules jcr:primaryType="nt:unstructured">
           <nt:unstructured jcr:primaryType="nt:unstructured">
               <properties jcr:primaryType="nt:unstructured">
                   <resourceType jcr:primaryType="nt:unstructured"
                                 name="sling:resourceType"
                                 propertyIndex="{Boolean}true"/>
               </properties>
           </nt:unstructured>
       </indexRules>
   </jcr:root>
   ```

1. `ui.apps/src/main/content/META-INF/vault/filter.xml`의 기존 `workspaceFilter` 요소 내부에 다음 필터를 추가합니다. 프로젝트의 다른 필터를 변경하지 마십시오.

   ```xml
   <filter root="/oak:index/customAFReferenceLuceneIndex-1"/>
   ```

1. 기존 빌드 구성을 사용하여 프로젝트를 빌드하고 결과 콘텐츠 패키지를 작성자 인스턴스에 설치합니다. 패키지 업로드 및 설치 지침은 [패키지 관리자](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system)를 참조하십시오.
1. `/oak:index/customAFReferenceLuceneIndex-1`이(가) 있는지 확인하십시오. 쿼리 계획을 확인하기 전에 비동기 인덱싱을 완료할 수 있도록 허용합니다.

다른 인덱스 이름을 선택한 경우 디렉터리, 필터 및 저장소 경로에서 해당 이름을 일관되게 사용합니다.

## CRXDE Lite으로 색인 만들기 {#create-the-index-with-crxde-lite}

이 대체 요소를 콘텐츠 패키지 메서드 대신 개발 환경에서 사용합니다.

인덱스 노드를 만들 때 다음 속성을 사용하십시오.

| 속성 | 유형 | 값 |
| --- | --- | --- |
| `selectionPolicy` | 문자열 | `tag` |
| `compatVersion` | Long | `2` |
| `includedPaths` | `String[]` | `/content` |
| `queryPaths` | `String[]` | `/content` |
| `tags` | `String[]` | `aemformsAFReferences` |
| `type` | 문자열 | `lucene` |
| `async` | `String[]` | `async` |
| `evaluatePathRestrictions` | 부울 | `true` |
| `reindex` | 부울 | `false` |

`String[]`은(는) 값이 하나만 있는 경우에도 다중 값 String 속성을 의미합니다.

1. `http://localhost:4502/crx/de/index.jsp`를 엽니다. 호스트 및 포트를 작성자 인스턴스의 호스트 및 포트로 바꿉니다.
1. 다음으로 이동 `/oak:index`. 노드를 마우스 오른쪽 단추로 클릭하고 [!UICONTROL 만들기] > [!UICONTROL 노드 만들기]를 선택합니다.
1. 형식이 `oak:QueryIndexDefinition`인 `customAFReferenceLuceneIndex-1`을(를) 만듭니다.
1. 위 표의 속성을 인덱스 노드에 추가합니다.
1. 인덱스 노드 아래에서 다음 하위 노드 계층을 생성합니다. 모든 하위 노드의 유형을 `nt:unstructured`(으)로 설정:

   ```text
   indexRules
       nt:unstructured
           properties
               resourceType
   ```

1. `resourceType`에서 값이 `sling:resourceType`인 `name`(문자열)과 값이 `true`인 `propertyIndex`(부울)을 추가합니다.
1. [!UICONTROL 모두 저장]을 선택하고 비동기 인덱싱을 완료할 수 있도록 허용합니다.

## 쿼리에서 색인을 사용하는지 확인합니다. {#verify-that-the-query-uses-the-index}

쿼리 계획을 확인하여 참조 쿼리가 사용자 지정 색인을 선택하는지 확인합니다.

1. 비동기 인덱싱이 완료되었는지 확인합니다. 인덱스 상태를 검사하려면 [인덱스 관리자](/help/sites-administering/operations-dashboard.md#the-index-manager)를 사용하세요.
1. [!UICONTROL 도구] > [!UICONTROL 작업] > [!UICONTROL 진단] > [!UICONTROL 쿼리 성능]을 열고 [!UICONTROL 쿼리 설명]을 선택합니다. XPath 쿼리 언어를 선택하고 다음을 입력합니다.

   ```text
   /jcr:root/content//element(*, nt:unstructured)[
     (@sling:resourceType = 'fd/af/components/aemform'
     or jcr:like(@sling:resourceType, '%components/aemformscontainer%')
     or jcr:like(@sling:resourceType, '%components/adaptiveForm/fragment%'))]
   option (index tag aemformsAFReferences)
   ```

1. [!UICONTROL 설명]을 선택합니다. 플랜이 순회 플랜이 아닌 쿼리 분기에 대해 `lucene:customAFReferenceLuceneIndex-1` 및 `/oak:index/customAFReferenceLuceneIndex-1` 또는 선택한 인덱스 이름을 사용하는지 확인하십시오. 자세한 내용은 [쿼리 설명](/help/sites-administering/operations-dashboard.md#explain-query)을 참조하세요.
1. 경고를 생성한 경험 조각 게시 작업을 반복합니다. `com.adobe.aem.formsndocuments.publish.AssetReferenceProvider.resolvePathsToFindReferences`의 새 순회 경고를 보려면 `error.log`을(를) 확인하십시오.

계획에서 사용자 지정 인덱스를 선택하지 않으면 위의 예제와 비교하여 태그, `indexRules` 계층 구조 및 `sling:resourceType` 속성 정의를 확인하십시오. 추가 진단은 [Oak 인덱스 문제 해결](/help/sites-deploying/troubleshooting-oak-indexes.md)을 참조하십시오.

## 관련 작업 {#related-tasks}

쿼리 성능 및 인덱스 구성에 대한 자세한 내용은 다음을 참조하십시오.

* [Oak 쿼리 및 색인화](/help/sites-deploying/queries-and-indexing.md)
* [쿼리 및 색인 생성에 대한 우수 사례](/help/sites-deploying/best-practices-for-queries-and-indexing.md)
* [느린 쿼리 문제 해결](/help/sites-developing/troubleshooting-slow-queries.md)
