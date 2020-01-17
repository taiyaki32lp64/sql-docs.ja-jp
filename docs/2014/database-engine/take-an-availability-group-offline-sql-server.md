---
title: 可用性グループをオフラインにする
description: Always On 可用性グループをオフラインに設定する手順
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], take offline
ms.assetid: 50f5aad8-0dff-45ef-8350-f9596d3db898
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 87dff347bd0aee1211093d9e3406a24670a80e7f
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228169"
---
# <a name="take-an-availability-group-offline-sql-server"></a>可用性グループをオフラインにする (SQL Server)
  このトピックでは、 [!INCLUDE[tsql](../includes/tsql-md.md)] の [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 以降のバージョンを使用して、AlwaysOn 可用性グループを ONLINE 状態から OFFLINE 状態にする方法について説明します。 同期コミット レプリカが同期されていない場合は OFFLINE 操作でエラーが発生し、可用性グループは ONLINE を維持するため、同期コミット データベースのデータ損失はありません。 可用性グループをオンラインにしておくと、非同期コミット データベースで発生する可能性があるデータ損失が防止されます。 可用性グループがオフラインになると、クライアントはそのデータベースを使用できなくなりますが、可用性グループをオンラインに戻すことはできません。 したがって、可用性グループは、可用性グループのリソースを WSFC クラスター間で移行する場合のみオフラインにしてください。  
  
 
  [!INCLUDE[ssHADR](../includes/sshadr-md.md)]のクラスター間での移行時は、任意のアプリケーションが可用性グループのプライマリ レプリカに直接接続している場合は、可用性グループをオフラインにする必要があります。 
  [!INCLUDE[ssHADR](../includes/sshadr-md.md)] のクラスター間の移行は、可用性グループの最小限のダウンタイムで OS のアップグレードをサポートします。 一般的なシナリオは、 [!INCLUDE[ssHADR](../includes/sshadr-md.md)] のクラスター間の移行を、 [!INCLUDE[win8](../includes/win8-md.md)] または [!INCLUDE[win8srv](../includes/win8srv-md.md)]への OS のアップグレードで使用することです。 詳細については、「[OS アップグレードのための AlwaysOn 可用性グループのクラスター間での移行](https://msdn.microsoft.com/library/jj873730.aspx)」を参照してください。  
  

  
##  <a name="BeforeYouBegin"></a>開始する前に  
  
> [!CAUTION]  
>  OFFLINE オプションは、可用性グループのリソースをクラスター間で移行する場合のみ使用してください。  
  
###  <a name="Prerequisites"></a>応募  
  
-   OFFLINE コマンドを入力するサーバー インスタンスが、 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 以上 (Enterprise Edition 以上) を実行している必要があります。  
  
-   可用性グループが現在オンラインになっている必要があります。  
  
###  <a name="Recommendations"></a>推奨事項  
 可用性グループをオフラインにする前に、可用性グループ リスナーを削除します。 詳細については、「 [可用性グループ リスナーの削除 &#40;SQL Server&#41;](availability-groups/windows/remove-an-availability-group-listener-sql-server.md)への OS のアップグレードで使用することです。  
  
###  <a name="Security"></a>保護  
  
####  <a name="Permissions"></a>許可  
 可用性グループの ALTER AVAILABILITY GROUP 権限、CONTROL AVAILABILITY GROUP 権限、ALTER ANY AVAILABILITY GROUP 権限、または CONTROL SERVER 権限が必要です。  
  
##  <a name="TsqlProcedure"></a>Transact-sql の使用  
 **可用性グループをオフラインにするには**  
  
1.  可用性グループの可用性レプリカをホストしているサーバー インスタンスに接続します。 このレプリカは、プライマリ レプリカでもセカンダリ レプリカでもかまいません。  
  
2.  
  [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) ステートメントを使用します。次にその例を示します。  
  
     ALTER AVAILABILITY GROUP *group_name* OFFLINE  
  
     
  *group_name* は可用性グループの名前です。  
  
### <a name="example"></a>例  
 次の例では、 `AccountsAG` 可用性グループをオフラインにします。  
  
```sql
ALTER AVAILABILITY GROUP AccountsAG OFFLINE;  
```  
  
##  <a name="FollowUp"></a>補足情報: 可用性グループがオフラインになった後  
  
-   **オフライン操作のログ記録:** オフライン操作が開始された WSFC ノードの id は、WSFC クラスターログと SQL エラーログの両方に格納されます。  
  
-   **グループをオフラインにする前に可用性グループリスナーを削除していない場合は、次のようにします。** 可用性グループを別の WSFC クラスターに移行する場合は、リスナーの VNN と VIP を削除します。 これらは、フェールオーバー クラスター管理コンソール、 [Remove-ClusterResource](https://technet.microsoft.com/library/ee461015\(WS.10\).aspx) PowerShell コマンドレット、または [cluster.exe](https://technet.microsoft.com/library/ee461015\(WS.10\).aspx)を使用して削除できます。 cluster.exe は Windows 8 では非推奨とされることに注意してください。  
  
##  <a name="RelatedTasks"></a>関連タスク  
  
-   [可用性グループリスナー &#40;SQL Server の削除&#41;](availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
-   [サーバーインスタンスの HADR クラスターコンテキストを変更する &#40;SQL Server&#41;](availability-groups/windows/change-the-hadr-cluster-context-of-server-instance-sql-server.md)  
  
##  <a name="RelatedContent"></a>関連するコンテンツ  
  
-   [SQL Server 2012 の技術記事](https://msdn.microsoft.com/library/bb418445\(SQL.10\).aspx)  
  
-   [SQL Server AlwaysOn チーム ブログ:SQL Server AlwaysOn チームのオフィシャル ブログ](https://blogs.msdn.com/b/sqlalwayson/)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループ &#40;SQL Server&#41;](availability-groups/windows/always-on-availability-groups-sql-server.md)  
