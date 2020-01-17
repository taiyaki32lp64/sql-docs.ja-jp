---
title: テーブルからの列の削除 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], deleting
- removing columns
- deleting columns
- dropping columns
ms.assetid: 0d8f6e4f-bc71-4fa3-8615-74249c8e072d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 718aeca12c90435b68fd6cedde150dfbdeb3c063
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62761655"
---
# <a name="delete-columns-from-a-table"></a>テーブルからの列の削除
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用してテーブル列を削除する方法について説明します。  
  
> [!CAUTION]  
>  テーブルから列を削除すると、列および列に含まれているすべてのデータがデータベースから削除されます。 このアクションを元に戻すことはできません。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **テーブルから列を削除する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 CHECK 制約がある列を削除することはできません。 最初に制約を削除する必要があります。  
  
 テーブル デザイナーを使用する場合を除き、PRIMARY KEY 制約、FOREIGN KEY 制約、またはその他の依存関係がある列を削除することはできません。 オブジェクト エクスプローラーまたは [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用する場合、最初に列のすべての依存関係を削除する必要があります。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 テーブルに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-delete-columns-by-using-object-explorer"></a>オブジェクト エクスプローラーを使用して列を削除するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  **オブジェクト エクスプローラー**で、列を削除するテーブルを右クリックし、 **[削除]** をクリックします。  
  
3.  **[オブジェクトの削除]** ダイアログ ボックスで **[OK]** をクリックします。  
  
 列に制約またはその他の依存関係が含まれている場合は、 **[オブジェクトの削除]** ダイアログ ボックスにエラー メッセージが表示されます。 参照制約を削除することによって、エラーを解決します。  
  
#### <a name="to-delete-columns-by-using-table-designer"></a>テーブル デザイナーを使用して列を削除するには  
  
1.  **オブジェクト エクスプローラー**で、列を削除するテーブルを右クリックし、 **[デザイン]** をクリックします。  
  
2.  削除する列を右クリックし、ショートカット メニューの **[列の削除]** をクリックします。  
  
3.  列にリレーションシップ (FOREIGN KEY または PRIMARY KEY) が適用されている場合は、選択した列および列のリレーションシップの削除を確認するメッセージが表示されます。 **[はい]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-delete-columns"></a>列を削除するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE dbo.doc_exb DROP COLUMN column_b ;  
    ```  
  
 列に制約またはその他の依存関係が含まれている場合は、エラー メッセージが返されます。 参照制約を削除することによって、エラーを解決します。  
  
 例については、「[ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)」を参照してください。  
  
##  <a name="FollowUp"></a>  
