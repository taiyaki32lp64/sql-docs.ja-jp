---
title: ステートメントのパラメーター |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement parameters [ODBC]
ms.assetid: 58d5b166-2578-4699-a560-1f1e6d86c49a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0f3aad1537475e288cff06725b5dbd0fe2383924
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107243"
---
# <a name="statement-parameters"></a>ステートメント パラメーター
A*パラメーター*は SQL ステートメントの変数です。 たとえば、部品テーブルに PartID、説明、および価格をという名前の列があるとします。 パラメーターなしのパーツを追加するには、が必要とするように SQL ステートメントの構築します。  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 このステートメントは、新しい注文を挿入、ことはできません、受注アプリケーションに最適なソリューションを挿入する値は、アプリケーションにハードコーディングすることはできません。 代わりに挿入する値を使用して、実行時に SQL ステートメントを作成することです。 ないも最適なソリューションでは、実行時にステートメントを作成する複雑なのためです。 最適なソリューションがの要素を置換するには、**値**疑問符 (?) 句または*パラメーター マーカー*:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 これらのパラメーター マーカーは、その後アプリケーション変数にバインドされます。 新しい行を追加するには、アプリケーションは、変数の値を設定し、ステートメントの実行にのみあります。 ドライバーで、変数から現在値が取得され、データ ソースに送信されます。 ステートメントは複数回実行できる、アプリケーションことができます、プロセスよりも効率的なステートメントを準備しています。  
  
 上記のステートメントは、新しい行を挿入する受注アプリケーションでハード コードされた可能性があります。 ただし、パラメーター マーカーでは、垂直方向のアプリケーションに制限はありません。 任意のアプリケーションのテキストとの変換を回避することで、実行時に SQL ステートメントを構築するが困難な簡単になります。 たとえば、部分 ID が示されている可能性が最も高いを整数としてアプリケーションに格納されています。 SQL ステートメントは、パラメーター マーカーを使用せずに作成は、アプリケーションが部分 ID をテキストに変換する必要があり、データ ソースを使用すると、整数に変換する必要があります。 パラメーター マーカーを使用すると、アプリケーションに送信できます部分 ID ドライバーとして、整数では、通常、整数としてのデータ ソースに送信できます。 これは、2 つの変換を保存します。 長い形式のデータ値は、これは非常に重要ですが、このような値のテキスト形式よく SQL ステートメントに許容される長さを超えているためです。  
  
 パラメーターは、SQL ステートメント内の特定の場所でのみ有効です。 選択リストにない許可されるなど (によって返される列の一覧を**選択**ステートメント) とは、等号 (=) などの二項演算子の両方のオペランドとしてため、許可することはできませんパラメーターの型を決定します。 一般に、パラメーターは、データ定義言語 (DDL) ステートメントではなく、データ操作言語 (DML) ステートメントでのみ有効です。 詳細については、次を参照してください[パラメーター マーカー](../../../odbc/reference/appendixes/parameter-markers.md)付録 c:。SQL 文法。  
  
 SQL ステートメントで名前付きパラメーターが、プロシージャが呼び出されるときに使用できます。 名前付きパラメーターは、SQL ステートメント内の位置ではなく、名前によって識別されます。 呼び出しでバインドできる**SQLBindParameter**、パラメーターがなくの IPD (実装パラメーター記述子) の SQL_DESC_NAME フィールドで識別されますが、 *ParameterNumber*の引数**SQLBindParameter**します。 呼び出すことでバインドすることも**SQLSetDescField**または**SQLSetDescRec**します。 名前付きパラメーターの詳細については、次を参照してください。 [(名前付きパラメーター) の名前によるパラメーターのバインド](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)、このセクションで後述します。 記述子の詳細については、次を参照してください。[記述子](../../../odbc/reference/develop-app/descriptors.md)します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [パラメーターのバインド](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [パラメーターの値の設定](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [長い形式のデータの送信](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [SQLGetData で出力パラメーターを取得します。](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [プロシージャのパラメーター](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [パラメーター値の配列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
