---
title: ビューの削除 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a0b11b2d6fa897b99276f75fb74e2c41e25db904
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68123468"
---
# <a name="delete-views"></a>ビューの削除
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、次のいずれかを使用してビューを削除できます: [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [セキュリティ](#Security)  
  
-   **以下を使用してデータベースからビューを削除するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
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
    >  **[オブジェクトの削除]** ダイアログ ボックスの **[依存関係の表示]** をクリックして _[view\_name_**の依存関係]** ダイアログ ボックスを開きます。 ビューに依存するすべてのオブジェクトと、ビューが依存するすべてのオブジェクトが表示されます。  
  
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
  
 詳細については、「[DROP VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/drop-view-transact-sql.md)」を参照してください。  
  
  
