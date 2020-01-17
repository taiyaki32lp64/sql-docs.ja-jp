---
title: エラーとメッセージの処理 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: a4a4d87ccae235aee1a11e58aff60fe8e34d6205
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207094"
---
# <a name="handling-errors-and-messages"></a>エラーとメッセージの処理
  アプリケーションが ODBC 関数を呼び出すときに、ドライバーは関数を実行し、2 つの方法で診断情報を返します。リターン コードは、全体的な成功または失敗の ODBC 関数を示し、診断レコードが、関数に関する詳細情報を提供します。 診断レコードは、ヘッダー レコードと状態レコードから構成されます。 関数が成功した場合でも、少なくとも 1 つの診断レコード、つまりヘッダー レコードが返されます。  
  
 診断情報を開発時に使用すると、ハードコードした SQL ステートメントに存在する、無効なハンドルや構文エラーなどのプログラミング エラーを把握できます。 実行時に使用すると、ユーザーが入力した SQL ステートメントのデータの切り捨て、規則違反、構文エラーなどの実行時エラーや警告を確認できます。 一般的に、プログラミング ロジックはリターン コードを基に組み立てます。  
  
 たとえば、アプリケーションから**SQLFetch**結果セット内の行を取得するリターン コードを示すかどうか、結果セットの末尾に達した (SQL_NO_DATA)、情報メッセージには、(SQL_SUCCESS_ が返された場合WITH_INFO)、またはエラー (SQL_ERROR) が発生しました。  
  
 場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーが SQL_SUCCESS 以外、アプリケーションを呼び出して**SQLGetDiagRec**またはエラー メッセージが情報を取得します。 使用**SQLGetDiagRec**を 1 つ以上のメッセージが表示される場合は、設定、メッセージを上下にスクロールします。  
  
 リターン コード SQL_INVALID_HANDLE は常にプログラミング エラーを示します。実行時にはこのコードが返されないようにしてください。 それ以外のリターン コードは実行時の情報を含んでいます。ただし、SQL_ERROR はプログラミング エラーを示す場合もあります。  
  
 元の[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] c には、Db-library のネイティブ API により、アプリケーションはエラー処理のコールバックをインストールして、メッセージ処理関数の戻り値のエラーやメッセージ。 PRINT、RAISERROR、DBCC、SET など、一部の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは、結果セットではなく DB-Library メッセージ ハンドラー関数に結果を返します。 しかし、ODBC API にはそのようなコールバック機能がありません。 ときに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーから返されるメッセージを検出した[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、ODBC リターン コードを SQL_SUCCESS_WITH_INFO または SQL_ERROR に設定し、メッセージ、1 つ以上の診断レコードが返されます。 そのため、ODBC アプリケーションする必要があります慎重にテストするにはこれらのリターン コードと呼び出し**SQLGetDiagRec**メッセージ データを取得します。  
  
 エラーのトレースの詳細については、「[データ アクセスのトレース](https://go.microsoft.com/fwlink/?LinkId=125805)」を参照してください。 エラーのトレースで追加の機能強化については[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]を参照してください[診断の情報を拡張イベント ログにアクセスする](../native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [メッセージを生成するステートメントの処理](processing-statements-that-generate-messages.md)  
  
-   [診断レコードと診断フィールド](diagnostic-records-and-fields.md)  
  
-   [ネイティブ エラー番号](native-error-numbers.md)  
  
-   [SQLSTATE &#40;ODBC エラー コード&#41;](sqlstate-odbc-error-codes.md)  
  
-   [エラー メッセージ](error-messages.md)  
  
## <a name="see-also"></a>関連項目  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)  
  
  
