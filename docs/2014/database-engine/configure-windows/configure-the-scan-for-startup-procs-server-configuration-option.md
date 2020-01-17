---
title: scan for startup procs サーバー構成オプションの構成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- scan for startup procs option
ms.assetid: 6bf9d252-e766-458d-9dcd-23d895f032a2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a1af9aea2b4088c2a8d3753fd55feaa0f43ae6ea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62811394"
---
# <a name="configure-the-scan-for-startup-procs-server-configuration-option"></a>scan for startup procs サーバー構成オプションの構成
  このトピックでは、 **で** または [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] scan for startup procs [!INCLUDE[tsql](../../includes/tsql-md.md)]サーバー構成オプションを構成する方法について説明します。 **scan for startup procs** オプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 起動時のストアド プロシージャの自動実行をスキャンする場合に使用します。 このオプションを 1 に設定すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって、サーバーで定義されているすべての自動実行ストアド プロシージャがスキャンされ、実行されます。 **scan for startup procs** の既定値は 0 です。この値を設定した場合、スキャンは行われません。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [推奨事項](#Recommendations)  
  
     [Security](#Security)  
  
-   **以下を使用して scan for startup procs オプションを構成するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **補足情報:** [scan for startup procs オプションを構成した後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   このオプションは詳細設定オプションであるため、熟練したデータベース管理者または認定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術者だけが変更するようにしてください。  
  
-   このオプションの値は **sp_configure**を使用して設定できますが、ストアド プロシージャを自動的に実行するかどうかを設定する **sp_procoption**を使用すれば、値が自動的に設定されます。 **sp_procoption** を使用して、最初のストアド プロシージャを autoproc として設定すると、このオプションの値は自動的に 1 に設定されます。 **sp_procoption** を使用して、最後のストアド プロシージャを autoproc として設定解除すると、このオプションの値は自動的に 0 に設定されます。 **sp_procoption** を使用して autoprocs として設定またはその設定を解除し、ストアド プロシージャを削除する前に必ず autoprocs の設定を解除すれば、このオプションを手動で設定する必要がなくなります。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 パラメーターなしで、または最初のパラメーターだけを指定して **sp_configure** を実行する権限は、既定ですべてのユーザーに付与されます。 両方のパラメーターを指定して **sp_configure** を実行し構成オプションを変更したり RECONFIGURE ステートメントを実行したりするには、ALTER SETTINGS サーバーレベル権限がユーザーに付与されている必要があります。 ALTER SETTINGS 権限は、 **sysadmin** 固定サーバー ロールと **serveradmin** 固定サーバー ロールでは暗黙のうちに付与されています。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-configure-the-scan-for-startup-procs-option"></a>[スタートアップ プロシージャのスキャン] オプションを構成するには  
  
1.  オブジェクト エクスプローラーで、サーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[詳細設定]** ノードをクリックします。  
  
3.  **[その他]** で、 **[スタートアップ プロシージャのスキャン]** オプションのドロップダウン リストから値を選択して、[True] または [False] を指定します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-configure-the-scan-for-startup-procs-option"></a>[スタートアップ プロシージャのスキャン] オプションを構成するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) を使用して、 `scan for startup procs` オプションの値を `1`に設定する方法を示します。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'scan for startup procs', 1 ;  
GO  
RECONFIGURE  
GO  
  
```  
  
##  <a name="FollowUp"></a>補足情報: scan for startup procs オプションを構成した後  
 設定を有効にするには、サーバーを再起動する必要があります。  
  
## <a name="see-also"></a>関連項目  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [sp_procoption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-procoption-transact-sql)  
  
  
