---
title: WebDAV 액세스
description: WebDAV를 사용하여 Adobe Experience Manager에 액세스하는 방법에 대해 알아봅니다.
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
exl-id: 891ee66c-e49c-4561-8fef-e6e448a8aa1c
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 1%

---

# WebDAV 액세스{#webdav-access}

KDE로 WebDAV를 통해 AEM에 연결하려면:

AEM에서는 저장소 컨텐츠를 표시하고 편집할 수 있는 WebDAV 지원을 제공합니다. WebDAV를 통해 연결하면 데스크톱을 통해 콘텐츠 저장소에 직접 액세스할 수 있습니다. WebDAV 연결을 통해 저장소에 추가된 텍스트 및 PDF 파일은 자동으로 전체 텍스트 인덱싱되며 표준 검색 인터페이스와 표준 Java™ API를 통해 검색할 수 있습니다.

## 일반 {#general}

[운영 체제별 세부 지침](/help/sites-administering/webdav-access.md#connecting-via-webdav) 는 이 문서에 포함되어 있지만 기본적으로 WebDAV 프로토콜을 사용하여 저장소에 연결하려면 WebDAV 클라이언트를 다음 위치로 지정합니다.

```xml
http://localhost:4502
```

![chlimage_1-111](assets/chlimage_1-111a.png)

이 URL은 운영 체제 수준에서 연결된 경우 기본 작업 영역( )에 대한 WebDAV 액세스를 제공합니다. `crx.default`). 사용자는 보다 간단하지만 추가 기능을 사용하여 작업 공간 이름을 지정할 수 있는 유연성을 추가로 제공하지 않습니다 [WebDAV URL](/help/sites-administering/webdav-access.md#webdav-urls).

AEM은 다음과 같이 저장소 컨텐츠를 표시합니다.

* 유형의 노드 `nt:folder` 은 폴더로 표시됩니다. 노드 아래 `nt:folder` 노드는 폴더 콘텐츠로 표시됩니다.

* 유형의 노드 `nt:file` 는 파일로 표시됩니다. 노드 아래 `nt:file` 노드는 표시되지 않지만 파일의 내용을 형성합니다.

WebDAV를 사용하여 폴더 및 파일을 만들고 편집할 때 AEM은 필요한 항목을 만들고 편집합니다 `nt:folder` 및 `nt:file` 노드. WebDAV를 사용하여 콘텐츠를 가져오고 내보내려면 `nt:file` 및 `nt:folder` 가능한 한 노드 유형을 입력합니다.

>[!NOTE]
>
>WebDAV를 설정하기 전에 [기술 요구 사항](/help/sites-deploying/technical-requirements.md#webdav-clients).

## WebDAV URL {#webdav-urls}

WebDAV 서버의 URL은 다음과 같은 구조로 되어 있습니다.

<table>
 <colgroup>
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
 </colgroup>
 <tbody>
  <tr>
   <td>
    <code>
     <strong>URL Component</strong>
    </code></td>
   <td><code>https://&lt;host&gt;:&lt;port&gt;</code></td>
   <td><code>/&lt;crx-webapp-path&gt;</code></td>
   <td><code>/repository</code></td>
   <td><code>/&lt;workspace&gt;</code></td>
  </tr>
  <tr>
   <td>
    <code>
     <strong>Example</strong>
    </code></td>
   <td><code>http://localhost:4502</code></td>
   <td><code>/crx</code></td>
   <td><code>/repository</code></td>
   <td><code>/crx.default</code></td>
  </tr>
  <tr>
   <td><strong>설명</strong></td>
   <td>AEM이 실행되는 호스트 및 포트</td>
   <td>AEM 저장소 웹 앱 경로</td>
   <td>WebDAV 서블릿이 매핑된 경로</td>
   <td>작업 공간 이름</td>
  </tr>
 </tbody>
</table>

경로의 작업 영역 요소를 변경하여 ( 기본값 이외의 작업 영역을 매핑할 수 있습니다. `crx.default`). 예를 들어, 작업 공간을 `staging`, 다음 URL 사용:

```xml
http://localhost:4502/crx/repository/staging
```

## WebDAV를 통해 연결 {#connecting-via-webdav}

[위에서 언급한 바와 같이](/help/sites-administering/webdav-access.md#general)WebDAV 프로토콜을 사용하여 저장소에 연결하려면 WebDAV 클라이언트를 저장소 위치에 지정합니다. 그러나 OS에 따라 클라이언트 연결과 관련된 단계가 다르며 OS를 구성해야 할 수도 있습니다.

다음 운영 체제를 연결하는 방법에 대한 지침이 제공됩니다.

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

Microsoft® Windows 7(이상) 시스템을 SSL로 보호되지 않은 AEM 인스턴스에 성공적으로 연결하려면 비보안 네트워크를 통해 기본 인증을 설정하는 옵션을 Windows에서 명시적으로 활성화해야 합니다. 이 기능을 사용하려면 WebClient의 Windows 레지스트리를 변경해야 합니다.

레지스트리가 업데이트되면 AEM 인스턴스를 드라이브로 매핑할 수 있습니다.

#### Windows 7 이상 구성 {#windows-and-greater-configuration}

보안되지 않은 네트워크를 통해 기본 인증을 허용하도록 레지스트리를 업데이트하려면 다음을 수행하십시오.

1. 다음 레지스트리 하위 키를 찾습니다.

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. 설정 `BasicAuthLevel` 다음 값에 대한 레지스트리 항목 하위 키 `2` 또는 그 이상

   이 키가 없으면 하위 키를 추가합니다.

1. 레지스트리 변경 내용을 적용하려면 시스템을 다시 시작하십시오.

>[!NOTE]
>
>Adobe은 저장소 사용자와 동일한 자격 증명을 사용하여 Windows 사용자를 만들 것을 권장합니다. 그렇지 않으면 권한 충돌이 발생할 수 있습니다.

#### Windows 8 구성 {#windows-configuration}

Windows 8의 경우 레지스트리 항목을 변경합니다. [Windows 7 이상에 대해 설명된 대로](/help/sites-administering/webdav-access.md#windows-and-greater-configuration). 그러나 이 작업을 수행하기 전에 레지스트리 항목을 보려면 데스크톱 환경을 활성화해야 합니다.

데스크탑 경험을 사용하려면 을 엽니다. **서버 관리자**, 그런 다음 **기능**, 그런 다음 **기능 추가**, 그런 다음 **데스크탑 경험**.

재부팅하면 Windows 7 이상에 대해 설명된 레지스트리 항목을 사용할 수 있습니다. Windows 7 이상에 설명된 대로 수정합니다.

#### Windows에서 연결 {#connecting-in-windows}

Windows 환경에서 WebDAV를 통해 AEM에 연결하려면 다음을 수행하십시오.

1. 열기 **Windows 탐색기** 또는 **파일 탐색기** 및 클릭 **컴퓨터** 또는 **이 PC**.

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. 마법사를 시작하려면 다음을 클릭하십시오. **네트워크 드라이브 매핑**.
1. 매핑 세부 정보를 입력합니다.

   * **드라이브**: 사용 가능한 편지 선택
   * **폴더**: `http://localhost:4502`
   * 확인 **다른 자격 증명을 사용하여 연결**

   마침을 클릭합니다.

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >AEM이 다른 포트에 있는 경우 4502 대신 해당 포트 번호를 사용하십시오. 또한 로컬 시스템에서 컨텐츠 저장소를 실행하지 않는 경우 `localhost` (각 서버 이름 또는 IP 주소 포함)

1. 사용자 이름 입력 `admin` 및 암호 `admin`. Adobe은 테스트를 위해 사전 구성된 관리자 계정을 사용할 것을 권장합니다.

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. 마법사가 닫히고 새로 매핑된 드라이브가 Windows 탐색기 또는 파일 탐색기 창에서 열립니다.

   ![chlimage_1-115](assets/chlimage_1-115a.png)

이제 Windows에서 WebDAV를 통해 AEM을 드라이브로 매핑했으며 다른 드라이브로 사용할 수 있습니다.

### macOS {#macos}

macOS에서 WebDAV를 통해 연결하는 데 필요한 구성 단계는 없습니다. WebDAV 서버에 연결할 수 있습니다.

1. 다음 중 하나로 이동 **파인더** 창에서 클릭 **이동** 및 **서버에 연결**, 또는 누르기 **Command+k**.
1. 다음에서 **서버에 연결** 창에서 AEM 위치를 입력합니다.

   * `http://localhost:4502`

   >[!NOTE]
   >
   >AEM이 다른 포트에 있는 경우 4502 대신 해당 포트 번호를 사용하십시오. 또한 로컬 시스템에서 컨텐츠 저장소를 실행하지 않는 경우 `localhost` (각 서버 이름 또는 IP 주소 포함)

1. 인증을 묻는 메시지가 표시되면 사용자 이름을 입력합니다 `admin` 및 암호 `admin`. Adobe은 테스트를 위해 사전 구성된 관리자 계정을 사용할 것을 권장합니다.

이제 macOS이 WebDAV를 통해 AEM에 연결되었으며 Mac의 다른 폴더로 사용할 수 있습니다.

### Linux® {#linux}

Linux®에서 WebDAV를 통해 연결하는 경우 구성이 필요하지 않지만 몇 가지 단계를 수행하여 데스크탑 환경에 따라 다르게 연결할 수 있습니다.

#### 그놈 {#gnome}

GNOME을 사용하여 WebDAV를 통해 AEM에 연결하려면:

1. Nautilus(파일 탐색기)에서 **위치** 및 선택 **서버에 연결**.
1. 다음에서 **서버에 연결** 서비스 유형에서 WebDAV(HTTP)를 선택합니다.

1. 위치 **서버**, 입력 `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >AEM이 다른 포트에 있는 경우 4502 대신 해당 포트 번호를 사용하십시오. 또한 로컬 시스템에서 컨텐츠 저장소를 실행하지 않는 경우 `localhost` (각 서버 이름 또는 IP 주소 포함)

1. 위치 **폴더**, 입력 `/dav`
1. 사용자 이름 입력 `admin`. Adobe은 테스트를 위해 사전 구성된 관리자 계정을 사용할 것을 권장합니다.
1. 포트를 비워 두고 연결의 이름을 입력합니다.
1. **연결**&#x200B;을 클릭합니다. AEM에 암호를 입력하라는 메시지가 표시됩니다.
1. 암호 입력 `admin` 및 클릭 **연결**.

GNOME은 이제 AEM을 볼륨으로 탑재했으며 다른 볼륨처럼 사용할 수 있습니다.

#### KDE {#kde}

1. 네트워크 폴더 마법사를 엽니다.
1. 선택 **웹 폴더**(webdav) 를 클릭하고 다음 을 클릭합니다.
1. 위치 **이름**&#x200B;를 클릭하고 연결 이름을 입력합니다.
1. 위치 **사용자**, 입력 `admin.` Adobe은 사전 구성된 관리자 계정을 사용할 것을 권장합니다.
1. 위치 **서버**, 입력 `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >AEM이 다른 포트에 있는 경우 4502 대신 해당 포트 번호를 사용하십시오. 또한 로컬 시스템에서 컨텐츠 저장소를 실행하지 않는 경우 `localhost` 해당 서버 이름 또는 IP 주소 사용

1. 위치 **폴더**, 입력 `dav`

1. 클릭 **저장 및 연결**.
1. 암호를 입력하라는 메시지가 표시되면 암호를 입력합니다 `admin` 및 클릭 **연결**.

KDE는 이제 AEM을 볼륨으로 탑재했으며 다른 볼륨처럼 사용할 수 있습니다.
