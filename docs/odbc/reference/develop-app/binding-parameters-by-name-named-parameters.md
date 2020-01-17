---
title: (名前付きパラメーター) の名前によるパラメーターのバインド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- named parameters [ODBC]
- binding parameters by name [ODBC]
ms.assetid: e2c3da5a-6c10-4dd5-acf9-e951eea71a6b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3fdd8d00bd6af5479079e66c1ca42f249e033d29
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107639"
---
# <a name="binding-parameters-by-name-named-parameters"></a>名前によるパラメーターのバインド (名前付きパラメーター)
特定の Dbms では、アプリケーションの代わりに、プロシージャの呼び出し内の位置での名前でストアド プロシージャにパラメーターを指定します。 このようなパラメーターが呼び出される*名前付きパラメーター*します。 ODBC では、名前付きパラメーターの使用をサポートします。 ODBC では、名前付きパラメーターはストアド プロシージャの呼び出しでのみ使用され、その他の SQL ステートメントでは使用できません。  
  
 ドライバーは、パラメーターが使用される名前付きかどうかを判断する IPD の SQL_DESC_UNNAMED フィールドの値を確認します。 SQL_DESC_UNNAMED が SQL_UNNAMED に設定されていない場合、ドライバーでは、IPD の SQL_DESC_NAME フィールドの名前をパラメーターを識別するために使用します。 パラメーターをバインドするアプリケーションを呼び出すことができます**SQLBindParameter**にパラメーター情報を指定して呼び出すことができますし、 **SQLSetDescField** IPD の SQL_DESC_NAME フィールドを設定します。 名前付きパラメーターを使用している場合、プロシージャの呼び出しでパラメーターの順序は重要ではありませんし、パラメーターのレコード番号は無視されます。  
  
 無名のパラメーターと名前付きパラメーターの違いは、記述子のレコード数と、プロシージャでパラメーター番号間のリレーションシップです。 無名のパラメーターを使用している場合、最初のパラメーター マーカーは、プロシージャの呼び出し (作成順序) の最初のパラメーターをさらに関連付けられているパラメーター記述子の最初のレコードに関連します。 名前付きパラメーターを使用している場合は、最初のパラメーター マーカーが、パラメーターの記述子の最初のレコードに関連するもが、記述子のレコード数と、プロシージャでパラメーター番号間のリレーションシップはもう存在しません。 名前付きパラメーターには、プロシージャのパラメーター位置; を記述子レコード番号のマッピングは使用しないでください。代わりに、記述子のレコード名は、プロシージャのパラメーター名にマップされます。  
  
> [!NOTE]  
>  IPD の自動作成が有効になっている場合、ドライバーが設定されます、記述子記述子レコードの順序でプロシージャの定義でパラメーターの順序が一致するよう場合でも、名前付きパラメーターが使用されます。  
  
 名前付きパラメーターを使用する場合のすべてのパラメーターはパラメーターを名前する必要があります。 任意のパラメーターが名前付きパラメーターでない場合は、パラメーターを名前パラメーターの ca のいずれもなります。 名前付きパラメーターと名前のないパラメーターの混在がある場合は、ドライバーに依存をする、動作になります。  
  
 名前付きパラメーターの例は、ストアド プロシージャが次のように定義された SQL Server であるとします。  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 この手順では、最初のパラメーターで@title_idが既定値は 1 です。 アプリケーションでは、次のコードを使用して、1 つだけの動的パラメーターを指定するように、このプロシージャを呼び出します。 このパラメーターは、名前を持つ名前付きパラメーター"\@引用符"。  
  
```  
// Prepare the procedure invocation statement.  
SQLPrepare(hstmt, "{call test(?)}", SQL_NTS);  
  
// Populate record 1 of ipd.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                  30, 0, szQuote, 0, &cbValue);  
  
// Get ipd handle and set the SQL_DESC_NAMED and SQL_DESC_UNNAMED fields  
// for record #1.  
SQLGetStmtAttr(hstmt, SQL_ATTR_IMP_PARAM_DESC, &hIpd, 0, 0);  
SQLSetDescField(hIpd, 1, SQL_DESC_NAME, "@quote", SQL_NTS);  
  
// Assuming that szQuote has been appropriately initialized,  
// execute.  
SQLExecute(hstmt);  
```
