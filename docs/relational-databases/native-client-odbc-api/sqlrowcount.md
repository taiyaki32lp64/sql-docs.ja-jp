---
title: SQLRowCount |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLRowCount function
ms.assetid: 967ed3d4-3d31-4485-ac92-027076ebc829
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 676e2cc86a6b41a1bc778160611a9a967336390f
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73785691"
---
# <a name="sqlrowcount"></a>SQLRowCount
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  パラメーター値の配列がステートメントの実行にバインドされている場合、 **SQLRowCount**は、ステートメントの実行時にパラメーター値のいずれかの行でエラー状態が発生した場合に SQL_ERROR を返します。 関数の*Rowcountptr*引数によって値が返されることはありません。  
  
 アプリケーションは、SQL_ATTR_PARAMS_PROCESSED_PTR ステートメント属性を使用して、エラーが発生するまでに処理されたパラメーター数をキャプチャできます。  
  
 また、SQL_ATTR_PARAM_STATUS_PTR ステートメント属性を使用してバインドされた状態値の配列を使用して、問題のあるパラメーター行の配列オフセットをキャプチャできます。 アプリケーションは、状態配列をすべて確認し、実際に処理された行数を判断できます。  
  
 OUTPUT 句を使用して INSERT、UPDATE、DELETE、または MERGE ステートメント [!INCLUDE[tsql](../../includes/tsql-md.md)] を実行すると、OUTPUT 句によって生成された結果セット内のすべての行が使用されるまで、SQLRowCount は影響を受ける行の数を返しません。 これらの行を使用するには、SQLFetch または SQLFetchScroll を呼び出します。 SQLResultCols は、すべての結果行が使用されるまで-1 を返します。 SQLFetch または SQLFetchScroll が SQL_NO_DATA を返すと、アプリケーションは SQLRowCount を呼び出して、次の結果に移動するために SQLMoreResults を呼び出す前に、影響を受けた行の数を確認する必要があります。  
  
## <a name="see-also"></a>参照  
 [SQLRowCount 関数](https://go.microsoft.com/fwlink/?LinkId=59367)   
 [ODBC API 実装の詳細](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
