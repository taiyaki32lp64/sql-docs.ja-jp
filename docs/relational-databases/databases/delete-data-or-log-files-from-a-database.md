---
title: データまたはログ ファイルのデータベースからの削除 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], files
- deleting files
- removing files
- removing data
- data deletions [SQL Server]
- file deletion [SQL Server]
- deleting data
ms.assetid: 0db4018c-ce2c-4ba1-bb29-1e4f3791c925
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8cdc8f15cedb170ae6c5aeab35c8f92a979d30d6
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909056"
---
# <a name="delete-data-or-log-files-from-a-database"></a>データまたはログ ファイルのデータベースからの削除
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、データ ファイルまたはログ ファイルを削除する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [前提条件](#Prerequisites)  
  
     [セキュリティ](#Security)  
  
-   **以下を使用してデータ ファイルまたはログ ファイルをデータベースから削除するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Prerequisites"></a> 前提条件  
  
-   ファイルは削除する前に空にしておく必要があります。 詳細については、「 [ファイルの圧縮](../../relational-databases/databases/shrink-a-file.md)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 データベースに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-delete-data-or-log-files-from-a-database"></a>データ ファイルまたはログ ファイルをデータベースから削除するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、ファイルを削除するデータベースを右クリックして、 **[プロパティ]** をクリックします。  
  
3.  **[ファイル]** ページをクリックします。  
  
4.  **[データベース ファイル]** グリッドで、削除するファイルをクリックし、 **[削除]** をクリックします。  
  
5.  **[OK]** をクリックします。  

##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-delete-data-or-log-files-from-a-database"></a>データ ファイルまたはログ ファイルをデータベースから削除するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 次の例では、`test1dat4` ファイルを削除します。  
  
 [!code-sql[DatabaseDDL#AlterDatabase4](../../relational-databases/databases/codesnippet/tsql/delete-data-or-log-files_1.sql)]  
  
 詳細については、「[ALTER DATABASE の File および Filegroup オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データベースの圧縮](../../relational-databases/databases/shrink-a-database.md)   
 [データベースに対するデータ ファイルまたはログ ファイルの追加](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)  
  
  
