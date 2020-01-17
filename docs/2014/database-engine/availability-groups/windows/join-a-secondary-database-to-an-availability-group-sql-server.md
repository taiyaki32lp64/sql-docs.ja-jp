---
title: 可用性グループへのセカンダリ データベースの参加 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.joindbs.f1
helpviewer_keywords:
- secondary databases [SQL Server], in availability group
- secondary databases [SQL Server]
- Availability Groups [SQL Server], joining
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], databases
ms.assetid: fd7efe79-c1f9-497d-bfe7-b2a2b2321cf5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5de4600d4f4c3d52d1757218e1f2d9b32f554286
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797667"
---
# <a name="join-a-secondary-database-to-an-availability-group-sql-server"></a>可用性グループへのセカンダリ データベースの参加 (SQL Server)
  このトピックでは、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]で、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、または PowerShell を使用して、AlwaysOn 可用性グループにセカンダリ データベースを参加させる方法について説明します。 セカンダリ レプリカのセカンダリ データベースを準備したら、できるだけ早くそのデータベースを可用性グループに参加させる必要があります。 これによって、対応するプライマリ データベースからセカンダリ データベースへのデータの移動が開始されます。  
  
-   **作業を開始する準備:**  
  
     [前提条件](#Prerequisites)  
  
     [セキュリティ](#Security)  
  
-   **以下を使用してセカンダリ データベースを準備するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
> [!NOTE]  
>  セカンダリデータベースがグループに参加した後の動作については、「 [ &#40;AlwaysOn 可用性グループ&#41;SQL Server の概要](overview-of-always-on-availability-groups-sql-server.md)」を参照してください。  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Prerequisites"></a> の前提条件  
  
-   セカンダリ レプリカをホストするサーバー インスタンスに接続されている必要があります。  
  
-   セカンダリ レプリカがあらかじめ可用性グループに参加している必要があります。 詳細については、「 [可用性グループへのセカンダリ レプリカの参加 &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)」を参照してください。  
  
-   セカンダリ データベースが最近準備されたものである必要があります。 詳細については、「[可用性グループに対するセカンダリ データベースの手動準備 &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> アクセス許可  
 可用性グループの ALTER AVAILABILITY GROUP 権限、CONTROL AVAILABILITY GROUP 権限、ALTER ANY AVAILABILITY GROUP 権限、または CONTROL SERVER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **セカンダリ データベースを可用性グループに参加させるには**  
  
1.  オブジェクト エクスプローラーで、セカンダリ レプリカをホストするサーバー インスタンスに接続し、サーバー ツリーを展開します。  
  
2.  **[AlwaysOn 高可用性]** ノードと **[可用性グループ]** ノードを展開します。  
  
3.  変更する可用性グループを展開し、 **[可用性データベース]** ノードを展開します。  
  
4.  データベースを右クリックし、 **[可用性グループへの参加]** をクリックします。  
  
5.  これにより、 **[可用性グループへのデータベースの参加]** ダイアログ ボックスが開きます。 タイトル バーに表示される可用性グループ名と、グリッドに表示されるデータベースの名前を確認し、 **[OK]** をクリックするか、 **[キャンセル]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **セカンダリ データベースを可用性グループに参加させるには**  
  
1.  セカンダリ レプリカをホストするサーバー インスタンスに接続します。  
  
2.  [ALTER DATABASE ステートメントの SET HADR 句](/sql/t-sql/statements/alter-database-transact-sql-set-hadr) を使用します。次にその例を示します。  
  
     ALTER DATABASE *database_name* SET HADR AVAILABILITY GROUP = *group_name*  
  
     ここで、 *database_name* は参加させるデータベースの名前で、 *group_name* は可用性グループの名前です。  
  
     次の例では、セカンダリ データベース `Db1`を、 `MyAG` 可用性グループのローカル セカンダリ レプリカに参加させます。  
  
    ```sql
    ALTER DATABASE Db1 SET HADR AVAILABILITY GROUP = MyAG;  
    ```  
  
    > [!NOTE]  
    >  コンテキストで使用するこの [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを確認するには、「[可用性グループの作成 &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md)」を参照してください。  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
 **セカンダリ データベースを可用性グループに参加させるには**  
  
1.  ディレクトリ変更コマンド (`cd`) を使用して、セカンダリ レプリカをホストするサーバー インスタンスに移動します。  
  
2.  `Add-SqlAvailabilityDatabase` コマンドレットを使用して、セカンダリ データベース (複数可) を可用性グループに参加させます。  
  
     たとえば、次のコマンドでは、セカンダリ レプリカをホストするいずれかのサーバー インスタンスで可用性グループ `Db1`にセカンダリ データベース `MyAG` を参加させます。  
  
    ```powershell
    Add-SqlAvailabilityDatabase -Path SQLSERVER:\SQL\SecondaryServer\InstanceName\AvailabilityGroups\MyAG -Database "Db1"  
    ```  
  
    > [!NOTE]  
    >  コマンドレットの構文を表示するには、`Get-Help` PowerShell 環境で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)」を参照してください。  
  
 **SQL Server PowerShell プロバイダーを設定して使用するには**  
  
-   [SQL Server PowerShell プロバイダー](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [可用性グループへのセカンダリ レプリカの参加 &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [可用性グループに対するセカンダリ データベースの手動準備 &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql)   
 [AlwaysOn 可用性グループ&#40;SQL Server&#41;の概要](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループ構成&#40;SQL Server&#41;削除された問題のトラブルシューティング](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
