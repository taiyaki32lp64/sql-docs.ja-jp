---
title: default language サーバー構成オプションの構成 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- default language option
ms.assetid: c08c26d8-5a62-487e-a4ee-4c529e4f9287
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e0f9a295cb5c49b9a88d70187cd49527df5ba83b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62811677"
---
# <a name="configure-the-default-language-server-configuration-option"></a>default language サーバー構成オプションの構成
  このトピックでは、 **または** を使用して、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] default language [!INCLUDE[tsql](../../includes/tsql-md.md)]サーバー構成オプションを構成する方法について説明します。 **default language** は、新しく作成したすべてのログインで使用される既定の言語を指定するオプションです。 既定の言語を設定するには、目的の言語の **langid** 値を指定します。 **langid** 値は、 **sys.syslanguages** 互換性ビューをクエリすることによって取得できます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [推奨事項](#Recommendations)  
  
     [Security](#Security)  
  
-   **以下を使用して default language オプションを構成するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **補足情報:** [default language オプションを構成した後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   ログインの既定の言語は、CREATE LOGIN または ALTER LOGIN でオーバーライドできます。 セッションの既定の言語が、Open Database Connectivity (ODBC) API または OLE DB API でセッションごとにオーバーライドされない限り、そのセッションのログインの言語になります。 **default language** オプションには、 [sys.syslanguages](/sql/relational-databases/system-compatibility-views/sys-syslanguages-transact-sql) で定義されている言語 ID (0 ～ 32) しか設定できないことに注意してください。 包含データベースを使用している場合、既定の言語をデータベースに対して設定するには CREATE DATABASE または ALTER DATABASE を使用し、包含データベース ユーザーに対して設定するには CREATE USER または ALTER USER を使用します。 包含データベースにおける既定の言語を設定する際は、 **sys.syslanguages** に格納されている **langid**値、言語の名前、または言語の別名を指定できます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 パラメーターなしで、または最初のパラメーターだけを指定して **sp_configure** を実行する権限は、既定ですべてのユーザーに付与されます。 両方のパラメーターを指定して **sp_configure** を実行し構成オプションを変更したり RECONFIGURE ステートメントを実行したりするには、ALTER SETTINGS サーバーレベル権限がユーザーに付与されている必要があります。 ALTER SETTINGS 権限は、 **sysadmin** 固定サーバー ロールと **serveradmin** 固定サーバー ロールでは暗黙のうちに付与されています。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-configure-the-default-language-option"></a>default language オプションを構成するには  
  
1.  オブジェクト エクスプローラーで、サーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[その他のサーバーの設定]** ノードをクリックします。  
  
3.  **[ユーザーの既定の言語]** ボックスで、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がシステム メッセージの表示に使用する言語を選択します。  
  
     既定の言語は English (英語) です。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-configure-the-default-language-option"></a>default language オプションを構成するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) を使用して、 `default language` オプションをフランス語 (`2`) に設定する方法を示します。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'default language', 2 ;  
GO  
RECONFIGURE ;  
GO  
```  
  
 詳細については、「 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)」を参照してください。  
  
##  <a name="FollowUp"></a>補足情報: default language オプションを構成した後  
 新しい設定は、サーバーを再起動しなくてもすぐに有効になります。  
  
## <a name="see-also"></a>関連項目  
 [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)   
 [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)   
 [ALTER USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-user-transact-sql)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
