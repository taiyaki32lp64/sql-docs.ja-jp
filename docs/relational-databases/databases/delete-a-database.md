---
title: データベースの削除 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- database removal [SQL Server], SQL Server Management Studio
- removing databases
- deleting databases
- dropping databases
- databases [SQL Server], dropping
- database removal [SQL Server]
ms.assetid: 1fd8c0f5-03e1-449a-af45-b8cacb479d9c
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 87ca7ef24d34a6f39255a92fcabaa2dab53cfa26
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006206"
---
# <a name="delete-a-database"></a>データベースの削除
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、ユーザー定義のデータベースを削除する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [前提条件](#Prerequisites)  
  
     [推奨事項](#Recommendations)  
  
     [セキュリティ](#Security)  
  
-   **以下を使用してデータベースを削除するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **補足情報:** [データベースを削除した後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   システム データベースは削除できません。  
  
###  <a name="Prerequisites"></a> 前提条件  
  
-   データベース上に存在するデータベース スナップショットをすべて削除します。 詳細については、「[データベース スナップショットの削除&#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)」を参照してください。  
  
-   データベースがログ配布に関係している場合は、ログ配布を削除します。  
  
-   データベースをトランザクション レプリケーション用にパブリッシュしている場合、またはマージ レプリケーションにパブリッシュしたりサブスクライブしている場合は、レプリケーションをデータベースから削除します。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   データベースの完全バックアップを行うことを検討します。 削除したデータベースの再作成は、バックアップを復元することによってのみ可能です。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 DROP DATABASE を実行するには、少なくともユーザーがデータベースで CONTROL 権限を持っている必要があります。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-delete-a-database"></a>データベースを削除するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、削除するデータベースを右クリックして、 **[削除]** をクリックします。  
  
3.  適切なデータベースが選択されていることを確認して、 **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-delete-a-database"></a>データベースを削除するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 `Sales` データベースと `NewSales` データベースを削除します。  
  
```sql  
USE master ;  
GO  
DROP DATABASE Sales, NewSales ;  
GO  
```  
  
##  <a name="FollowUp"></a>補足情報: データベースを削除した後  
 **master** データベースをバックアップします。 **master** データベースを復元する必要がある場合、 **master** データベースが最後にバックアップされてから削除されたデータベースがあると、システム カタログ ビュー内にそのデータベースの参照が残っているので、エラー メッセージが表示されることがあります。  
  
## <a name="see-also"></a>参照  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
  
