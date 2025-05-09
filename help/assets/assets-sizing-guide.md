---
title: '[!DNL Assets] 크기 조정 가이드'
description: ' [!DNL Adobe Experience Manager Assets]을(를) 배포하는 데 필요한 인프라 및 리소스를 예상하는 효율적인 지표를 결정하는 모범 사례입니다.'
contentOwner: AG
role: Architect, Admin
feature: Asset Management
exl-id: fd58ead9-5e18-4f55-8d20-1cf4402fad97
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 0%

---

# [!DNL Assets] 크기 조정 가이드 {#assets-sizing-guide}

[!DNL Adobe Experience Manager Assets] 구현에 대한 환경 크기를 조정할 때 디스크, CPU, 메모리, IO 및 네트워크 처리량 측면에서 사용 가능한 리소스가 충분한지 확인하는 것이 중요합니다. 이러한 리소스의 크기를 조정하려면 시스템에 로드되는 에셋의 수를 이해해야 합니다. 더 나은 지표를 사용할 수 없는 경우 기존 라이브러리의 크기를 라이브러리 사용 기간으로 나누어 자산이 생성되는 비율을 찾을 수 있습니다.

## 디스크 {#disk}

### 데이터 저장소 {#datastore}

[!DNL Assets] 구현에 필요한 디스크 공간 크기를 조정할 때 흔히 저지르는 실수는 시스템에 수집할 원시 이미지의 크기를 기준으로 계산하는 것입니다. 기본적으로 [!DNL Experience Manager]은(는) [!DNL Experience Manager] 사용자 인터페이스 요소를 렌더링하는 데 사용할 원본 이미지 외에 세 개의 렌디션을 만듭니다. 이전 구현에서 이러한 렌디션은 수집하는 에셋의 크기를 두 배로 가정하는 것으로 관찰되었습니다.

대부분의 사용자는 기본 제공 렌디션 외에 사용자 정의 렌디션을 정의합니다. 렌디션 외에 [!DNL Assets]을(를) 사용하면 [!DNL Adobe InDesign] 및 [!DNL Adobe Illustrator]과(와) 같은 일반적인 파일 형식에서 하위 자산을 추출할 수 있습니다.

마지막으로, [!DNL Experience Manager]의 버전 관리 기능은 버전 기록에 중복 에셋을 저장합니다. 삭제되는 버전을 자주 구성할 수 있습니다. 그러나 많은 사용자가 시스템에서 버전을 장기간 유지하도록 선택하므로 추가 저장 공간이 필요합니다.

이러한 요소들을 고려하여 사용자 자산을 저장할 수 있을 만큼 정확한 저장 공간을 계산하는 방법론이 필요합니다.

1. 시스템에 로드되는 에셋의 크기와 수를 결정합니다.
1. [!DNL Experience Manager] (으)로 업로드할 대표적인 자산 샘플을 얻습니다. 예를 들어 PSD, JPG, AI 및 PDF 파일을 시스템에 로드하려는 경우 각 파일 형식의 여러 샘플 이미지가 필요합니다. 또한 이러한 샘플은 이미지의 다양한 파일 크기와 복잡성을 나타냅니다.
1. 사용할 렌디션을 정의합니다.
1. [!DNL ImageMagick] 또는 [!DNL Adobe Creative Cloud] 응용 프로그램을 사용하여 [!DNL Experience Manager]에서 렌디션을 만듭니다. 사용자가 지정하는 렌디션 외에도 기본 렌디션을 만듭니다. Dynamic Media을 구현하는 사용자의 경우 IC 바이너리를 사용하여 Experience Manager에 저장할 PTIFF 표현물을 생성할 수 있습니다.
1. 하위 에셋을 사용하려는 경우 적절한 파일 형식에 대해 하위 에셋을 생성합니다.
1. 출력 이미지, 렌디션 및 하위 에셋의 크기를 원본 이미지와 비교합니다. 시스템이 로드될 때 예상 증가 계수를 생성할 수 있습니다. 예를 들어, 1GB의 에셋을 처리한 후 조합 크기가 3GB인 렌디션과 하위 에셋을 생성하는 경우 렌디션 증가 인자는 3입니다.
1. 시스템에서 에셋 버전을 유지 관리할 최대 시간을 결정합니다.
1. 시스템에서 기존 에셋을 수정하는 빈도를 결정합니다. [!DNL Experience Manager]이(가) Creative Workflow에서 공동 작업 허브로 사용되는 경우 변경량이 많습니다. 완료된 자산만 시스템에 업로드하는 경우 이 숫자는 훨씬 적습니다.
1. 매월 시스템에 로드되는 에셋 수를 결정합니다. 확실하지 않은 경우 현재 사용할 수 있는 에셋 수를 확인하고 가장 오래된 에셋의 연령을 기준으로 숫자를 나누어 대략적인 숫자를 계산합니다.

위의 단계를 수행하면 다음을 확인할 수 있습니다.

* 로드할 자산의 원시 크기입니다.
* 로드할 자산 수.
* 렌디션 증가 요소.
* 매월 수정된 자산 수입니다.
* 자산 버전을 유지 관리하기 위한 개월 수.
* 매월 로드되는 새 에셋 수
* 스토리지 공간 할당을 위한 수년간의 증가.

네트워크 크기 조정 스프레드시트에서 이러한 숫자를 지정하여 데이터 저장소에 필요한 총 공간을 결정할 수 있습니다. 또한 자산 버전을 유지하거나 [!DNL Experience Manager]의 자산을 수정하여 디스크 증가에 미치는 영향을 확인하는 데 유용한 도구입니다.

도구에 채워진 예제 데이터는 위에 언급된 단계를 수행하는 것이 얼마나 중요한지 보여줍니다. 로드되는 원시 이미지(1TB)만을 기준으로 데이터 저장소의 크기를 조정하는 경우 저장소 크기를 15배율로 과소평가했을 수 있습니다.

[파일 가져오기](assets/disk_sizing_tool.xlsx)

### 공유 데이터 저장소 {#shared-datastores}

대규모 데이터 저장소의 경우 네트워크 연결 드라이브의 공유 파일 데이터 저장소 또는 Amazon S3 데이터 저장소를 통해 공유 데이터 저장소를 구현할 수 있습니다. 이 경우 개별 인스턴스는 바이너리의 사본을 유지 관리할 필요가 없습니다. 또한 공유 데이터 저장소는 바이너리 없는 복제를 용이하게 하며 자산을 게시 환경으로 복제하는 데 사용되는 대역폭을 줄이는 데 도움이 됩니다.

#### 사용 사례 {#use-cases}

기본 작성자 인스턴스와 대기 작성자 인스턴스 간에 데이터 저장소를 공유하여 기본 인스턴스의 변경 내용으로 대기 인스턴스를 업데이트하는 데 걸리는 시간을 최소화할 수 있습니다. 또한 작성자와 게시 인스턴스 간에 데이터 저장소를 공유하여 복제 중 트래픽을 최소화할 수 있습니다.

#### 단점 {#drawbacks}

일부 위험 때문에 데이터 저장소를 공유하는 것은 모든 경우에 권장되지 않습니다.

#### 단일 장애 지점 {#single-point-of-failure}

공유 데이터 저장소가 있으면 인프라에 단일 장애 지점이 생깁니다. 시스템에 각각 고유한 데이터 저장소가 있는 작성자 1개와 게시 인스턴스 2개가 있는 시나리오를 생각해 보십시오. 둘 중 하나가 충돌해도 나머지 두 개는 계속 실행될 수 있습니다. 그러나 데이터 저장소를 공유하는 경우 단일 디스크 장애로 전체 인프라가 중단될 수 있습니다. 따라서 데이터 저장소를 빠르게 복원할 수 있는 공유 데이터 저장소의 백업을 유지 관리해야 합니다.

공유 데이터 저장소에 AWS S3 서비스를 배포하면 일반 디스크 아키텍처에 비해 실패 확률이 크게 감소하므로 선호됩니다.

#### 복잡성 증가 {#increased-complexity}

공유 데이터 저장소는 가비지 수집과 같은 작업의 복잡성도 증가시킵니다. 일반적으로 독립형 데이터 저장소에 대한 가비지 수집은 한 번의 클릭으로 시작할 수 있습니다. 그러나 공유 데이터 저장소는 단일 노드에서 실제 컬렉션을 실행하는 것 외에도 데이터 저장소를 사용하는 각 멤버에 대해 표시 스윕 작업이 필요합니다.

AWS 작업의 경우 EBS 볼륨의 RAID 어레이를 구축하는 대신 단일 중앙 위치(Amazon S3 사용)를 구현하면 시스템의 복잡성과 운영 위험을 크게 줄일 수 있습니다.

#### 성능 관련 문제 {#performance-concerns}

공유 데이터 저장소를 사용하려면 모든 인스턴스 간에 공유되는 네트워크 탑재 드라이브에 바이너리를 저장해야 합니다. 이러한 바이너리는 네트워크를 통해 액세스되므로 시스템 성능에 부정적인 영향을 줍니다. 빠른 네트워크 연결을 사용하여 빠른 디스크 배열에 미치는 영향을 부분적으로 줄일 수 있습니다. 그러나, 이것은 값비싼 제안이다. AWS 작업이 있는 경우 모든 디스크가 원격이며 네트워크 연결이 필요합니다. 인스턴스 시작 또는 중지 시 사용 후 볼륨에서 데이터가 손실됩니다.

#### 지연 {#latency}

S3 구현의 지연은 백그라운드 쓰기 스레드에 의해 도입됩니다. 백업 절차는 이러한 지연 시간을 고려해야 합니다. 또한 백업을 수행할 때 Lucene 인덱스가 완료되지 않은 상태로 남아 있을 수 있습니다. S3 데이터 저장소에 기록되고 다른 인스턴스에서 액세스되는 모든 시간에 민감한 파일에 적용됩니다.

### 노드 저장소 또는 문서 저장소 {#node-store-document-store}

NodeStore 또는 DocumentStore의 정확한 크기 조정 수치에 도달하기 어려운 이유는 다음 리소스로 인해 발생합니다.

* 에셋 메타데이터
* 에셋 버전
* 감사 로그
* 보관 및 활성 워크플로우

바이너리는 데이터 저장소에 저장되므로 각 바이너리는 일부 공간을 차지합니다. 대부분의 저장소 크기는 100GB 미만입니다. 그러나 최대 1TB의 용량이 큰 저장소가 있을 수 있습니다. 또한 오프라인 압축을 수행하려면 미리 압축된 버전과 함께 압축된 저장소를 다시 작성하기 위해 볼륨에 충분한 여유 공간이 필요합니다. 가장 좋은 방법은 저장소의 예상 크기를 1.5배로 늘리는 것입니다.

저장소의 경우 IOPS 수준이 3000보다 큰 SSD 또는 디스크를 사용합니다. IOPS로 인해 성능 병목 현상이 발생할 가능성을 없애려면 CPU IO 대기 수준을 모니터링하여 문제의 조기 징후를 파악합니다.

[파일 가져오기](assets/aem_environment_sizingtool.xlsx)

## 네트워크 {#network}

[!DNL Assets]에는 많은 [!DNL Experience Manager] 프로젝트보다 네트워크 성능을 더 중요하게 만드는 여러 사용 사례가 있습니다. 고객의 서버 속도가 빠를 수 있지만, 시스템에서 에셋을 업로드하고 다운로드하는 사용자의 로드를 지원할 만큼 네트워크 연결이 크지 않으면 여전히 속도가 느린 것으로 표시됩니다. [사용자 경험, 인스턴스 크기 조정, 워크플로 평가 및 네트워크 토폴로지에 대한 Assets 고려 사항](/help/assets/assets-network-considerations.md)에서 [!DNL Experience Manager]에 대한 사용자의 네트워크 연결에서 제한점을 확인하는 데 좋은 방법이 있습니다.

## 제한 사항 {#limitations}

구현 크기를 조정할 때는 시스템 제한 사항을 염두에 두는 것이 중요합니다. 제안된 구현이 이러한 제한을 초과하는 경우 여러 [!DNL Assets] 구현 간에 에셋을 분할하는 등 창의적인 전략을 사용하십시오.

파일 크기만이 메모리 부족(OOM) 문제에 기여하는 유일한 요소는 아닙니다. 또한 이미지의 크기에 따라 다릅니다. [!DNL Experience Manager]을(를) 시작할 때 더 높은 힙 크기를 제공하면 OOM 문제를 방지할 수 있습니다.

또한 구성 관리자에서 `com.day.cq.dam.commons.handler.StandardImageHandler` 구성 요소의 임계값 크기 속성을 편집하여 0보다 큰 중간 임시 파일을 사용할 수 있습니다.

## 최대 자산 수 {#maximum-number-of-assets}

파일 시스템 제한 사항으로 인해 데이터 저장소에 존재할 수 있는 파일 수 제한은 21억 개입니다. 데이터 저장소 제한에 도달하기 오래 전에 많은 수의 노드로 인해 저장소에 문제가 발생할 수 있습니다.

Camera Raw 렌디션이 잘못 생성된 경우 라이브러리를 사용합니다. 단, 이 경우 이미지의 가장 긴 변이 65000 픽셀보다 크지 않아야 합니다. 또한 이미지에는 512MP(512 x 1024 x 1024픽셀)를 초과할 수 없습니다. 에셋의 크기는 중요하지 않습니다.

픽셀 크기와 같은 추가 요소가 처리에 영향을 주므로 [!DNL Experience Manager]에 대한 특정 힙을 사용하여 즉시 지원되는 TIFF 파일의 크기를 정확하게 추정하기는 어렵습니다. [!DNL Experience Manager]에서 255MB의 파일을 즉시 처리할 수 있지만, 18MB의 파일 크기는 처리할 수 없습니다. 왜냐하면 후자의 픽셀이 전자의 픽셀보다 비정상적으로 더 많기 때문입니다.

## 에셋 크기 {#size-of-assets}

기본적으로 [!DNL Experience Manager]을(를) 사용하면 최대 2GB의 파일 크기 에셋을 업로드할 수 있습니다. [!DNL Experience Manager]에서 매우 큰 에셋을 업로드하려면 [매우 큰 에셋을 업로드하는 구성](managing-video-assets.md#configuration-to-upload-assets-that-are-larger-than-gb)을 참조하십시오.
