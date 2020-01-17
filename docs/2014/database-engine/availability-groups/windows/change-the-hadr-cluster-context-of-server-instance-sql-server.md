---
title: サーバー インスタンスの HADR クラスター コンテキストの変更 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- Availability replicas [SQL Server], change WSFC cluster context
ms.assetid: ecd99f91-b9a2-4737-994e-507065a12f80
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: de783ffdb5480a9cdebec2380f81e50a9cba11ec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62815405"
---
# <a name="change-the-hadr-cluster-context-of-server-instance-sql-server"></a>サーバー インスタンスの HADR クラスター コンテキストの変更 (SQL Server)
  このトピックでは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以降で [!INCLUDE[tsql](../../../includes/tsql-md.md)] を使用して [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] インスタンスの HADR クラスター コンテキストを切り替える方法について説明します。 *HADR クラスター コンテキスト* は、サーバー インスタンスによってホストされる可用性レプリカのメタデータを管理する Windows Server フェールオーバー クラスタリング (WSFC) クラスターを決定します。  
  
 HADR クラスター コンテキストの切り替えは、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] を新しい WSFC クラスター上の [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] インスタンスに移行するクラスター間での移行中にのみ実行します。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] のクラスター間の移行は、可用性グループの最小限のダウンタイムで [!INCLUDE[win8](../../../includes/win8-md.md)] または [!INCLUDE[win8srv](../../../includes/win8srv-md.md)] への OS のアップグレードをサポートします。 詳細については、「[OS アップグレードのための AlwaysOn 可用性グループのクラスター間での移行](https://msdn.microsoft.com/library/jj873730.aspx)」を参照してください。  
  

  
##  <a name="BeforeYouBegin"></a> はじめに  
  
> [!CAUTION]  
>  HADR クラスター コンテキストの切り替えは、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 配置のクラスター間での移行中にのみ実行してください。  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   HADR クラスター コンテキストの切り替えは、ローカル WSFC クラスターとリモート クラスター間でのみ実行できます。 リモート クラスター間で HADR クラスター コンテキストを切り替えることはできません。  
  
-   HADR クラスター コンテキストは、SQL Server インスタンスが可用性レプリカをホストしていない場合のみリモート クラスターに切り替えることができます。  
  
-   リモート HADR クラスター コンテキストは、いつでもローカル クラスターに切り替えることができます。 ただし、コンテキストは、サーバー インスタンスが可用性レプリカをホストしている限り、再度切り替えることはできません。  
  
###  <a name="Prerequisites"></a> 前提条件  
  
-   HADR クラスター コンテキストを変更するサーバー インスタンスは、 [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] 以上 (Enterprise Edition 以上) を実行している必要があります。  
  
-   サーバー インスタンスで AlwaysOn が有効になっている必要があります。 詳細については、「[AlwaysOn 可用性グループの有効化と無効化 &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)」を参照してください。  
  
-   ローカル クラスター コンテキストからリモート クラスターに切り替えるための条件を満たすには、サーバー インスタンスで可用性レプリカをホストしていないことが必要です。 [sys.availability_replicas](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql) カタログ ビューに行は返されません。  
  
     サーバー インスタンス上に可用性レプリカが存在する場合は、HADR クラスター コンテキストを変更する前に、次のいずれかを実行する必要があります。  
  
    |レプリカのロール|操作|リンク|  
    |------------------|------------|----------|  
    |1 次式|可用性グループをオフラインにします。|[可用性グループをオフラインにする &#40;SQL Server&#41;](../../take-an-availability-group-offline-sql-server.md)|  
    |セカンダリ|可用性グループからセカンダリ レプリカを削除する|[可用性グループからのセカンダリ レプリカの削除 &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)|  
  
-   リモート クラスターからローカル クラスターに切り替える前に、すべての同期コミット レプリカを SYNCHRONIZED にする必要があります。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   完全なドメイン名を指定することをお勧めします。 これは、短い名前のターゲット IP アドレスを検出するとき、ALTER SERVER CONFIGURATION は DNS 解決を使用するためです。 ある種の状況では、DNS の検索順序によっては、短い名前を使用すると混乱が生じる可能性があります。 たとえば、 `abc` ドメインのノード (`node1.abc.com`) で実行される次のコマンドを考慮してください。 目的のクラスターは、 `CLUS01` ドメインの `xyz` クラスターです (`clus01.xyz.com`)。 ただし、ローカル ドメイン ホストも、 `CLUS01` という名前のクラスターをホストしています (`clus01.abc.com`)。  
  
     ターゲット クラスターの短い名前である `CLUS01`を指定した場合、DNS の名前の解決で、違うクラスター ( `clus01.abc.com`) が返される可能性があります。 このような混乱を避けるには、次の例に示すように、ターゲット クラスターの完全な名前を指定します。  
  
    ```  
    ALTER SERVER CONFIGURATION SET HADR CLUSTER CONTEXT = 'clus01.xyz.com'  
    ```  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
  
-   **SQL Server ログイン (SQL Server login)**  
  
     CONTROL SERVER 権限が必要です。  
  
-   **SQL Server サービス アカウント**  
  
     サーバー インスタンスの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントは、以下を所有している必要があります。  
  
    -   宛先 WSFC クラスターを開く権限。  
  
    -   リモート WSFC 読み取り/書き込みアクセス。  
  
 
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **可用性レプリカの WSFC クラスター コンテキストを変更するには**  
  
1.  可能性グループのプライマリ レプリカまたはセカンダリ レプリカをホストするサーバー インスタンスに接続します。  
  
2.  次に示すように、 [ALTER SERVER CONFIGURATION](/sql/t-sql/statements/alter-server-configuration-transact-sql) ステートメントの SET HADR CLUSTER CONTEXT 句を使用します。  
  
     ALTER SERVER CONFIGURATION SET HADR CLUSTER CONTEXT **=** { **'*`windows_cluster`*'** | LOCAL }  
  
     パラメーターの説明  
  
     *windows_cluster*  
     WSFC クラスターのクラスター オブジェクト名 (CON)。 短い名前または完全なドメイン名を指定できます。 完全なドメイン名を指定することをお勧めします。 詳細については、このトピックの「 [推奨事項](#Recommendations)」を参照してください。  
  
     LOCAL  
     ローカル WSFC クラスター。  
  
### <a name="examples"></a>使用例  
 次の例では、HADR クラスター コンテキストを別のクラスターに変更します。 変更先の WSFC クラスターである `clus01`を識別するため、この例では、完全なクラスター オブジェクト名である `clus01.xyz.com`を指定します。  
  
```  
ALTER SERVER CONFIGURATION SET HADR CLUSTER CONTEXT = 'clus01.xyz.com';  
```  
  
 次の例では、HADR クラスター コンテキストをローカル WSFC クラスターに変更します。  
  
```  
ALTER SERVER CONFIGURATION SET HADR CLUSTER CONTEXT = LOCAL;  
```  
  

  
##  <a name="FollowUp"></a> 補足情報:可用性レプリカのクラスター コンテキストの切り替え後  
 新しい HADR クラスター コンテキストは、サーバー インスタンスの再起動なしですぐに有効になります。 HADR クラスター コンテキスト設定は、サーバー インスタンスが再起動した場合でも変更されない永続的なインスタンス レベルの設定です。  
  
 次に示すように、 [sys.dm_hadr_cluster](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql) 動的管理ビューをクエリすることで、新しい HADR クラスター コンテキストを確認します。  
  
```  
SELECT cluster_name FROM sys.dm_hadr_cluster  
```  
  
 このクエリは、HADR クラスター コンテキストを設定するクラスターの名前を返します。  
  
 HADR クラスター コンテキストが新しいクラスターに切り替わるとき:  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンスによって現在ホストされている可用性レプリカのメタデータがクリーンアップされます。  
  
-   可用性レプリカに所属していたすべてのデータベースが、RESTORING 状態になります。  
  
 
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [可用性グループ リスナーの削除 &#40;SQL Server&#41;](remove-an-availability-group-listener-sql-server.md)  
  
-   [可用性グループをオフラインにする &#40;SQL Server&#41;](../../take-an-availability-group-offline-sql-server.md)  
  
-   [可用性グループへのセカンダリ レプリカの追加 &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [可用性グループからのセカンダリ レプリカの削除 &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [可用性グループへのセカンダリ データベースの参加 &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
 
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   [SQL Server 2012 技術記事](https://msdn.microsoft.com/library/bb418445\(SQL.10\).aspx)  
  
-   [SQL Server AlwaysOn チームのブログ:SQL Server AlwaysOn チームのオフィシャル ブログ](https://blogs.msdn.com/b/sqlalwayson/)  
  
  
  
## <a name="see-also"></a>関連項目  
 [AlwaysOn 可用性グループ (SQL Server)](always-on-availability-groups-sql-server.md) [Windows Server フェールオーバー クラスタ リング&#40;WSFC&#41;と SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)  
  
  
