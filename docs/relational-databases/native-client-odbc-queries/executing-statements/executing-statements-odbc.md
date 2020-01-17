---
title: ステートメントの実行 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: efd0b9ba46975512491dadccb5a44940af52ec28
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73791027"
---
# <a name="executing-statements-odbc"></a>ステートメントの実行 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Native Client ODBC ドライバー [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースで SQL ステートメントを実行するためのさまざまな方法が用意されています。  
  
-   直接実行  
  
-   準備実行  
  
 直接実行では、[!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを含む文字列を作成し、 **SQLExecDirect**関数を使用して実行するために送信します。 準備実行では、[!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを含む文字列を作成してから、そのステートメントを 2 段階に分けて実行します。 最初の段階では、 [SQLPrepare 関数](https://go.microsoft.com/fwlink/?LinkId=59360)関数を使用して、[!INCLUDE[ssDE](../../../includes/ssde-md.md)]内のステートメントの実行プランを解析およびコンパイルします。 2番目の段階では、 **Sqlexecute**関数を使用して、事前に準備された実行プランを実行します。 この方法では、各実行にかかる解析とコンパイルのオーバーヘッドが抑制されます。 準備実行は、通常、同一のパラメーター化された SQL ステートメントを繰り返し実行するアプリケーションで使用されます。  
  
 どちらの実行方法でも、[!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントまたは SQL ステートメントのバッチを 1 つ実行でき、ステートメントからストアド プロシージャを呼び出すことができます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [直接実行](../../../relational-databases/native-client-odbc-queries/executing-statements/direct-execution.md)  
  
-   [準備実行](../../../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
-   [手順](../../../relational-databases/native-client-odbc-queries/executing-statements/procedures.md)  
  
-   [ステートメントのバッチ](../../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md)  
  
-   [ISO オプションの効果](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md)  
  
## <a name="see-also"></a>参照  
 [クエリ&#40;の実行 ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
