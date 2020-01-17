---
title: 可用性グループの DTC サービスをクラスター化する
description: 'Always On 可用性グループ用に Microsoft 分散トランザクション コーディネーター (DTC) サービスをクラスター化するための要件と手順について説明します。 '
ms.custom: seo-lt-2019
ms.date: 08/30/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: a47c5005-20e3-4880-945c-9f78d311af7a
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: b16af8c06f6ce1a5ab221f267b5b16dde27b587e
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244392"
---
# <a name="how-to-cluster-the-dtc-service-for-an-always-on-availability-group"></a>Always On 可用性グループの DTC サービスをクラスター化する方法

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

このトピックでは、[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 用に Microsoft 分散トランザクション コーディネーター (DTC) サービスをクラスター化するための要件と手順について説明します。 分散トランザクションと [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]の詳細については、「 [Always On 可用性グループとデータベース ミラーリングでの複数データベースにまたがるトランザクションと分散トランザクション &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)」をご覧ください。

 ## <a name="checklist-preliminary-requirements"></a>チェックリスト:準備要件

||タスク|リファレンス|  
|------|-----------------|----------|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|すべてのノード、サービス、可用性グループが正しく構成されていることを確認します。|[Always On 可用性グループの前提条件、制限事項、推奨事項 (SQL Server)](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)|
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|可用性グループの DTC 要件が満たされていることを確認します。|[Always On 可用性グループとデータベース ミラーリングでの複数データベースにまたがるトランザクションと分散トランザクション (SQL Server)](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)

## <a name="checklist-clustered-dtc-resource-dependencies"></a>チェックリスト:クラスター化された DTC リソースの依存関係

||タスク|リファレンス|  
|------|-----------------|----------|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|共有記憶域ドライブ。|[Configuring the Shared-Storage Drive](https://msdn.microsoft.com/library/cc982358(v=bts.10).aspx)(共有記憶域ドライブの構成)。 ドライブ文字に **M**を使用することを検討します。|
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|固有の DTC ネットワーク名リソース。  名前は、Active Directory にクラスター コンピューター オブジェクトとして登録されます。<br /><br />次のいずれかが満たされていることを確認します。<br /><br />•  DTC ネットワーク名リソースを作成するユーザーに、DTC ネットワーク名リソースが保存される OU またはコンテナーに対するコンピューター オブジェクト作成アクセス許可があること。<br /><br />•  ユーザーにコンピューター オブジェクトの作成アクセス許可がない場合は、DTC ネットワーク名リソース用のクラスター コンピューター オブジェクトの用意をドメイン管理者に依頼します。|[Active Directory ドメイン サービスでクラスター コンピューター オブジェクトをプレステージする](https://technet.microsoft.com/library/dn466519(v=ws.11).aspx)|
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|使用可能な有効な静的 IP アドレスとその IP アドレスの適切なサブネット マスク。||

## <a name="cluster-the-dtc-resource"></a>DTC リソースをクラスター化する
可用性グループ リソースを作成したら、クラスター化された DTC リソースを作成し、可用性グループに追加します。  サンプル スクリプトは「[Create Clustered DTC for an Always On Availability Group](../../../database-engine/availability-groups/windows/create-clustered-dtc-for-an-always-on-availability-group.md)」(AlwaysOn 可用性グループのクラスター化された DTC を作成する) で確認できます。


## <a name="checklist-post-clustered-dtc-resource-configurations"></a>チェックリスト:クラスター化 DTC リソースの事後構成

||タスク|リファレンス|  
|------|-----------------|----------|  
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|クラスター化された DTC リソースへの安全なネットワーク アクセスを有効にします。|[MS DTC への安全なネットワーク アクセスを有効にする](https://technet.microsoft.com/library/cc753620(v=ws.10).aspx)|
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|ローカル DTC サービスを停止して無効にします。|[サービスの開始方法を構成する](https://technet.microsoft.com/library/cc755249(v=ws.11).aspx)|
|![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|可用性グループの各インスタンスの SQL Server サービスを停止して再開します。  必要に応じて可用性グループをフェールオーバーします。|[可用性グループの計画的な手動フェールオーバーの実行 (SQL Server)](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)<br /><br />[データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](../../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)|

- サーバーが Windows Server 2012 R2 の場合、オペレーティング システムに [KB 3030373](https://support.microsoft.com/kb/3090973) が適用されている必要があります。

- [AlwaysOn 可用性グループの前提条件、制限事項、および推奨事項](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)のチェックリストに従って、可用性グループ用にサーバーを準備します。

- [**Always On 可用性グループ**](../../../database-engine/availability-groups/windows/configuration-of-a-server-instance-for-always-on-availability-groups-sql-server.md)のサーバー インスタンスを構成します。

### <a name="resources"></a>リソース


[可用性グループでの DTC のテストに関する詳細については、次を参照してください。](https://blogs.technet.microsoft.com/dataplatform/2016/01/25/sql-server-2016-dtc-support-in-availability-groups/)

[AlwaysOn 可用性グループ システム ビューの監視](monitor-availability-groups-transact-sql.md)

[可用性グループの作成の手順](create-an-availability-group-transact-sql.md)


[可用性グループでの SQL Server 2016 DTC のサポート](https://blogs.technet.microsoft.com/dataplatform/2016/01/25/sql-server-2016-dtc-support-in-availability-groups/) 

[外部リンク: Windows Server 2008 R2 で SQL Server のクラスター化されたインスタンスの DTC を構成する](https://sqlha.com/2013/03/12/how-to-properly-configure-dtc-for-clustered-instances-of-sql-server-with-windows-server-2008-r2/)
