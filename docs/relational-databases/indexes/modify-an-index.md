---
title: インデックスの変更 | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
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
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9c8334573b66b5c227a5033a63b5aedf06909c78
ms.sourcegitcommit: 2efb0fa21ff8093384c1df21f0e8910db15ef931
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68316966"
---
# <a name="modify-an-index"></a>インデックスの変更
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

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
  
次の例では、AdventureWorks データベース内で、`DROP_EXISTING` オプションを使って `Production.WorkOrder` テーブルの `ProductID` 列にある既存のインデックスを削除して再作成します。 ここではオプション `FILLFACTOR` および `PAD_INDEX` も設定されています。  
  
[!code-sql[IndexDDL#CreateIndex4](../../relational-databases/indexes/codesnippet/tsql/modify-an-index_1.sql)]  
  
次の例では、ALTER INDEX を使用して、 `AK_SalesOrderHeader_SalesOrderNumber`インデックスのいくつかのオプションを設定します。  
  
[!code-sql[IndexDDL#AlterIndex4](../../relational-databases/indexes/codesnippet/tsql/modify-an-index_2.sql)]  
  
#### <a name="to-modify-index-columns"></a>インデックス列を変更するには  
  
1.  インデックス列の位置を追加、削除、または変更するには、インデックスを削除してから再作成する必要があります。  
  
## <a name="see-also"></a>参照  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [インデックス オプションの設定](../../relational-databases/indexes/set-index-options.md)   
 [インデックスの名前変更](../../relational-databases/indexes/rename-indexes.md)  
  
  
