---
title: 백업용 AEM Forms 준비
seo-title: 백업용 AEM Forms 준비
description: 백업 및 복원 서비스를 사용하여 Java API 및 웹 서비스 API를 사용하여 AEM Forms 서버의 백업 모드를 시작하고 나가는 방법을 알아봅니다.
seo-description: 백업 및 복원 서비스를 사용하여 Java API 및 웹 서비스 API를 사용하여 AEM Forms 서버의 백업 모드를 시작하고 나가는 방법을 알아봅니다.
uuid: b8ef2bed-62e2-4000-b55a-30d2fc398a5f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e747147e-e96d-43c7-87b3-55947eef81f5
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '2540'
ht-degree: 0%

---


# AEM Forms 백업 준비 중 {#preparing-aem-forms-for-backup}

## 백업 및 복원 서비스 {#about-the-backup-and-restore-service} 정보

백업 및 복원 서비스를 사용하면 AEM Forms을 *백업 모드*&#x200B;에 삽입하여 핫 백업을 수행할 수 있습니다. 백업 및 복원 서비스는 AEM Forms의 백업을 실제로 수행하거나 시스템을 복원하지 않습니다. 대신 서버를 계속 실행할 수 있도록 하면서 서버가 일관되고 안정적인 백업을 위해 상태로 됩니다. GDS(Global Document Storage) 및 양식 서버에 연결된 데이터베이스를 백업하는 작업은 사용자가 책임집니다. GDS는 오래 지속되는 프로세스 내에서 사용되는 파일을 저장하는 데 사용되는 디렉토리입니다.

백업 모드는 백업 절차가 진행되는 동안 GDS 파일이 삭제되지 않도록 서버가 입력하는 상태입니다. 대신 백업 모드가 끝난 후에 삭제할 파일의 레코드를 유지하기 위해 GDS 디렉토리 아래에 하위 디렉토리가 만들어집니다. 파일은 시스템이 다시 시작될 때까지 유지되도록 만들어진 파일로 여러 일 또는 여러 해에 걸쳐 사용될 수 있습니다. 이러한 파일은 양식 서버의 전체 상태 중 중요한 부분이며 PDF 파일, 정책 또는 양식 템플릿을 포함할 수 있습니다. 이러한 파일 중 하나가 손실되거나 손상된 경우 양식 서버의 프로세스가 불안정해지거나 데이터가 손실될 수 있습니다.

스냅샷 백업을 수행하도록 선택할 수 있습니다. 이 경우 보통 일정 기간 동안 백업 모드를 시작한 다음 백업 작업을 완료한 후 백업 모드를 종료할 수 있습니다. 백업 모드를 종료해야 GDS에서 파일을 제거하여 불필요하게 큰 파일이 발생하지 않도록 할 수 있습니다. 백업 모드를 명시적으로 종료하거나 백업 모드 세션에서 시간이 만료될 때까지 기다릴 수 있습니다.

또한 서버를 영구 백업 모드로 둘 수도 있습니다. 이는 롤링 백업 또는 지속적인 시스템 적용 범위에 대한 백업 전략에 일반적으로 사용됩니다. 순환 백업 모드는 이전 세션이 릴리스되는 즉시 새 백업 모드 세션이 시작되어 시스템이 항상 백업 모드임을 나타냅니다. 연속 백업 모드에서는 파일이 2개의 백업 모드 세션 후에 제거되고 더 이상 참조되지 않습니다.

백업 및 복원 서비스를 사용하여 기존 응용 프로그램 또는 양식 서버에 연결된 GDS 또는 데이터베이스의 백업을 수행하기 위해 만드는 새 응용 프로그램에 추가할 수 있습니다.

>[!NOTE]
>
>AEM Forms 구현의 다른 측면과 마찬가지로, 백업 및 복구 전략을 개발 또는 스테이징 환경에서 개발 및 테스트하여 운영 환경에서 전체 솔루션이 데이터 손실 없이 예상대로 작동되도록 해야 합니다.

백업 및 복원 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* 백업 모드를 시작합니다.
* 백업 모드를 종료합니다.

>[!NOTE]
>
>AEM Forms에 대한 백업을 수행할 때 고려해야 할 사항에 대한 자세한 내용은 [관리 도움말](https://www.adobe.com/go/learn_aemforms_admin_63)을 참조하십시오.

>[!NOTE]
>
>백업 및 복원 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## 양식 서버 {#entering-backup-mode-on-the-forms-server}에 백업 모드 시작

양식 서버의 핫 백업을 허용하려면 백업 모드를 시작합니다. 백업 모드를 시작할 때 조직의 백업 절차에 따라 다음 정보를 지정합니다.

* 백업 프로세스에 유용할 수 있는 백업 모드 세션을 식별하는 고유한 레이블입니다.
* 백업 절차를 완료하는 시간입니다.
* 연속 백업 모드인지 여부를 나타내는 플래그입니다. 이는 롤링 백업을 수행하는 경우에만 유용합니다.

응용 프로그램을 작성하여 백업 모드로 전환하기 전에 양식 서버를 백업 모드로 설정한 후 사용할 백업 절차를 이해하는 것이 좋습니다. AEM Forms에 대한 백업을 수행할 때 고려해야 할 사항에 대한 자세한 내용은 [관리 도움말](https://www.adobe.com/go/learn_aemforms_admin_63)을 참조하십시오.

>[!NOTE]
>
>백업 및 복원 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary-of-steps} 단계 요약

백업 모드를 시작하는 응용 프로그램을 만들려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. BackupService 클라이언트 개체를 만듭니다.
1. 고유 레이블, 백업 수행 시간 및 연속 백업 모드인지 여부를 결정합니다.
1. 백업 모드를 시작합니다.
1. (선택 사항) 서버에서 백업 모드 세션에 대한 정보를 검색합니다.
1. GDS(Global Data Store) 및 데이터베이스의 백업을 수행합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. 이러한 파일은 코드를 제대로 컴파일하고 백업 및 복원 서비스 API를 사용하기 위해 프로젝트에 포함되어야 합니다.

이러한 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

**BackupService 클라이언트 API 개체 만들기**

백업 모드를 프로그래밍 방식으로 종료하려면 백업 및 복원 서비스 API를 사용할 BackupService 클라이언트 개체를 만듭니다.

**고유 레이블을 결정하고 백업 수행 시간을 결정하고 백업 모드를 계속 유지할지 여부를 결정합니다.**

백업 모드를 시작하기 전에 고유한 레이블을 결정하고 백업을 수행하기 위해 할당할 시간을 결정하고 양식 서버가 백업 모드를 유지할지 여부를 결정해야 합니다. 이러한 고려 사항은 조직에서 설정한 백업 절차와 통합하는 데 중요합니다. ([관리 도움말](https://www.adobe.com/go/learn_aemforms_admin_63)을 참조하십시오.)

**백업 모드 시작**

조직의 백업 절차와 일치하는 매개 변수를 사용하여 백업 모드를 시작합니다.

**서버의 백업 모드 세션에 대한 정보 검색**

백업 모드를 시작한 후 세션에 대한 정보를 검색할 수 있습니다. 이 정보는 백업 절차와 통합하는 데 사용할 수 있습니다.

**GDS 및 데이터베이스의 백업 수행**

백업 모드를 성공적으로 시작한 후 GDS(Global Document Storage) 및 양식 서버가 연결된 데이터베이스의 백업을 수행할 수 있습니다. 이 단계는 이 단계를 수동으로 수행하거나 다른 도구를 실행하여 백업 절차를 수행할 수 있으므로 조직에만 적용됩니다.

### Java API {#enter-backup-mode-using-the-java-api}을 사용하여 백업 모드를 시작합니다.

백업 및 복원 서비스 API를 사용하여 백업 모드를 시작합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-backup-restore-client-sdk.jar 같은 필요한 클라이언트 JAR 파일을 포함합니다. Java 클라이언트 응용 프로그램을 만들려면 프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (AEM Forms이 JBoss Application Server에 배포된 경우 필수)
   * jbossall-client.jar (AEM Forms이 JBoss Application Server에 배포된 경우 필수)

1. BackupService 클라이언트 API 개체 만들기

   `ServiceClientFactory` 개체와 BackupService 클라이언트 API 개체를 함께 사용합니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다. ([연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하십시오.)
   * 생성자를 사용하여 `BackupService` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. 고유 레이블을 결정하고 백업 수행 시간을 결정하고 백업 모드를 계속 유지할지 여부를 결정합니다.

   고유한 레이블을 선택하고 백업을 수행하기 위해 할당할 시간을 결정하고 양식 서버가 연속 백업 모드를 유지할지 여부를 결정합니다.

1. 백업 모드 시작

   다음 매개 변수를 사용하여 `enterBackupMode` 메서드를 호출하여 백업 모드를 시작합니다.

   * 백업 모드 세션을 식별하는 사람이 읽을 수 있는 고유한 레이블을 지정하는 `String` 값. XML 형식으로 인코딩할 수 없는 공백이나 문자는 사용하지 않는 것이 좋습니다.
   * 백업 모드에서 유지할 시간(분)을 지정하는 `int` 값입니다. `1`에서 `10080`(1주의 분) 사이의 값을 지정할 수 있습니다. 이 값은 연속 백업 모드를 사용할 때 무시됩니다.
   * 연속 백업 모드인지 여부를 지정하는 `Boolean` 값입니다. `True` 값은 연속 백업 모드로 지정합니다. 연속 백업 모드에서는 백업 모드를 유지할 시간(분)에 대해 지정한 값이 무시됩니다.

      연속 백업 모드는 현재 백업 모드 세션이 완료된 후 새 백업 모드 세션을 시작하는 것을 의미합니다. `False` 값은 연속 백업 모드를 사용하지 않고 백업 모드를 종료하면 GDS에서 파일 제거가 다시 시작되는 것을 의미합니다.

1. 서버의 백업 모드 세션에 대한 정보 검색

   `enterBackupMode` 메서드를 호출한 후 반환되는 `BackupModeEntryResult` 개체를 사용하여 정보를 검색합니다. 백업 모드를 시작한 후 검색할 수 있는 정보는 백업 절차와 통합하는 데 유용합니다. 예를 들어 레이블, 백업 ID 및 시작 시간은 백업 절차의 파일 이름을 입력하는 데 유용합니다.

1. GDS 및 데이터베이스의 백업 수행

   GDS(Global Document Storage) 및 양식 서버가 연결된 데이터베이스를 백업합니다. 백업을 수행하는 작업은 AEM Forms SDK의 일부가 아니며 조직에서 백업 절차에 대한 수동 단계를 포함할 수도 있습니다.

### 웹 서비스 API {#enter-backup-mode-using-the-web-service-api}를 사용하여 백업 모드를 시작합니다.

백업 및 복원 서비스 API에서 제공하는 웹 서비스를 사용하여 백업 모드를 시작합니다.

1. 프로젝트 파일 포함

   * 백업 및 복원 서비스 API WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조하십시오.

1. BackupService 클라이언트 API 개체 만들기

   Microsoft .NET 클라이언트 어셈블리를 사용하여 기본 생성자를 호출하여 `BackupServiceService` 개체를 만들고 `Credentials` 메서드를 사용하여 자격 증명을 지정합니다.

1. 고유 레이블을 결정하고 백업 수행 시간을 결정하고 백업 모드를 계속 유지할지 여부를 결정합니다.

   고유한 레이블을 선택하고 백업을 수행하기 위해 할당할 시간을 결정하고 양식 서버가 연속 백업 모드를 유지할지 여부를 결정합니다.

1. 백업 모드 시작

   백업 모드를 시작하려면 enterBackupMode 메서드를 호출하고 다음 값을 전달합니다.

   * 백업 모드 세션을 식별하는 사람이 읽을 수 있는 고유한 레이블을 지정하는 `String` 값. XML 형식으로 인코딩할 수 없는 공백이나 문자는 사용하지 않는 것이 좋습니다.
   * 백업 모드에서 유지할 시간(분)을 지정하는 `Uint32` 값. `1`에서 `10080`(1주의 분 수)까지의 값을 지정할 수 있습니다. 이 값은 연속 백업 모드를 사용할 때 무시됩니다.
   * 연속 백업 모드인지 여부를 지정하는 `Boolean` 값입니다. `True` 값은 연속 백업 모드로 지정합니다. 연속 백업 모드에서는 백업 모드를 유지할 시간(분)에 대해 지정한 값이 무시됩니다. 연속 백업 모드는 현재 백업 모드 세션이 완료된 후 새 백업 모드 세션을 시작하는 것을 의미합니다.

      `False` 값은 연속 백업 모드를 사용하지 않고 백업 모드를 종료하면 GDS에서 파일 제거가 다시 시작되는 것을 의미합니다.

1. 서버의 백업 모드 세션에 대한 정보 검색

   성공 여부를 확인하기 위해 반환된 BackupModeEntryResult에서 enterBackupMode 메서드를 호출한 후 백업 모드 세션에 대한 정보를 검색합니다. 백업 모드를 시작한 후 검색할 수 있는 정보는 백업 절차와 통합하는 데 유용합니다. 예를 들어 레이블, 백업 ID 및 시작 시간은 백업 절차의 파일 이름을 입력하는 데 유용합니다.

1. GDS 및 데이터베이스의 백업 수행

   GDS(Global Document Storage) 및 양식 서버가 연결된 데이터베이스를 백업합니다. 백업을 수행하는 작업은 AEM Forms SDK의 일부가 아니며 조직에서 백업 절차에 대한 수동 단계를 포함할 수도 있습니다.

## 양식 서버 {#leaving-backup-mode-on-the-forms-server}에서 백업 모드 종료

양식 서버가 양식 서버의 GDS(Global Document Storage)에서 파일 제거를 다시 시작할 수 있도록 백업 모드를 종료합니다.

애플리케이션을 작성하여 종료 모드로 전환하기 전에 AEM Forms과 함께 사용되는 백업 절차를 이해하는 것이 좋습니다. AEM Forms에 대한 백업을 수행할 때 고려해야 할 사항에 대한 자세한 내용은 [관리 도움말](https://www.adobe.com/go/learn_aemforms_admin_63)을 참조하십시오.

>[!NOTE]
>
>백업 및 복원 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary_of_steps-1} 단계 요약

백업 모드를 종료하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. BackupService 클라이언트 개체를 만듭니다.
1. 백업 모드를 종료합니다.
1. (선택 사항) 양식 서버에서 실행 중인 백업 모드 세션에 대한 정보를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 모든 파일을 포함합니다. 이러한 파일은 코드를 제대로 컴파일하고 백업 및 복원 서비스 API를 사용하는 데 중요합니다.

이러한 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)을 참조하십시오.

**BackupService 클라이언트 API 개체 만들기**

백업 모드를 프로그래밍 방식으로 종료하려면 백업 및 복원 서비스 API를 사용할 BackupService 클라이언트 개체를 만듭니다.

**백업 모드 종료**

GDS(Global Document Storage)에서 일반적인 파일 제거를 다시 시작하려면 백업 모드를 종료하십시오. 백업 모드를 종료하기 전에 백업 절차가 완료되었는지 확인해야 합니다.

**종료한 백업 모드 세션에 대한 정보 검색**

백업 모드를 종료하면 세션에 대한 정보를 검색할 수 있습니다. 이 정보는 백업 절차와 통합하는 데 사용할 수 있습니다.

### Java API {#leave-backup-mode-using-the-java-api}를 사용하여 백업 모드를 종료합니다.

백업 및 복원 서비스 API(Java)를 사용하여 백업 모드를 종료합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-backup-restore-client-sdk.jar 같은 필요한 클라이언트 JAR 파일을 포함합니다. Java 클라이언트 응용 프로그램을 만들려면 프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (AEM Forms이 JBoss Application Server에 배포된 경우 필수)
   * jbossall-client.jar (AEM Forms이 JBoss Application Server에 배포된 경우 필수)

1. BackupService 클라이언트 API 개체 만들기

   `ServiceClientFactory` 개체와 BackupService 클라이언트 API 개체를 함께 사용합니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다. ([연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하십시오.)
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 매개 변수로 전달하여 `BackupService` 개체를 만듭니다.

1. 백업 모드 시작

   `leaveBackupMode` 메서드를 호출하여 백업 모드를 종료합니다.

1. 서버의 백업 모드 세션에 대한 정보 검색

   반환되는 `BackupModeResult` 개체를 사용하여 작업에 대한 정보를 검색합니다. 백업 모드를 시작한 후 검색할 수 있는 정보는 백업 절차와 통합하는 데 유용합니다. 예를 들어 레이블, 백업 ID 및 시작 시간은 백업 절차의 파일 이름을 입력하는 데 유용합니다.

### 웹 서비스 API {#leave-backup-mode-using-the-web-service-api}을(를) 사용하여 백업 모드를 종료합니다.

백업 및 복원 서비스 API(웹 서비스)를 사용하여 백업 모드를 종료합니다.

1. 프로젝트 파일 포함

   웹 서비스를 사용하려면 프록시 파일을 포함해야 합니다. 백업 및 복원 서비스 API를 웹 서비스로 사용하도록 프로젝트를 구성하려면 다음 단계를 따르십시오.

   * 백업 및 복원 서비스 API WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조하십시오.

1. BackupService 클라이언트 API 개체 만들기

   Microsoft .NET 클라이언트 어셈블리를 사용하여 기본 생성자를 호출하여 `BackupServiceService` 객체를 만듭니다.

1. 백업 모드 시작

   `leaveBackupMode` 웹 서비스 작업을 호출하여 백업 모드를 종료합니다.

1. 서버의 백업 모드 세션에 대한 정보 검색

   작업 후 백업 모드 식별자를 검색하여 성공했는지 확인합니다. 백업 모드를 종료한 후 검색할 수 있는 정보는 백업 절차와 통합하는 데 유용합니다.

