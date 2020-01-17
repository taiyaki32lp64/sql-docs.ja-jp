---
title: 可用性グループでのリモート BLOB ストア (RBS)
description: 'Always On 可用性グループの一部であるデータベースでリモート Blob ストア (RBS) を使用する方法について説明します。 '
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 01a70258-d4fd-40bc-bc44-c490b5d6c420
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 864ed8080c3978ec272f5212fa0a5e8dc40c2350
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822486"
---
# <a name="use-remote-blob-store-rbs-with-always-on-availability-groups"></a>Always On 可用性グループでのリモート BLOB ストア (RBS) の使用
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] では、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][リモート BLOB ストア (RBS)](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md) の BLOB オブジェクトの高可用性およびディザスター リカバリー ソリューションを提供できます。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] では、可用性データベースに格納されている RBS メタデータとスキーマをセカンダリ レプリカにレプリケートすることによってこれらを保護します。 これは SharePoint コンテンツ データベースです。 一般に、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、この RBS メタデータが BLOB とは別に格納されます。  
  
 次のように、RBS の BLOB データの保護は BLOB ストアの場所によって異なります。  
  
|BLOB ストアの場所|可用性グループによるこの BLOB データの保護|  
|-------------------------|-----------------------------------------------------|  
|RBS メタデータを含む同じデータベース (RBS リモート FILESTREAM プロバイダーを使用して格納)|はい|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の同じインスタンスにある別のデータベース (RBS リモート FILESTREAM プロバイダーを使用して格納)|はい<br /><br /> このデータベースは、RBS メタデータを含むデータベースと同じ可用性グループに含めることをお勧めします。|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の別のインスタンスにある別のデータベース (RBS リモート FILESTREAM プロバイダーを使用して格納)|はい<br /><br /> このデータベースは、別の可用性グループに含まれている必要があります。|  
|サード パーティの BLOB ストア|いいえ<br /><br /> この BLOB データを保護するには、BLOB ストア プロバイダーの高可用性メカニズムを使用します。|  
  
##  <a name="Limitations"></a> 制限事項  
  
-   RBS Maintainer は、プライマリ レプリカで対象にする必要があります。  
  
##  <a name="Recommendations"></a> 推奨事項  
  
-   可用性グループ リスナーを使用します。 詳細については、「 [可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)での 1 つ以上の可用性グループの構成と管理において重要です。  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   [リモート BLOB ストアのメンテナンス](https://msdn.microsoft.com/library/gg316773\(SQL.105\).aspx) ( [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] オンライン ブック)  
  
-   [RBS Maintainer の実行](https://blogs.msdn.com/b/sqlrbs/archive/2010/03/19/running-rbs-maintainer.aspx) (ブログ)  
  
-   [FILESTREAM プロバイダーでのリモート BLOB ストレージ (RBS) の構成 (SharePoint 2010)](https://blogs.msdn.com/b/mvpawardprogram/archive/2012/04/02/configure-remote-blob-storage-rbs-with-the-filestream-provider-sharepoint-2010.aspx) (ブログ)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn クライアントの接続 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)   
 [リモート BLOB ストア &#40;RBS&#41; &#40;SQL Server&#41;](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
  
  
