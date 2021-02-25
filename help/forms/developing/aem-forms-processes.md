---
title: AEM Forms 프로세스 이해
seo-title: AEM Forms 프로세스 이해
description: AEM Forms 프로세스 이해
uuid: 7cbebe7d-f222-42fa-8eb6-d2443458a791
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools, coding
discoiquuid: ac9fe461-63e7-442b-bd1c-eb9576ef55aa
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---


# AEM Forms 프로세스 이해 {#understanding-aem-forms-processes}

**이 문서의 샘플과 예는 JEE 환경의 AEM Forms에만 해당됩니다.**

AEM Forms 서비스 세트가 하나의 문서에서 작동하는 일반적인 용도는 다음과 같습니다. 워크벤치를 사용하여 프로세스를 생성하여 서비스 컨테이너로 요청을 전송할 수 있습니다. 프로세스는 자동화할 비즈니스 프로세스를 나타냅니다. 프로세스 만들기에 대한 자세한 내용은 [Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63) 사용을 참조하십시오.

프로세스가 활성화되면 서비스가 되고 다른 서비스처럼 호출할 수 있습니다. 암호화 서비스와 같은 표준 서비스와 프로세스에서 시작된 서비스 간의 한 가지 차이점은 암호화 서비스에는 여러 작업을 수행하는 하나의 작업이 있다는 것입니다. 반면 표준 서비스에는 여러 가지 작업이 있다. 각 작업은 일반적으로 문서에 정책을 적용하거나 문서를 암호화하는 등 하나의 작업을 수행합니다.

프로세스는 짧거나 오래 사용할 수 있습니다. 단기 프로세스는 해당 프로세스가 호출된 것과 동일한 실행 스레드에서 동기적으로 수행되는 작업입니다. 짧은 사용 작업은 클라이언트 응용 프로그램이 메서드를 호출하고 반환 값을 기다리는 대부분의 프로그래밍 언어에서 발견되는 표준 동작과 비교할 수 있습니다.

그러나 다음과 같은 요인으로 인해 프로세스를 동기식으로 완료할 수 없는 경우가 있습니다.

* 프로세스는 상당한 시간 동안 진행될 수 있습니다.
* 프로세스는 조직의 경계를 확장할 수 있습니다.
* 프로세스를 완료하려면 외부 입력이 필요합니다. 예를 들어 사무실 밖에 있는 관리자에게 양식이 전송되는 상황을 가정해 보십시오. 이 경우 관리자가 양식을 반환하고 채울 때까지 프로세스가 완료되지 않습니다.

   이러한 유형의 프로세스를 오래 지속되는 과정이라고 합니다. 긴 기간의 프로세스는 비동기적으로 수행되므로 시스템에서 리소스를 허용하는 방식으로 인터랙션하고 작업을 추적 및 모니터링할 수 있습니다. 긴 수명 프로세스가 호출되면 AEM Forms은 장기 체류 프로세스 상태를 추적하는 레코드의 일부로서 호출 식별자 값을 만듭니다. 레코드는 AEM Forms 데이터베이스에 저장됩니다. 더 이상 필요하지 않은 긴 프로세스 레코드를 삭제할 수 있습니다.

>[!NOTE]
>
>AEM Forms은 단기 프로세스를 호출할 때 레코드를 만들지 않습니다.

호출 식별자 값을 사용하여 긴 기간의 프로세스 상태를 추적할 수 있습니다. 예를 들어 프로세스 호출 식별자 값을 사용하여 실행 중인 프로세스 인스턴스 종료와 같은 프로세스 관리자 작업을 수행할 수 있습니다.

**단기 체류 프로세스 예**

다음 그림은 *MyApplication/EncryptDocument*&#x200B;라는 짧은 기간의 프로세스의 예입니다.

>[!NOTE]
>
>이 프로세스는 기존 AEM Forms 프로세스를 기반으로 하지 않습니다. 이 프로세스를 호출하는 방법에 대해 설명하는 코드 예제와 함께 따라 Workbench를 사용하여 `MyApplication/EncryptDocument` 프로세스를 만드십시오. ([Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63) 사용 참조)

이 단기 프로세스가 호출되면 다음 작업을 수행합니다.

1. 프로세스로 전달된 보안되지 않은 PDF 문서를 입력 값으로 가져옵니다.
1. 암호로 PDF 문서를 암호화합니다. 이 프로세스에 대한 입력 매개 변수의 이름은 `inDoc`이고 데이터 유형은 문서입니다.
1. 암호로 암호화된 PDF 문서를 로컬 파일 시스템에 PDF 파일로 저장합니다. 이 프로세스에서는 암호화된 PDF 문서를 출력 값으로 반환합니다. 이 프로세스에 대한 출력 매개 변수의 이름은 `outDoc`이고 데이터 유형은 문서입니다.

   이 프로세스는 호출된 동일한 실행 스레드에서 동기적으로 완료됩니다. 이 짧은 기간의 프로세스 이름은 `MyApplication/EncryptDocument`이고 작업은 `invoke`입니다.

   >[!NOTE]
   >
   >일반적으로 수명이 짧은 프로세스는 3개 이상의 작업으로 구성됩니다. 워크벤치를 사용하여 프로세스를 생성합니다. ([Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63) 사용 참조)

   *AEM 형식으로 프로그래밍*&#x200B;은 이 짧은 프로세스를 프로그래밍 방식으로 호출할 수 있는 다음 방법에 대해 설명합니다.

   * [AEM Forms Remoting을 사용하여 안전하지 않은 문서를 전달하여](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)  짧은 기간 프로세스 호출(Flex 응용 프로그램 사용)
   * [호출 API](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api) (Java 호출 API)를 사용하여 짧은 기간 프로세스 호출
   * [Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding) (웹 서비스 예)
   * [MTOM을 사용하여 AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)  호출(웹 서비스 예제)
   * [SwaRef를 사용하여 AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)  호출(웹 서비스 예제)
   * [HTTP를 통해 BLOB 데이터를 사용하여 AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http)  호출(웹 서비스 예)
   * [DIME](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) (웹 서비스 예)를 사용하여 AEM Forms 호출
   * [REST를 사용하여 MyApplication/EncryptDocument 프로세스 호출](/help/forms/developing/invoking-aem-forms-using-rest.md)

**장기간 프로세스 예**

다음 그림은 오랜 기간의 프로세스를 보여주는 예입니다.

이 프로세스는 신청인이 대출 양식을 제출할 때 호출됩니다. 대출 담당자가 대출 요청을 승인하거나 거부하기 전에는 이 과정이 완료되지 않습니다. 이 긴 기간의 프로세스 이름은 *FirstAppSolution/PreRoanProcess*&#x200B;이며 해당 작업은 `invoke_Async`입니다. 이 프로세스는 비동기적으로 호출되어야 합니다. 이 오래 지속되는 프로세스를 프로그래밍 방식으로 호출하는 방법에 대한 자세한 내용은 [인간 중심의 긴 수명 프로세스 호출](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)을 참조하십시오.

>[!NOTE]
>
>이 프로세스는 [첫 번째 AEM Forms 응용 프로그램 만들기](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)에 지정된 자습서를 따라 만들 수 있습니다.