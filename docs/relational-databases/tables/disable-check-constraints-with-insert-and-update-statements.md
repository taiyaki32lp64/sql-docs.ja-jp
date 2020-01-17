---
title: INSERT ステートメントまたは UPDATE ステートメントによる CHECK 制約の無効化 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- CHECK constraints, disabling
- constraints [SQL Server], disabling
- disabling constraints
- constraints [SQL Server], check
ms.assetid: c7287ad1-50d2-4e80-bc0c-b5570f7e5f69
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9a25909bfcfb6e8bbc228af03a608c416ab55bd3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016379"
---
# <a name="disable-check-constraints-with-insert-and-update-statements"></a>INSERT ステートメントまたは UPDATE ステートメントによる CHECK 制約の無効化
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して INSERT および UPDATE トランザクションの CHECK 制約を無効にできます。 CHECK 制約を無効にすると、今後列に行われる挿入または更新は、制約条件に対して検証されません。 新しいデータが既存の制約に違反することがわかっている場合、またはデータベース内の既存のデータのみに制約を適用する場合に、このオプションを使用します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [セキュリティ](#Security)  
  
-   **INSERT ステートメントおよび UPDATE ステートメントの実行中に CHECK 制約を無効にする方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 テーブルに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-disable-a-check-constraint-for-insert-and-update-statements"></a>INSERT ステートメントおよび UPDATE ステートメントの実行中に CHECK 制約を無効にするには  
  
1.  **オブジェクト エクスプローラー**で、制約が設定されているテーブルを展開し、 **[制約]** フォルダーを展開します。  
  
2.  制約を右クリックし、 **[変更]** をクリックします。  
  
3.  **テーブル デザイナー**の下にあるグリッドで、 **[INSERT および UPDATE に適用]** をクリックし、ドロップダウン メニューの **[いいえ]** をクリックします。  
  
4.  **[閉じる]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-disable-a-check-constraint-for-insert-and-update-statements"></a>INSERT ステートメントおよび UPDATE ステートメントの実行中に CHECK 制約を無効にするには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE Purchasing.PurchaseOrderHeader  
    NOCHECK CONSTRAINT CK_PurchaseOrderHeader_Freight;   
    GO  
    ```  
  
 詳細については、「[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)」を参照してください。  
  
###  <a name="TsqlExample"></a>  
