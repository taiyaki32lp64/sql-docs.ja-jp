---
title: ステートメントの実行 (ODBC) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC]
- ODBC applications, statements
- statements [ODBC], executing
ms.assetid: 063fc40d-ff81-490d-9c9b-2faefb729f37
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1517e17a7b0ecaf9137e3af21e076dacc2fd98f3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207059"
---
# <a name="executing-statements-odbc"></a>ステートメントの実行 (ODBC)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーで SQL ステートメントを実行するさまざまな方法を提供する、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データベース。  
  
-   直接実行  
  
-   準備実行  
  
 直接実行は、含む文字列の構築では、[!INCLUDE[tsql](../../../includes/tsql-md.md)]ステートメントと実行を使用するための送信、 **SQLExecDirect**関数。 準備実行では、[!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを含む文字列を作成してから、そのステートメントを 2 段階に分けて実行します。 最初のステージを使用して、 [SQLPrepare 関数](https://go.microsoft.com/fwlink/?LinkId=59360)を解析およびコンパイルでステートメントの実行プランの関数、[!INCLUDE[ssDE](../../../includes/ssde-md.md)]します。 2 番目の段階を使用して、 **SQLExecute**関数を事前に準備された実行プランを実行します。 この方法では、各実行にかかる解析とコンパイルのオーバーヘッドが抑制されます。 準備実行は、通常、同一のパラメーター化された SQL ステートメントを繰り返し実行するアプリケーションで使用されます。  
  
 どちらの実行方法でも、[!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントまたは SQL ステートメントのバッチを 1 つ実行でき、ステートメントからストアド プロシージャを呼び出すことができます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [直接実行](direct-execution.md)  
  
-   [準備実行](prepared-execution.md)  
  
-   [手順](procedures.md)  
  
-   [ステートメントのバッチ](batches-of-statements.md)  
  
-   [ISO オプションの効果](effects-of-iso-options.md)  
  
## <a name="see-also"></a>関連項目  
 [クエリの実行&#40;ODBC&#41;](../executing-queries-odbc.md)  
  
  
