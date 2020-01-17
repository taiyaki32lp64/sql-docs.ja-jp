---
title: 可用性グループの削除 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.deleteag.f1
helpviewer_keywords:
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], dropping
ms.assetid: 4b7f7f62-43a3-49db-a72e-22d4d7c2ddbb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e4227b0af8453a40e9dd63b4aef170d52f8115b2
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782927"
---
# <a name="remove-an-availability-group-sql-server"></a>可用性グループの削除 (SQL Server)
  このトピックでは、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] で [!INCLUDE[tsql](../../../includes/tsql-md.md)]、[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、または PowerShell を使用して、AlwaysOn 可用性グループを削除する方法について説明します。 可用性グループを削除する際、可用性レプリカの 1 つをホストするサーバー インスタンスがオフラインだった場合は、再度オンラインになった時点でローカルの可用性レプリカが削除されます。 可用性グループを削除すると、関連付けられている可用性グループ リスナーもすべて削除されます。  
  
 必要であれば、可用性グループの削除は、その可用性グループに対する適切なセキュリティ資格情報が存在する任意の Windows Server フェールオーバー クラスタリング (WSFC) ノードから行うことができます。 そのため、可用性レプリカがまったく残っていなくても可用性グループを削除することができます。  
  
> [!IMPORTANT]  
>  可能であれば、プライマリ レプリカをホストするサーバー インスタンスに接続しているときにのみ可用性グループを削除してください。 可用性グループをプライマリ レプリカから削除すると、元のプライマリ データベースで変更が許可されます (高可用性の保護なし)。 セカンダリ レプリカから可用性グループを削除すると、プライマリ レプリカは RESTORING 状態になり、変更はデータベースで許可されません。  
  
-   **作業を開始する準備:**  
  
     [制限事項と推奨事項](#Restrictions)  
  
     [セキュリティ](#Security)  
  
-   **以下を使用して可用性グループを削除するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [関連コンテンツ](#RelatedContent)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と推奨事項  
  
-   オンライン状態の可用性グループをセカンダリ レプリカから削除すると、プライマリ レプリカは RESTORING 状態になります。 したがって、可能であれば、プライマリ レプリカをホストするサーバー インスタンスから可用性グループのみを削除してください。  
  
-   WSFC フェールオーバー クラスターから削除されたコンピューターで可用性グループを削除した場合、可用性グループはローカルからのみ削除されます。  
  
-   Windows Server フェールオーバー クラスタリング (WSFC) クラスターにクォーラムがない場合は、可用性グループを削除しないでください。 クラスターのクォーラムがないときに可用性グループを削除すると、クラスターに格納されているメタデータ可用性グループは削除されません。 クラスターのクォーラムが再取得された後、WSFC クラスターから削除するために、可用性グループをもう一度削除する必要があります。  
  
-   セカンダリ レプリカについては、DROP AVAILABILITY GROUP は緊急の目的だけに使用してください。 理由は、可用性グループを削除すると可用性グループがオフラインになるためです。 セカンダリ レプリカから可用性グループを削除した場合、プライマリ レプリカは、OFFLINE 状態がクォーラム損失、強制フェールオーバー、または DROP AVAILABILITY GROUP コマンドのどの原因で発生したのかを特定できません。 スプリット ブレイン状況の発生を防ぐために、プライマリ レプリカは RESTORING 状態に遷移します。 詳細については、「 [動作方法: DROP AVAILABILITY GROUP の動作](https://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) 」(CSS SQL Server エンジニアのブログ) を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> アクセス許可  
 可用性グループの ALTER AVAILABILITY GROUP 権限、CONTROL AVAILABILITY GROUP 権限、ALTER ANY AVAILABILITY GROUP 権限、または CONTROL SERVER 権限が必要です。 ローカル サーバー インスタンスによってホストされていない可用性グループを削除するには、その可用性グループ上の CONTROL SERVER 権限または CONTROL 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **可用性グループを削除するには**  
  
1.  オブジェクト エクスプローラーで、プライマリ レプリカをホストするサーバー インスタンスに接続するか (可能な場合)、可用性グループの適切なセキュリティ資格情報を持つ WSFC ノード上の AlwaysOn 可用性グループに対して有効な別のサーバー インスタンスに接続します。 サーバー ツリーを展開します。  
  
2.  **[AlwaysOn 高可用性]** ノードと **[可用性グループ]** ノードを展開します。  
  
3.  削除する可用性グループが複数であるか単独であるかによって、次のように実行する手順が異なります。  
  
    -   (プライマリ レプリカが接続先のサーバー インスタンスにある) 複数の可用性グループを削除するには、 **[オブジェクト エクスプローラーの詳細]** ペインを使用して、削除するすべての可用性グループを表示し、選択します。 詳細については、「[[オブジェクト エクスプローラーの詳細] を使用した可用性グループの監視 &#40;SQL Server Management Studio&#41;](use-object-explorer-details-to-monitor-availability-groups.md) を参照してください。  
  
    -   単独の可用性グループを削除するには、 **[オブジェクト エクスプローラー]** ペインまたは **[オブジェクト エクスプローラーの詳細]** ペインで目的の可用性グループを選択します。  
  
4.  選択した 1 つまたは複数の可用性グループを右クリックし、 **[削除]** を選択します。  
  
5.  **[可用性グループの削除]** ダイアログ ボックスで、表示された可用性グループを削除するために、 **[OK]** をクリックします。 表示された可用性グループをすべて削除しない場合は、 **[キャンセル]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **可用性グループを削除するには**  
  
1.  プライマリ レプリカをホストするサーバー インスタンスに接続するか (可能な場合)、可用性グループの適切なセキュリティ資格情報を持つ WSFC ノード上の AlwaysOn 可用性グループに対して有効な別のサーバー インスタンスに接続します。  
  
2.  [DROP AVAILABILITY GROUP](/sql/t-sql/statements/drop-availability-group-transact-sql) ステートメントを使用します。次にその例を示します。  
  
     DROP AVAILABILITY GROUP *group_name*  
  
     *group_name* には、削除する可用性グループの名前を指定します。  
  
     次の例では、 `MyAG` 可用性グループを削除します。  
  
    ```sql
    DROP AVAILABILITY GROUP MyAG;  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
 **可用性グループを削除するには**  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell プロバイダーで次の操作を行います。  
  
1.  プライマリ レプリカをホストするサーバー インスタンスにディレクトリを変更 (`cd`) するか (可能な場合)、可用性グループの適切なセキュリティ資格情報を持つ WSFC ノード上の AlwaysOn 可用性グループに対して有効な別のサーバー インスタンスに接続します。  
  
2.  **Remove-SqlAvailabilityGroup** コマンドレットを使用します。  
  
     たとえば、次のコマンドでは、 `MyAg`という名前の可用性グループが削除されます。 このコマンドは、可用性グループの可用性レプリカをホストするサーバー インスタンスで実行できます。  
  
    ```powershell
    Remove-SqlAvailabilityGroup -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg  
    ```  
  
    > [!NOTE]  
    >  コマンドレットの構文を表示するには、`Get-Help` PowerShell 環境で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)」を参照してください。  
  
 **SQL Server PowerShell プロバイダーを設定して使用するには**  
  
-   [SQL Server PowerShell プロバイダー](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   [動作方法: DROP AVAILABILITY GROUP の動作](https://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (CSS SQL Server エンジニアのブログ)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループ&#40;SQL Server&#41;の概要](overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループの作成と構成 &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)  
