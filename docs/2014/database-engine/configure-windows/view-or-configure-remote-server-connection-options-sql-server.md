---
title: リモート サーバー接続オプションの表示または構成 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- remote servers [SQL Server], connection options
- servers [SQL Server], remote
- connections [SQL Server], remote servers
ms.assetid: 356d3e6b-8514-4bd2-a683-9de147949b2b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5dfc0aa145f106fc57c25a6249b928ee27ab4b87
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62757202"
---
# <a name="view-or-configure-remote-server-connection-options-sql-server"></a>リモート サーバー接続オプションの表示または構成 (SQL Server)
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]でサーバー レベルのリモート サーバー接続オプションを表示または構成する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **リモート サーバー接続オプションを構成する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **補足情報:** [リモート サーバー接続オプションを構成した後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 **sp_serveroption** を実行するには、サーバーに対する ALTER ANY LINKED SERVER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-view-or-configure-remote-server-connection-options"></a>リモート サーバー接続オプションを表示または構成するには  
  
1.  オブジェクト エクスプローラーでサーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[サーバーのプロパティ - \<***server_name***>]** ダイアログ ボックスで、 **[接続]** をクリックします。  
  
3.  **[接続]** ページで、 **[リモート サーバー接続]** の設定を確認し、必要に応じて変更します。  
  
4.  リモート サーバー ペアのもう一方のサーバーに対して、手順 1. ～ 3. を繰り返します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-view-remote-server-connection-options"></a>リモート サーバー接続オプションを表示するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sp_helpserver](/sql/relational-databases/system-stored-procedures/sp-helpserver-transact-sql) を使用して、すべてのリモート サーバーに関する情報を返します。  
  
```sql  
USE master;  
GO  
EXEC sp_helpserver ;  
```  
  
#### <a name="to-configure-remote-server-connection-options"></a>リモート サーバー接続オプションを構成するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sp_serveroption](/sql/relational-databases/system-stored-procedures/sp-serveroption-transact-sql) を使用して、リモート サーバーを構成する方法を示します。 この例では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の別のインスタンスに対応するリモート サーバー `SEATTLE3`を、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のローカル インスタンスと互換性のある照合順序になるように構成します。  
  
```sql  
USE master;  
EXEC sp_serveroption 'SEATTLE3', 'collation compatible', 'true';  
```  
  
##  <a name="FollowUp"></a>補足情報: リモート サーバー接続オプションを構成した後  
 設定を有効にするには、リモート サーバーを停止し、再起動する必要があります。  
  
## <a name="see-also"></a>関連項目  
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [リモート サーバー](remote-servers.md)   
 [リンク サーバー &#40;データベース エンジン&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-linkedservers-transact-sql)   
 [sp_helpserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpserver-transact-sql)   
 [sp_serveroption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-serveroption-transact-sql)  
  
  
