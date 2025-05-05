---
title: 실행 모드
description: 실행 모드를 사용하여 특정 목적을 위해 AEM 인스턴스를 조정하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Administering
exl-id: 6d03cb1d-500e-4a23-80e5-347a43dff30e
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 1%

---

# 실행 모드{#run-modes}

실행 모드를 사용하면 작성자 또는 게시, 테스트, 개발, 인트라넷 또는 기타 등의 특정 목적을 위해 AEM 인스턴스를 조정할 수 있습니다.

다음과 같은 작업을 수행할 수 있습니다.

* [각 실행 모드에 대한 구성 매개 변수의 컬렉션을 정의](#defining-configuration-properties-for-a-run-mode)합니다.

  기본 구성 매개변수 세트가 모든 실행 모드에 적용됩니다. 그런 다음 특정 환경의 목적에 맞게 추가 세트를 조정할 수 있습니다. 이는 필요에 따라 적용됩니다.

* [특정 모드에 대해 설치할 추가 번들을 정의합니다](#defining-additional-bundles-to-be-installed-for-a-run-mode).

모든 설정 및 정의는 하나의 저장소에 저장되며 **실행 모드**&#x200B;를 설정하여 활성화됩니다.

## 설치 실행 모드 {#installation-run-modes}

설치(또는 고정) 실행 모드는 설치 시 사용된 다음 인스턴스의 전체 수명 동안 고정되며 변경할 수 없습니다.

설치 실행 모드는 즉시 제공됩니다.

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

상호 배타적인 실행 모드의 두 쌍입니다. 예를 들어 다음과 같은 작업을 수행할 수 있습니다.

* `author` 또는 `publish`을(를) 동시에 정의하지 않음

* `author`을(를) `samplecontent` 또는 `nosamplecontent`과(와) 결합(둘 다 아님)

>[!CAUTION]
>
>위의 실행 모드(author, publish, samplecontent, nosamplecontent) 중 하나를 사용할 때 설치 시 사용되는 값은 해당 설치의 *전체 수명*&#x200B;에 대한 실행 모드를 정의합니다.
>
>이러한 실행 모드에 대해 *설치 후에는 변경할 수 없습니다*.

## 사용자 지정된 실행 모드 {#customized-run-modes}

자신만의 맞춤화된 실행 모드를 만들 수도 있습니다. 이를 결합하여 다음과 같은 시나리오를 다룰 수 있습니다.

* `author` + `development`

* `publish` + `test`

* `publish` + `test` + `golive`

* `publish` + `intranet`

* 필요에 따라 . .

각 시작 시 사용자 정의된 실행 모드를 선택할 수도 있습니다.

## samplecontent 및 nosamplecontent 사용 {#using-samplecontent-and-nosamplecontent}

이러한 모드를 사용하여 샘플 콘텐츠의 사용을 제어할 수 있습니다. 샘플 콘텐츠는 빠른 시작을 빌드하기 전에 정의되며 패키지, 구성 등을 포함할 수 있습니다.

* `samplecontent` 실행 모드에서는 이 콘텐츠를 설치합니다(기본 모드).

* `nosamplecontent` 모드에서는 샘플 콘텐츠가 설치되지 않습니다.

nosamplecontent 실행 모드는 프로덕션 설치용으로 설계되었습니다.

## 실행 모드에 대한 구성 속성 정의 {#defining-configuration-properties-for-a-run-mode}

특정 실행 모드에 사용되는 구성 속성에 대한 값 모음을 저장소에 저장할 수 있습니다.

실행 모드는 폴더 이름에 접미사로 표시됩니다. 이렇게 하면 모든 구성을 하나의 저장소에으로 저장할 수 있습니다. 예:

* `config`

  모든 실행 모드에 적용 가능

* `config.author`

  작성자 실행 모드에 사용됩니다.

* `config.publish`

  게시 실행 모드에 사용됨

* `config.<run-mode>`

  적용 가능한 실행 모드에 사용됩니다(예: config).

이러한 폴더 내의 개별 구성 노드를 정의하고 여러 실행 모드 조합에 대한 구성을 만드는 방법에 대한 자세한 내용은 [저장소의 OSGi 구성](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)을 참조하십시오.

>[!NOTE]
>
>[설치 실행 모드](#installation-run-modes)(예: 작성자)의 경우 설치 후에는 실행 모드를 변경할 수 없습니다. 그러나 개별 구성 속성에 대한 변경 사항은 다시 시작할 때 적용됩니다.

## 실행 모드에 대해 설치할 추가 번들 정의 {#defining-additional-bundles-to-be-installed-for-a-run-mode}

특정 실행 모드에 대해 설치해야 하는 추가 번들을 지정할 수도 있습니다. 이러한 정의에서는 설치 폴더를 사용하여 번들을 고정합니다. 다시 실행 모드는 접두사로 표시됩니다.

* `install.author`
* `install.publish`

이 폴더는 `nt:folder` 형식이며 적절한 번들을 포함해야 합니다.

## 특정 실행 모드로 CQ 시작 {#starting-cq-with-a-specific-run-mode}

여러 실행 모드에 대한 구성을 정의한 경우 시작 시 사용할 구성을 정의해야 합니다. 사용할 실행 모드를 지정하는 방법에는 몇 가지가 있습니다. 해결 순서는 다음과 같습니다.

1. [시스템 속성(](#using-a-system-property-in-the-start-script)
1. [&#128279;](#using-the-sling-properties-file)
1. [&#128279;](#using-the-r-option)
1. [파일 이름 감지](#filename-detection-renaming-the-jar-file)

응용 프로그램 서버를 사용하는 경우 [web.xml에서 실행 모드를 정의](#defining-the-run-mode-in-web-xml-with-application-server)할 수도 있습니다.

### sling.properties 파일 사용 {#using-the-sling-properties-file}

`sling.properties` 파일을 사용하여 필요한 실행 모드를 정의할 수 있습니다.

1. 구성 파일을 편집합니다.

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. 다음 속성을 추가합니다. 다음 예제는 작성자를 위한 것입니다.

   `sling.run.modes=author`

### -r 옵션 사용 {#using-the-r-option}

빠른 시작을 시작할 때 `-r` 옵션을 사용하여 사용자 지정 실행 모드를 활성화할 수 있습니다. 예를 들어 다음 명령을 사용하여 실행 모드가 dev로 설정된 AEM 인스턴스를 시작합니다. &quot;

```shell
java -jar cq-56-p4545.jar -r dev
```

### 시작 스크립트에서 시스템 속성 사용 {#using-a-system-property-in-the-start-script}

시작 스크립트의 시스템 속성을 사용하여 실행 모드를 지정할 수 있습니다.

* 예를 들어, 다음을 사용하여 인스턴스를 미국에서 프로덕션 게시 인스턴스로 시작합니다.

  `-Dsling.run.modes=publish,prod,us`

### 파일 이름 감지 - jar 파일 이름 바꾸기 {#filename-detection-renaming-the-jar-file}

설치하기 전에 설치 jar 파일의 이름을 바꾸어 다음 두 가지 설치 실행 모드를 활성화할 수 있습니다.

* 게시
* 작성자

jar 파일은 명명 규칙을 사용해야 합니다.

`cq5-<run-mode>-p<port-number>`

예를 들어 jar 파일의 이름을 지정하여 `publish` 실행 모드를 설정합니다.

`cq5-publish-p4503`

### web.xml에서 실행 모드 정의(Application Server 사용) {#defining-the-run-mode-in-web-xml-with-application-server}

응용 프로그램 서버를 사용하는 경우 속성을 구성할 수도 있습니다.

`sling.run.modes`

파일에서 다음을 수행합니다.

`WEB-INF/web.xml`

이 파일은 AEM `war` 파일에 있으며 배포 전에 업데이트해야 합니다.

자세한 내용은 [응용 프로그램 서버에 AEM 설치](/help/sites-deploying/application-server-install.md)를 참조하십시오.
