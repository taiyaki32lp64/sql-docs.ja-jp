---
title: 実行中のバッチ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC], executing
- SQL statements [ODBC], batches
ms.assetid: f082c717-4f82-4820-a2fa-ba607d8fd872
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 84d3cf65284d767d437987c8ff2b21793466106e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901266"
---
# <a name="executing-batches"></a>バッチの実行
アプリケーションでは、ステートメントのバッチを実行する前に、サポートされているかどうかをまずおください。 これは、アプリケーション呼び出しを行う**SQLGetInfo** SQL_BATCH_SUPPORT、SQL_PARAM_ARRAY_ROW_COUNTS、および SQL_PARAM_ARRAY_SELECTS オプションを使用します。 最初のオプションは、行の数を生成して、結果セットを生成するステートメントは明示的なバッチおよび行の数と結果の可用性に関する情報を返しますの設定で後者の 2 つのオプションの中に、プロシージャでサポートされてがパラメーター化するかどうかを返します実行します。  
  
 ステートメントのバッチがを通じて実行された**SQLExecute**または**SQLExecDirect**します。 たとえば、次の呼び出しは、明示的なバッチのステートメントを新しい販売注文を開くを実行します。  
  
```  
SQLCHAR *BatchStmt =  
   "INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)"  
      "VALUES (2002, 1001, {fn CURDATE()}, 'Garcia', 'OPEN');"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 1, 1234, 10);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 2, 987, 8);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 3, 566, 17);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 4, 412, 500)";  
  
SQLExecDirect(hstmt, BatchStmt, SQL_NTS);  
```  
  
 バッチの結果を生成するときにステートメントが実行される、1 つを返しますまたは詳細行の数または結果を設定します。 これらを取得する方法については、次を参照してください。[複数結果](../../../odbc/reference/develop-app/multiple-results.md)します。  
  
 ステートメントのバッチには、パラメーター マーカーが含まれている場合は、その他のステートメントでは、パラメーターの順序を増やすことでこれら番号が付けられます。 次のステートメントのバッチが 1 ~ 21 です。 番号付きのパラメーターを持ちなど最初にある**挿入**ステートメントは、番号付き 1 ~ 5 と最後の**挿入**ステートメントは番号付きの 18 ~ 21 です。  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 パラメーターの詳細については、次を参照してください。[ステートメント パラメーター](../../../odbc/reference/develop-app/statement-parameters.md)、このセクションで後述します。
