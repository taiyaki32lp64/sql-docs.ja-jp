---
title: インデックスの名前変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- renaming indexes
- index names [SQL Server]
- indexes [SQL Server], renaming
ms.assetid: d3d612a1-ea1b-4d99-85d2-0a2ad54f4b0e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 744e7a10c9c4dcd776d58b6234749f2be5aa1479
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63036231"
---
# <a name="rename-indexes"></a>インデックスの名前変更
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]のインデックスの名前を変更する方法について説明します。 インデックスの名前を変更すると、現在のインデックス名が指定した新しい名前に置き換えられます。 指定する名前は、テーブルやビュー内で一意になる必要があります。 たとえば、2 つのテーブルにそれぞれ **XPK_1**という名前のインデックスを含めることはできますが、同じテーブルに **XPK_1**という名前のインデックスを 2 つ含めることはできません。 無効になっている既存のインデックスと同じ名前のインデックスを作成することはできません。 インデックス名を変更しても、インデックスは再構築されません。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **以下を使用してインデックスの名前を変更するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 テーブルに PRIMARY KEY 制約または UNIQUE 制約を作成すると、制約と同じ名前のインデックスが自動的に作成されます。 インデックス名はテーブル内で一意になる必要があるので、そのテーブルに既存の PRIMARY KEY 制約または UNIQUE 制約と同じ名前のインデックスを作成したり、同じ名前を付けることはできません。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> アクセス許可  
 インデックスに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-rename-an-index-by-using-the-table-designer"></a>テーブル デザイナーを使用してインデックスの名前を変更するには  
  
1.  オブジェクト エクスプローラーで、インデックスの名前を変更するテーブルが格納されているデータベースをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[テーブル]** フォルダーを展開します。  
  
3.  インデックスの名前を変更するテーブルを右クリックし、 **[デザイン]** を選択します。  
  
4.  **[テーブル デザイナー]** メニューの **[インデックス/キー]** をクリックします。  
  
5.  **[選択された主/一意キーまたはインデックス]** ボックスで、名前の変更対象のインデックスを選択します。  
  
6.  グリッド内の **[名前]** をクリックし、テキスト ボックスに新しい名前を入力します。  
  
7.  **[閉じる]** をクリックします。  
  
8.  **ファイル** メニューの **テーブル名**_の保存_をクリックします。  
  
#### <a name="to-rename-an-index-by-using-object-explorer"></a>オブジェクト エクスプローラーを使用してインデックスの名前を変更するには  
  
1.  オブジェクト エクスプローラーで、インデックスの名前を変更するテーブルが格納されているデータベースをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[テーブル]** フォルダーを展開します。  
  
3.  プラス記号をクリックして、インデックスの名前を変更するテーブルを展開します。  
  
4.  プラス記号をクリックして **[インデックス]** フォルダーを展開します。  
  
5.  名前を変更するインデックスを右クリックし、 **[名前の変更]** をクリックします。  
  
6.  新しいインデックス名を入力して、Enter キーを押します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-rename-an-index"></a>インデックスの名前を変更するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    --Renames the IX_ProductVendor_VendorID index on the Purchasing.ProductVendor table to IX_VendorID.   
  
    EXEC sp_rename N'Purchasing.ProductVendor.IX_ProductVendor_VendorID', N'IX_VendorID', N'INDEX';   
    GO  
    ```  
  
 詳細については、「[sp_rename &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql)」を参照してください。  
  
  
