---
title: SQLRowCount |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLRowCount function
ms.assetid: 967ed3d4-3d31-4485-ac92-027076ebc829
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ff2a744f68cf6152330179eb8dcab1f33911914
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046607"
---
# <a name="sqlrowcount"></a>SQLRowCount
  パラメーター値の配列がステートメントの実行にバインドされている場合`SQLRowCount`パラメーター値のいずれかの行は、ステートメントの実行でエラーを生成する場合、SQL_ERROR を返します。 値が返されない、 *RowCountPtr*関数の引数。  
  
 アプリケーションは、SQL_ATTR_PARAMS_PROCESSED_PTR ステートメント属性を使用して、エラーが発生するまでに処理されたパラメーター数をキャプチャできます。  
  
 また、SQL_ATTR_PARAM_STATUS_PTR ステートメント属性を使用してバインドされた状態値の配列を使用して、問題のあるパラメーター行の配列オフセットをキャプチャできます。 アプリケーションは、状態配列をすべて確認し、実際に処理された行数を判断できます。  
  
 ときに、 [!INCLUDE[tsql](../../includes/tsql-md.md)] OUTPUT 句を付けて INSERT、UPDATE、DELETE、または MERGE ステートメントが実行され、SQLRowCount では、OUTPUT 句によって生成される結果セット内のすべての行が消費されるまでの影響を受ける行の数が返されません。 消費するこれらの行を呼び出す SQLFetch または SQLFetchScroll です。 SQLResultCols 結果のすべての行が消費されるまで-1 が返されます。 SQLFetch または SQLFetchScroll sql_no_data が返されると、アプリケーションは、次の結果に移動する SQLMoreResults を呼び出す前に影響を受ける行の数を決定する SQLRowCount を呼び出す必要があります。  
  
## <a name="see-also"></a>参照  
 [SQLRowCount 関数](https://go.microsoft.com/fwlink/?LinkId=59367)   
 [ODBC API 実装の詳細](odbc-api-implementation-details.md)  
  
  
