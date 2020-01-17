---
title: '代替: SQL ステートメントを使用して |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ADO]
- editing data [ADO], sql statements
- ADO, SQL statements
ms.assetid: 8b528b23-063d-45ea-8dea-6a90d4060b20
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f41ef7f0641877056a6e2f3d85fd6a40ff7826db
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925997"
---
# <a name="alternatives-using-sql-statements"></a>代替: SQL ステートメントの使用
ADO では、その組み込みプロパティとデータを編集するためのメソッドの代わりに、コマンドを使用してもできます。 プロバイダーによっては、このセクションで説明されているすべての操作することもできます、データ ソースにコマンドを渡すことによって。 SQL UPDATE ステートメントを使用してを使用せずにデータを変更するなど、**値**のプロパティを**フィールド**します。 SQL の INSERT ステートメントは、ADO メソッドではなく、データ ソースに新しいレコードを追加するために使用できます**AddNew**します。 SQL またはプロバイダーのデータ操作言語の詳細については、データ ソースのドキュメントを参照してください。  
  
 たとえば、次のコードに示すように、データベースへの DELETE ステートメントを含む SQL 文字列を渡すことができます。  
  
```  
'BeginSQLDelete  
strSQL = "DELETE FROM Shippers WHERE ShipperID = " & intId  
objConn1.Execute strSQL, , adCmdText + adExecuteNoRecords  
'EndSQLDelete  
```
