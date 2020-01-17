---
title: データベース スナップショットの表示 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], viewing
- displaying database snapshots
- viewing database snapshots
ms.assetid: 123f19b2-0850-4033-8507-59ebdfb368ee
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1b8648b9166ffa192ca21233ab6add38260a7dea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62871159"
---
# <a name="view-a-database-snapshot-sql-server"></a>データベース スナップショットの表示 (SQL Server)
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用して [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]データベース スナップショットを表示する方法について説明します。  
  
> [!NOTE]  
>  データベース スナップショットの作成、復元、削除には、 [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用する必要があります。  
  
 **このトピックの内容**  
  
-   **データベース スナップショットの確認に使用するツール:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **データベース スナップショットを確認するには**  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開します。  
  
3.  **[データベース スナップショット]** を展開し、表示するスナップショットを選択します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **データベース スナップショットを確認するには**  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスのデータベース スナップショットの一覧を表示するには、 **sys.databases** カタログ ビューの [source_database_id](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 列で NULL 以外の値に対してクエリを実行します。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [データベース スナップショットの作成 &#40;Transact-SQL&#41;](create-a-database-snapshot-transact-sql.md)  
  
-   [データベースをデータベース スナップショットに戻す](revert-a-database-to-a-database-snapshot.md)  
  
-   [データベース スナップショットの削除 &#40;Transact-SQL&#41;](drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>関連項目  
 [Database Snapshots &#40;SQL Server&#41;](database-snapshots-sql-server.md)  
  
  
