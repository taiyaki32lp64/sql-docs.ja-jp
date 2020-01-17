---
title: エラーとメッセージの処理 |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, about error handling
- errors [ODBC]
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], about messages
- ODBC error handling
- SQL_INVALID_HANDLE return code
- errors [ODBC], about error handling
- messages [ODBC]
ms.assetid: 74ea9630-e482-4a46-bb45-f5234f079b48
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 779a06881d49cf7853f20a5241c52b25d4ccfc24
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73783468"
---
# <a name="handling-errors-and-messages"></a>エラーとメッセージの処理
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  アプリケーションで ODBC 関数を呼び出すときは、ドライバーが関数を実行して診断情報を 2 とおりの方法で返します。つまり、リターン コードで ODBC 関数が成功したか失敗したかを示し、診断レコードで関数の詳細な情報を伝えます。 診断レコードは、ヘッダー レコードと状態レコードから構成されます。 関数が成功した場合でも、少なくとも 1 つの診断レコード、つまりヘッダー レコードが返されます。  
  
 診断情報を開発時に使用すると、ハードコードした SQL ステートメントに存在する、無効なハンドルや構文エラーなどのプログラミング エラーを把握できます。 実行時に使用すると、ユーザーが入力した SQL ステートメントのデータの切り捨て、規則違反、構文エラーなどの実行時エラーや警告を確認できます。 一般的に、プログラミング ロジックはリターン コードを基に組み立てます。  
  
 たとえば、アプリケーションが**Sqlfetch**を呼び出して結果セット内の行を取得した後、結果セットの末尾に到達したか (SQL_NO_DATA)、情報メッセージが返されたかどうか (SQL_SUCCESS_WITH_INFO)、またはエラーが発生しました (SQL_ERROR)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーが SQL_SUCCESS 以外のものを返す場合、アプリケーションは**SQLGetDiagRec**を呼び出して、情報メッセージまたはエラーメッセージを取得できます。 複数のメッセージがある場合は、 **SQLGetDiagRec**を使用してメッセージセットを上下にスクロールします。  
  
 リターン コード SQL_INVALID_HANDLE は常にプログラミング エラーを示します。実行時にはこのコードが返されないようにしてください。 それ以外のリターン コードは実行時の情報を含んでいます。ただし、SQL_ERROR はプログラミング エラーを示す場合もあります。  
  
 元の [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ネイティブ API、DB-LIBRARY (C 用) を使用すると、アプリケーションで、エラーまたはメッセージを返すコールバックエラー処理関数とメッセージ処理関数をインストールできます。 PRINT、RAISERROR、DBCC、SET など、一部の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは、結果セットではなく DB-Library メッセージ ハンドラー関数に結果を返します。 しかし、ODBC API にはそのようなコールバック機能がありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]から返されたメッセージを検出すると、ODBC リターンコードが SQL_SUCCESS_WITH_INFO または SQL_ERROR に設定され、そのメッセージが1つ以上の診断レコードとして返されます。 そのため、ODBC アプリケーションでは、これらのリターンコードを注意深くテストし、 **SQLGetDiagRec**を呼び出してメッセージデータを取得する必要があります。  
  
 エラーのトレースの詳細については、「[データ アクセスのトレース](https://go.microsoft.com/fwlink/?LinkId=125805)」を参照してください。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]に追加されたエラートレースの機能強化の詳細については、「[拡張イベントログの診断情報](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)へのアクセス」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [メッセージを生成するステートメントの処理](../../relational-databases/native-client-odbc-error-messages/processing-statements-that-generate-messages.md)  
  
-   [診断レコードと診断フィールド](../../relational-databases/native-client-odbc-error-messages/diagnostic-records-and-fields.md)  
  
-   [ネイティブ エラー番号](../../relational-databases/native-client-odbc-error-messages/native-error-numbers.md)  
  
-   [SQLSTATE &#40;ODBC エラーコード&#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md)  
  
-   [エラー メッセージ](../../relational-databases/native-client-odbc-error-messages/error-messages.md)  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
