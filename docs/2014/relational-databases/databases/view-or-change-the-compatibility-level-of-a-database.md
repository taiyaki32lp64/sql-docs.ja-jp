---
title: データベースの互換性レベルの表示または変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- compatibility levels [SQL Server], viewing
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], changing
ms.assetid: 579867ec-57cb-4cb8-af35-9688c1e9e15d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ccc7b96f4275b09b90b8120813b93f860ec07b9a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62871060"
---
# <a name="view-or-change-the-compatibility-level-of-a-database"></a>データベースの互換性レベルの表示または変更
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、データベースの互換性レベルを表示または変更する方法について説明します。 データベースの互換性レベルを変更する前に、この変更がアプリケーションに及ぼす影響について理解しておく必要があります。 詳細については、「[ALTER DATABASE 互換性レベル &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)」を参照してください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **以下を使用してデータベースの互換性レベルを表示または変更するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 データベースに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-view-or-change-the-compatibility-level-of-a-database"></a>データベースの互換性レベルを表示または変更するには  
  
1.  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]の適切なインスタンスに接続した後、オブジェクト エクスプローラーでサーバー名をクリックします。  
  
2.  **[データベース]** を展開します。さらに、そのデータベースに応じて、ユーザー データベースを選択するか、または **[システム データベース]** を展開してシステム データベースを選択します。  
  
3.  データベースを右クリックし、 **[プロパティ]** をクリックします。  
  
     **[データベースのプロパティ]** ダイアログ ボックスが表示されます。  
  
4.  **[ページの選択]** ペインの **[オプション]** をクリックします。  
  
     **[互換性レベル]** ボックスの一覧に現在の互換性レベルが表示されます。  
  
5.  互換性レベルを変更するには、一覧から別のオプションを選択します。 選択できるのは、 **[SQL Server 2008 (100)]** 、 **[SQL Server 2012 (110)]** 、 **[SQL Server 2014 (120)]** のいずれかです。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-view-the-compatibility-level-of-a-database"></a>データベースの互換性レベルを表示するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースの互換性レベルを返します。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT compatibility_level  
FROM sys.databases WHERE name = 'AdventureWorks2012';  
GO  
  
```  
  
#### <a name="to-change-the-compatibility-level-of-a-database"></a>データベースの互換性レベルを変更するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例の互換性レベルを変更、[!INCLUDE[ssSampleDBobject](../../includes/sssql14-md.md)]します。  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET COMPATIBILITY_LEVEL = 120;  
GO  
```  
  
  
