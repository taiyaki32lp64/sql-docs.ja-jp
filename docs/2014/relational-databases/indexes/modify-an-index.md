---
title: インデックスの変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- indexes [SQL Server], modifying
- modifying indexes
- index changes [SQL Server]
ms.assetid: 97e3110d-fde7-4f5d-9309-dc1697960aeb
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1da4462f3ba23d263cd30d222f7b9026285b1159
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63162370"
---
# <a name="modify-an-index"></a>インデックスの変更
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]のインデックスを変更する方法について説明します。  
  
> [!IMPORTANT]  
>  PRIMARY KEY 制約または UNIQUE 制約の結果として作成されたインデックスは、この方法を使用して変更することはできません。 このような場合には、制約を変更する必要があります。  
  
 **このトピックの内容**  
  
-   **インデックスを変更するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-modify-an-index"></a>インデックスを変更するには  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、テーブルが属するデータベースを展開して、 **[テーブル]** を展開します。  
  
3.  インデックスが属するテーブルを展開し、 **[インデックス]** を展開します。  
  
4.  変更するインデックスを右クリックし、 **[プロパティ]** をクリックします。  
  
5.  **[インデックスのプロパティ]** ダイアログ ボックスで、目的の変更を行います。 たとえば、インデックス キーの列の追加や削除を行うことができます。また、インデックス オプションの設定も変更できます。  
  
#### <a name="to-modify-index-columns"></a>インデックス列を変更するには  
  
1.  インデックス列の位置を追加、削除、または変更するには、 **[インデックスのプロパティ]** ダイアログ ボックスの **[全般]** ページをクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-modify-an-index"></a>インデックスを変更するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 次の例では、 `ProductID` オプションを使って、 `Production.WorkOrder` テーブルの `DROP_EXISTING` 列にある既存のインデックスを削除して再作成します。 ここではオプション `FILLFACTOR` および `PAD_INDEX` も設定されています。  
  
     [!code-sql[IndexDDL#CreateIndex4](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/createindex.sql#createindex4)]  
  
     次の例では、ALTER INDEX を使用して、 `AK_SalesOrderHeader_SalesOrderNumber`インデックスのいくつかのオプションを設定します。  
  
     [!code-sql[IndexDDL#AlterIndex4](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex4)]  
  
#### <a name="to-modify-index-columns"></a>インデックス列を変更するには  
  
1.  インデックス列の位置を追加、削除、または変更するには、インデックスを削除してから再作成する必要があります。  
  
## <a name="see-also"></a>関連項目  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [INDEXPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/indexproperty-transact-sql)   
 [sys.indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)   
 [sys.index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-index-columns-transact-sql)   
 [インデックス オプションの設定](set-index-options.md)   
 [インデックスの名前変更](indexes.md)  
  
  
