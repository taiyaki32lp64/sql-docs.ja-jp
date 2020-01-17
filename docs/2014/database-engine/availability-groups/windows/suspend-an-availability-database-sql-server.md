---
title: 可用性データベースの中断 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.suspenddatamove.f1
helpviewer_keywords:
- secondary databases [SQL Server], in availability group
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], suspending a database
- Availability Groups [SQL Server], databases
ms.assetid: 86858982-6af1-4e80-9a93-87451f0d7ee9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7c428d9141acfaca3e8ec7876e62b733c30ec161
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797962"
---
# <a name="suspend-an-availability-database-sql-server"></a>可用性データベースの中断 (SQL Server)
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]、または PowerShell を使用して、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]の可用性データベースを中断できます。 中断コマンドは、中断または再開するデータベースをホストするサーバー インスタンス上で実行する必要があります。  
  
 中断コマンドの効果は、次のように、中断するのがセカンダリ データベースかプライマリ データベースかによって異なります。  
  
|中断されたデータベース|中断コマンドの影響|  
|------------------------|-------------------------------|  
|[セカンダリ データベース]|ローカルのセカンダリ データベースのみが中断され、同期の状態は NOT SYNCHRONIZING になります。 他のセカンダリ データベースは影響を受けません。 中断されたデータベースはデータ (ログ レコード) を受信および適用しなくなり、プライマリ データベースと同期されなくなります。 読み取り可能なセカンダリ上の既存の接続は、引き続き使用できます。 読み取り可能なセカンダリ上で中断されたデータベースに対する新しい接続は、データ移動が再開されるまでは許可されません。<br /><br /> プライマリ データベースは使用可能です。 対応する各セカンダリ データベースを中断した場合、プライマリ データベースは公開された状態で実行されます。<br /><br /> **\*\* 重要 \*\*** セカンダリ データベースが中断されている間、対応するプライマリ データベースの送信キューが未送信トランザクション ログ レコードに蓄積されます。 セカンダリ レプリカへの接続では、データ移動が中断されたときに使用可能であったデータが返されます。|  
|プライマリ データベース|プライマリ データベースは、接続されているすべてのセカンダリ データベースへのデータ移動を停止します。 プライマリ データベースは、公開モードで実行を継続します。 クライアントはプライマリ データベースを使用でき、読み取り可能なセカンダリ上の既存の接続は引き続き使用でき、新しい接続も確立できます。|  
  
> [!NOTE]  
>  AlwaysOn セカンダリ データベースの中断が、プライマリ データベースの可用性に直接影響することはありません。 ただし、セカンダリ データベースを中断すると、プライマリ データベースの冗長性とフェールオーバー機能に影響する場合があります。 ミラーリングの場合はこれと異なり、ミラーリングの状態はミラー データベースでもプリンシパル データベースでも中断になります。 AlwaysOn プライマリ データベースを中断すると、対応するすべてのセカンダリ データベースでデータ移動が中断され、そのデータベースの冗長性とフェールオーバー機能はプライマリ データベースが再開されるまで停止されます。  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [前提条件](#Prerequisites)  
  
     [推奨事項](#Recommendations)  
  
     [セキュリティ](#Security)  
  
-   **データベースを中断するために使用するもの:**  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **補足情報:** [トランザクション ログがいっぱいになった状態の回避](#FollowUp)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 SUSPEND コマンドは、対象のデータベースをホストするレプリカによって受け付けられるとすぐに戻りますが、実際にはデータベースの中断が非同期に行われます。  
  
###  <a name="Prerequisites"></a> の前提条件  
 中断するデータベースをホストするサーバー インスタンスに接続している必要があります。 プライマリ データベースとそれに対応するセカンダリ データベースを中断するには、プライマリ レプリカをホストするサーバー インスタンスに接続します。 プライマリ データベースを使用可能な状態で維持したままセカンダリ データベースを中断するには、セカンダリ レプリカに接続します。  
  
###  <a name="Recommendations"></a> 推奨事項  
 ボトルネックの発生中、1 つ以上のセカンダリ データベースを短時間中断すると、プライマリ レプリカのパフォーマンスが一時的に高まる効果が見込めます。 セカンダリ データベースが中断している間、対応するプライマリ データベースのトランザクション ログを切り捨てることはできません。 これにより、プライマリ データベースでログ レコードが蓄積されます。 そのため、中断したセカンダリ データベースをすぐに再開または削除することをお勧めします。 詳細については、このトピックの「 [補足情報: トランザクション ログがいっぱいになった状態の回避](#FollowUp)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> アクセス許可  
 データベースに対する ALTER 権限が必要です。  
  
 可用性グループの ALTER AVAILABILITY GROUP 権限、CONTROL AVAILABILITY GROUP 権限、ALTER ANY AVAILABILITY GROUP 権限、または CONTROL SERVER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **データベースを中断するには**  
  
1.  オブジェクト エクスプローラーで、データベースを中断する可用性レプリカをホストするサーバー インスタンスに接続し、サーバー ツリーを展開します。 詳細については、このトピックの「 [前提条件](#Prerequisites)」をご覧ください。  
  
2.  **[AlwaysOn 高可用性]** ノードと **[可用性グループ]** ノードを展開します。  
  
3.  可用性グループを展開します。  
  
4.  **[可用性データベース]** ノードを展開し、データベースを右クリックして、 **[データ移動の中断]** をクリックします。  
  
5.  **[データ移動の中断]** ダイアログ ボックスで、 **[OK]** をクリックします。  
  
     オブジェクト エクスプローラーで、データベース アイコンに中断インジケーターが表示され、データベースが中断されていることが示されます。  
  
> [!NOTE]  
>  このレプリカの場所で他のデータベースを中断するには、データベースごとに手順 4. と手順 5. を繰り返します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **データベースを中断するには**  
  
1.  中断するデータベースのレプリカをホストするサーバー インスタンスに接続します。 詳細については、このトピックの「 [前提条件](#Prerequisites)」をご覧ください。  
  
2.  次の [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-hadr)ステートメントを使用して、データベースを中断します。  
  
     ALTER DATABASE *database_name* SET HADR SUSPEND  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
 **データベースを中断するには**  
  
1.  ディレクトリ (`cd`) を、中断するデータベースのレプリカをホストするサーバー インスタンスに変更します。 詳細については、このトピックの「 [前提条件](#Prerequisites)」をご覧ください。  
  
2.  `Suspend-SqlAvailabilityDatabase` コマンドレットを使用して可用性グループを中断します。  
  
     たとえば、次のコマンドでは、 `MyDb3` という名前のサーバー インスタンス上の可用性グループ `MyAg` に含まれている可用性データベース `Computer\Instance`のデータの同期を中断します。  
  
    ```powershell
    Suspend-SqlAvailabilityDatabase -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\Databases\MyDb3  
    ```  
  
    > [!NOTE]  
    >  コマンドレットの構文を表示するには、`Get-Help` PowerShell 環境で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)」を参照してください。  
  
 **SQL Server PowerShell プロバイダーを設定して使用するには**  
  
-   [SQL Server PowerShell プロバイダー](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a> Follow Up: Avoiding a Full Transaction Log  
 通常、データベースで自動チェックポイントが実行されている場合は、次のログ バックアップの後、そのチェックポイントまでトランザクション ログが切り捨てられます。 ただし、セカンダリ データベースを中断している間、現在のすべてのログ レコードは、プライマリ データベースでアクティブのままになります。 最大サイズに到達したか、サーバー インスタンスの領域が不足して、トランザクション ログがいっぱいになると、データベースではそれ以上の更新を実行できません。  
  
 この問題を回避するには、次のいずれかの操作を実行する必要があります。  
  
-   プライマリ データベースのログ領域を追加します。  
  
-   ログがいっぱいになる前に、セカンダリ データベースを再開します。 詳細については、このトピックの「 [可用性データベースの再開 &#40;SQL Server&#41;](resume-an-availability-database-sql-server.md)の可用性データベースを中断できます。  
  
-   セカンダリ データベースを削除します。 詳細については、「[可用性グループからのセカンダリ データベースの削除 &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)」をご覧ください。  
  
 **満杯になったトランザクション ログのトラブルシューティング**  
  
-   [満杯になったトランザクション ログのトラブルシューティング &#40;SQL Server エラー 9002&#41;](../../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [可用性データベースの再開 &#40;SQL Server&#41;](resume-an-availability-database-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループ&#40;SQL Server&#41;の概要](overview-of-always-on-availability-groups-sql-server.md)   
 [可用性データベースの再開 &#40;SQL Server&#41;](resume-an-availability-database-sql-server.md)  
