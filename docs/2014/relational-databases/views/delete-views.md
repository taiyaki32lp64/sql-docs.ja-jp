---
title: ビューの削除 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- dropping views
- deleting views
- views [SQL Server], deleting
- removing views
ms.assetid: 6823c7f8-06ca-4bda-8482-7092f03d52a0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b7e727451fb0f9dc7a3d0726a2cb0fa2d6adf997
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68196405"
---
# <a name="delete-views"></a>ビューの削除
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、次のいずれかを使用してビューを削除できます: [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  

  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   ビューを削除すると、ビューの定義やビューに関するその他の情報がシステム カタログから削除されます。 ビューに対する権限もすべて削除されます。  
  
-   `DROP TABLE` を使用して削除されたテーブルのすべてのビューは、 `DROP VIEW`を使用して明示的に削除する必要があります。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 SCHEMA に対する ALTER 権限、または OBJECT に対する CONTROL 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-delete-a-view-from-a-database"></a>データベースからビューを削除するには  
  
1.  **オブジェクト エクスプローラー**で、削除するビューを含むデータベースを展開します。次に、 **[ビュー]** フォルダーを展開します。  
  
2.  削除するビューを右クリックし、 **[削除]** をクリックします。  
  
3.  **[オブジェクトの削除]** ダイアログ ボックスで **[OK]** をクリックします。  
  
    > [!IMPORTANT]  
    >  **[オブジェクトの削除]** ダイアログ ボックスの **[依存関係の表示]** をクリックして _[view_name_**の依存関係]** ダイアログ ボックスを開きます。 ビューに依存するすべてのオブジェクトと、ビューが依存するすべてのオブジェクトが表示されます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-delete-a-view-from-a-database"></a>データベースからビューを削除するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、ビューが既に存在する場合にのみ、指定されたビューを削除します。  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    IF OBJECT_ID ('HumanResources.EmployeeHireDate', 'V') IS NOT NULL  
    DROP VIEW HumanResources.EmployeeHireDate;  
    GO  
    ```  
  
 詳細については、「[DROP VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-view-transact-sql)」を参照してください。  
  
  
