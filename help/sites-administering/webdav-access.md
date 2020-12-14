---
title: WebDAV 액세스
seo-title: WebDAV 액세스
description: AEM에서 WebDAV 액세스 방법에 대해 알아봅니다.
seo-description: AEM에서 WebDAV 액세스 방법에 대해 알아봅니다.
uuid: b0ecaa5d-5454-42df-8453-404ece734c32
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 1eaf7afe-a181-45df-8766-bd564b1ad22a
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 1%

---


# WebDAV Access{#webdav-access}

KDE와 WebDAV를 통해 AEM에 연결하려면:

AEM은 저장소 컨텐츠를 표시하고 편집할 수 있는 WebDAV 지원을 제공합니다. WebDAV를 통해 연결하면 데스크탑을 통해 컨텐츠 저장소에 바로 액세스할 수 있습니다. WebDAV 연결을 통해 저장소에 추가되는 텍스트 및 PDF 파일은 자동으로 전체 텍스트 인덱싱되며 표준 검색 인터페이스와 표준 Java API를 통해 검색할 수 있습니다.

## 일반 {#general}

[이 문서에는 운영 ](/help/sites-administering/webdav-access.md#connecting-via-webdav) 체제별 세부 지침이 포함되어 있지만 WebDAV 프로토콜을 사용하여 저장소에 연결하는 것은 기본적으로 WebDAV 클라이언트를 다음 위치로 지정합니다.

```xml
http://localhost:4502
```

![chlimage_1-111](assets/chlimage_1-111a.png)

이 URL은 운영 체제 수준에서 연결되면 기본 작업 영역( `crx.default`)에 대한 WebDAV 액세스를 제공합니다. 사용자는 작업 영역 이름을 보다 간단하게 사용할 수 있지만 추가 [WebDAV URL](/help/sites-administering/webdav-access.md#webdav-urls)을(를) 사용하여 수행할 수 있는 작업 영역 이름을 지정할 때의 추가 유연성을 제공하지 않습니다.

AEM에는 다음과 같이 리포지토리 컨텐츠가 표시됩니다.

* `nt:folder` 유형의 노드가 폴더로 표시됩니다. `nt:folder` 노드 아래의 노드는 폴더 컨텐츠로 표시됩니다.

* `nt:file` 유형의 노드가 파일로 표시됩니다. `nt:file` 노드 아래의 노드는 표시되지 않지만 파일의 내용을 형성합니다.

WebDAV를 사용하여 폴더 및 파일을 만들고 편집하는 경우 AEM은 필요한 `nt:folder` 및 `nt:file` 노드를 만들고 편집합니다. WebDAV를 사용하여 내용을 가져오고 내보내려는 경우 `nt:file` 및 `nt:folder` 노드 유형을 가능한 한 많이 사용해 보십시오.

>[!NOTE]
>
>WebDAV를 설정하기 전에 [기술 요구 사항](/help/sites-deploying/technical-requirements.md#webdav-clients)을 확인하십시오.

## WebDAV URL {#webdav-urls}

WebDAV 서버의 URL에는 다음 구조가 있습니다.

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
   <td>AEM 리포지토리 웹 앱용 경로</td>
   <td>WebDAV 서블릿이 매핑되는 경로</td>
   <td>작업 영역의 이름</td>
  </tr>
 </tbody>
</table>

경로의 작업 영역 요소를 변경하면 기본값( `crx.default`) 이외의 작업 영역을 매핑할 수 있습니다. 예를 들어 `staging`이라는 작업 영역을 매핑하려면 다음 URL을 사용하십시오.

```xml
http://localhost:4502/crx/repository/staging
```

## WebDAV {#connecting-via-webdav}을(를) 통해 연결

[위에](/help/sites-administering/webdav-access.md#general) 언급했듯이 WebDAV 프로토콜을 사용하여 저장소에 연결하려면 WebDAV 클라이언트를 저장소 위치로 지정합니다. 그러나 OS에 따라 클라이언트 연결에 관련된 단계가 다르며 필요한 OS의 구성이 있을 수 있습니다.

다음 운영 체제를 연결하는 방법에 대한 지침이 제공됩니다.

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

Microsoft Windows 7 이상 시스템을 SSL로 보안이 설정되지 않은 AEM 인스턴스에 성공적으로 연결하려면 Windows에서 비보안 네트워크를 통해 기본 인증을 설정하는 옵션을 명시적으로 설정해야 합니다. WebClient의 Windows 레지스트리를 변경해야 합니다.

레지스트리가 업데이트되면 AEM 인스턴스를 드라이브로 매핑할 수 있습니다.

#### Windows 7 이상 구성 {#windows-and-greater-configuration}

보안되지 않은 네트워크에 대한 기본 인증을 허용하도록 레지스트리를 업데이트하려면:

1. 다음 레지스트리 하위 키를 찾습니다.

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. `BasicAuthLevel` 레지스트리 항목 하위 키를 `2` 이상의 값으로 설정합니다.

   없는 경우 하위 키를 추가합니다.

1. 레지스트리 변경 사항을 적용하려면 시스템을 다시 시작해야 합니다.

이 레지스트리 변경에 대한 자세한 내용은 [Microsoft 지원 KB 841215](https://support.microsoft.com/default.aspx/kb/841215)을 참조하십시오.

Windows에서 WebDav 클라이언트의 응답 향상에 대한 자세한 내용은 [Microsoft 지원 KB 2445570](https://support.microsoft.com/kb/2445570)을 참조하십시오.

>[!NOTE]
>
>Adobe에서는 저장소 사용자와 동일한 자격 증명을 사용하여 Windows 사용자를 만드는 것이 좋습니다. 그렇지 않으면 권한 충돌이 발생할 수 있습니다.

#### Windows 8 구성 {#windows-configuration}

Windows 8의 경우 Windows 7 이상](/help/sites-administering/webdav-access.md#windows-and-greater-configuration)에 대해 설명된 대로 레지스트리 항목 [을 변경해야 합니다. 그러나 레지스트리 항목을 보려면 먼저 데스크탑 경험을 활성화해야 합니다.

데스크탑 경험을 활성화하려면 **서버 관리자**&#x200B;를 열고 **기능**&#x200B;을 선택한 다음 **기능 추가**&#x200B;을 선택한 다음 **데스크탑 경험**&#x200B;을(를) 엽니다.

Windows 7 이상 버전에 대해 설명된 레지스트리 항목을 재부팅한 후 사용할 수 있습니다. Windows 7 이상에 대해 설명된 대로 수정합니다.

#### Windows {#connecting-in-windows}에서 연결

Windows 환경에서 WebDAV를 통해 AEM에 연결하려면:

1. **Windows 탐색기** 또는 **파일 탐색기**&#x200B;를 열고 **컴퓨터** 또는 **이 PC**&#x200B;을 클릭합니다.

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. **네트워크 드라이브 매핑**&#x200B;을 클릭하여 마법사를 시작합니다.
1. 매핑 세부 정보를 입력합니다.

   * **드라이브**:사용 가능한 편지 선택
   * **폴더**:  `http://localhost:4502`
   * 다른 자격 증명을 사용하여 **연결 확인**

   마침을 클릭합니다.

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >AEM이 다른 포트에 있는 경우 4502 대신 해당 포트 번호를 사용하십시오. 또한 로컬 컴퓨터에서 컨텐츠 저장소를 실행하고 있지 않으면 `localhost`을(를) 해당 서버 이름 또는 IP 주소로 바꾸십시오.

1. 사용자 이름 `admin` 및 암호 `admin`를 입력합니다. Adobe은 테스트용으로 사전 구성된 관리 계정을 사용하는 것이 좋습니다.

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. 마법사가 닫히고 새로 매핑된 드라이브가 Windows 탐색기 또는 파일 탐색기 창에서 열립니다.

   ![chlimage_1-115](assets/chlimage_1-115a.png)

이제 Windows에서는 AEM을 WebDAV를 통해 드라이브로 매핑했으며 다른 드라이브로 사용할 수 있습니다.

### macOS {#macos}

macOS에서 WebDAV를 통해 연결할 때는 구성 단계가 필요하지 않습니다. WebDAV 서버에 연결하면 됩니다.

1. **Finder** 창으로 이동하여 **Go** 및 **서버에 연결**&#x200B;을 클릭하거나 **Command+k**&#x200B;을 누릅니다.
1. **서버에 연결** 창에서 AEM 위치를 입력합니다.

   * `http://localhost:4502`
   >[!NOTE]
   >
   >AEM이 다른 포트에 있는 경우 4502 대신 해당 포트 번호를 사용하십시오. 또한 로컬 컴퓨터에서 컨텐츠 저장소를 실행하고 있지 않으면 `localhost`을(를) 해당 서버 이름 또는 IP 주소로 바꾸십시오.

1. 인증 메시지가 표시되면 사용자 이름 `admin` 및 암호 `admin`를 입력합니다. Adobe은 테스트용으로 사전 구성된 관리 계정을 사용하는 것이 좋습니다.

macOS는 이제 WebDAV를 통해 AEM에 연결되어 있으므로 Mac에서 다른 폴더로 사용할 수 있습니다.

### Linux {#linux}

Linux에서 WebDAV를 통해 연결하려면 어떤 구성도 필요하지 않지만 데스크톱 환경에 따라 다른 방식으로 연결을 만들기 위해 몇 단계를 거쳐야 합니다.

#### GNOME {#gnome}

GNOME를 통해 WebDAV를 통해 AEM에 연결하려면 다음을 수행하십시오.

1. Nautilus(파일 탐색기)에서 **위치**&#x200B;를 선택하고 **서버에 연결**&#x200B;을 선택합니다.
1. **서버에 연결** 창의 서비스 유형에서 WebDAV(HTTP)를 선택합니다.

1. **서버**&#x200B;에 `http://localhost:4502/crx/repository/crx.default`를 입력합니다.

   >[!NOTE]
   >
   >AEM이 다른 포트에 있는 경우 4502 대신 해당 포트 번호를 사용하십시오. 또한 로컬 컴퓨터에서 컨텐츠 저장소를 실행하고 있지 않으면 `localhost`을(를) 해당 서버 이름 또는 IP 주소로 바꾸십시오.

1. **폴더**&#x200B;에 `/dav`를 입력합니다.
1. 사용자 이름 `admin`을 입력합니다. Adobe은 테스트용으로 사전 구성된 관리 계정을 사용하는 것이 좋습니다.
1. 포트를 비워 두고 연결에 사용할 이름을 입력합니다.
1. **Connect**&#x200B;를 클릭합니다. AEM에서 암호를 입력하라는 메시지를 표시합니다.
1. `admin` 암호를 입력하고 **Connect**&#x200B;를 클릭합니다.

GNOME는 이제 AEM을 볼륨으로 마운트했으며 다른 볼륨처럼 사용할 수 있습니다.

#### KDE {#kde}

1. 네트워크 폴더 마법사를 엽니다.
1. **WebFolder**(webdav)을 선택하고 [다음]을 클릭합니다.
1. **이름**&#x200B;에 연결 이름을 입력합니다.
1. **사용자**&#x200B;에 `admin.` Adobe에서 사전 구성된 관리 계정을 사용하는 것이 좋습니다.
1. **서버**&#x200B;에 `http://localhost:4502/crx/repository/crx.default`를 입력합니다.

   >[!NOTE]
   >
   >AEM이 다른 포트에 있는 경우 4502 대신 해당 포트 번호를 사용하십시오. 또한 로컬 컴퓨터에서 컨텐츠 저장소를 실행하고 있지 않으면 `localhost`을(를) 해당 서버 이름 또는 IP 주소로 바꾸십시오

1. **폴더**&#x200B;에 `dav`를 입력합니다.

1. **저장 및 연결**&#x200B;을 클릭합니다.
1. 암호를 입력하라는 메시지가 표시되면 `admin` 암호를 입력하고 **Connect**&#x200B;를 클릭합니다.

KDE는 이제 AEM을 볼륨으로 마운트했으며 다른 볼륨처럼 사용할 수 있습니다.
