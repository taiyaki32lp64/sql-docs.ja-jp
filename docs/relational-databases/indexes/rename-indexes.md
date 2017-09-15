---
title: "インデックスの名前変更 | Microsoft Docs"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- renaming indexes
- index names [SQL Server]
- indexes [SQL Server], renaming
ms.assetid: d3d612a1-ea1b-4d99-85d2-0a2ad54f4b0e
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 59c77e43b02e26626c280f6325cdb67a11021db9
ms.contentlocale: ja-jp
ms.lasthandoff: 06/22/2017

---
# <a name="rename-indexes"></a>インデックスの名前変更
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]のインデックスの名前を変更する方法について説明します。 インデックスの名前を変更すると、現在のインデックス名が指定した新しい名前に置き換えられます。 指定する名前は、テーブルやビュー内で一意になる必要があります。 たとえば、2 つのテーブルにそれぞれ **XPK_1**という名前のインデックスを含めることはできますが、同じテーブルに **XPK_1**という名前のインデックスを 2 つ含めることはできません。 無効になっている既存のインデックスと同じ名前のインデックスを作成することはできません。 インデックス名を変更しても、インデックスは再構築されません。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [セキュリティ](#Security)  
  
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
  
3.  インデックスの名前を変更するテーブルを右クリックし、 **[デザイン]**を選択します。  
  
4.  **[テーブル デザイナー]** メニューの **[インデックス/キー]**をクリックします。  
  
5.  **[選択された主/一意キーまたはインデックス]** ボックスで、名前の変更対象のインデックスを選択します。  
  
6.  グリッド内の **[名前]** をクリックし、テキスト ボックスに新しい名前を入力します。  
  
7.  **[閉じる]**をクリックします。  
  
8.  **ファイル** メニューの **テーブル名***の保存*をクリックします。  
  
#### <a name="to-rename-an-index-by-using-object-explorer"></a>オブジェクト エクスプローラーを使用してインデックスの名前を変更するには  
  
1.  オブジェクト エクスプローラーで、インデックスの名前を変更するテーブルが格納されているデータベースをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[テーブル]** フォルダーを展開します。  
  
3.  プラス記号をクリックして、インデックスの名前を変更するテーブルを展開します。  
  
4.  プラス記号をクリックして **[インデックス]** フォルダーを展開します。  
  
5.  名前を変更するインデックスを右クリックし、 **[名前の変更]**をクリックします。  
  
6.  新しいインデックス名を入力して、Enter キーを押します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-rename-an-index"></a>インデックスの名前を変更するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]**をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]**をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    --Renames the IX_ProductVendor_VendorID index on the Purchasing.ProductVendor table to IX_VendorID.   
  
    EXEC sp_rename N'Purchasing.ProductVendor.IX_ProductVendor_VendorID', N'IX_VendorID', N'INDEX';   
    GO  
    ```  
  
 詳細については、「[sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)」を参照してください。  
  
  
