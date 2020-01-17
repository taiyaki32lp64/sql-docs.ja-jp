---
title: cursor threshold サーバー構成オプションの構成 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- cursor threshold option
ms.assetid: 189f2067-c6c4-48bd-9bd9-65f6b2021c12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a710ef8474ea0ce67d0b549febb3a9dd40aa36e0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62811378"
---
# <a name="configure-the-cursor-threshold-server-configuration-option"></a>cursor threshold サーバー構成オプションの構成
  このトピックでは、 **で** または [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] cursor threshold [!INCLUDE[tsql](../../includes/tsql-md.md)]サーバー構成オプションを構成する方法について説明します。 **cursor threshold** オプションは、カーソル キーセットが非同期に生成されるカーソル セット内の行数を指定します。 カーソルが結果セットのキーセットを生成するとき、その結果セットに返される行数をクエリ オプティマイザーが予測します。 返される行数がこのしきい値を超えていると予測された場合、カーソルは非同期に生成されます。これにより、ユーザーはカーソルの作成が続行されている間に行を取り出すことができます。 返される行数がこのしきい値以下と予測された場合、カーソルは同期をとって生成され、すべての行が返されるまでクエリが待機します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [推奨事項](#Recommendations)  
  
     [Security](#Security)  
  
-   **以下を使用して cursor threshold オプションを構成するには**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **補足情報:** [cursor threshold オプションを構成した後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、キーセット ドリブン カーソルまたは静的 [!INCLUDE[tsql](../../includes/tsql-md.md)] カーソルの非同期な作成はサポートされません。 [!INCLUDE[tsql](../../includes/tsql-md.md)] カーソル操作はバッチで行われます。したがって、 [!INCLUDE[tsql](../../includes/tsql-md.md)] カーソルを非同期に生成する必要はありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 各カーソル操作におけるクライアントのラウンド トリップのため、待機時間が少ない OPEN が問題になるような非同期キーセット ドリブン カーソルまたは静的 API (アプリケーション プログラミング インターフェイス) サーバー カーソルは、 で引き続きサポートされます。  
  
-   キーセットの行数を予測するクエリ オプティマイザーの精度は、カーソル内の各テーブルの統計の新しさによって左右されます。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   このオプションは詳細設定オプションであるため、熟練したデータベース管理者または認定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術者だけが変更するようにしてください。  
  
-   **cursor threshold** を -1 に設定すると、すべてのキーセットが同期して生成されます。これはカーソル セットが小さい場合に役立ちます。 **cursor threshold** を 0 に設定すると、すべてのカーソル キーセットが非同期に生成されます。 それ以外の値を設定した場合、クエリ オプティマイザーによってカーソル セットの予測行数が比較され、 **cursor threshold**に設定した値を超えていれば、キーセットが非同期に生成されます。 小さな結果セットは同期をとって作成する方がよいので、 **cursor threshold** の値は小さくしすぎないでください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 パラメーターなしで、または最初のパラメーターだけを指定して **sp_configure** を実行する権限は、既定ですべてのユーザーに付与されます。 両方のパラメーターを指定して **sp_configure** を実行し構成オプションを変更したり RECONFIGURE ステートメントを実行したりするには、ALTER SETTINGS サーバーレベル権限がユーザーに付与されている必要があります。 ALTER SETTINGS 権限は、 **sysadmin** 固定サーバー ロールと **serveradmin** 固定サーバー ロールでは暗黙のうちに付与されています。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-configure-the-cursor-threshold-option"></a>cursor threshold オプションを設定するには  
  
1.  オブジェクト エクスプローラーで、サーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[詳細設定]** ノードをクリックします。  
  
3.  **[その他]** の **[カーソルのしきい値]** オプションを目的の値に変更します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-configure-the-cursor-threshold-option"></a>cursor threshold オプションを設定するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) を使用して `cursor threshold` オプションを `0` に設定して、カーソル キーセットを非同期に生成する方法を示します。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'cursor threshold', 0 ;  
GO  
RECONFIGURE  
GO  
  
```  
  
 詳細については、「 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)」を参照してください。  
  
##  <a name="FollowUp"></a>補足情報: cursor threshold オプションを構成した後  
 新しい設定は、サーバーを再起動しなくてもすぐに有効になります。  
  
## <a name="see-also"></a>参照  
 [@@CURSOR_ROWS &#40;Transact-SQL&#41;](/sql/t-sql/functions/cursor-rows-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql)  
  
  
