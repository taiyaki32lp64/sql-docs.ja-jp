---
title: パラメーターのバインド |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, parameters
- parameters [SQL Server Native Client], ODBC
- statements [ODBC], parameters
- binding parameters [SQL Server Native Client]
- parameter markers [ODBC]
- unbound parameter markers
- SQLBindParameter function
- ODBC applications, parameters
- bound parameter markers [SQL Server Native Client]
ms.assetid: d6c69739-8f89-475f-a60a-b2f6c06576e2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9dfe88f11cc26d4a9711b7f21caf4c4475ec954b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206738"
---
# <a name="binding-parameters"></a>パラメーターのバインド
  SQL ステートメントの各パラメーター マーカーは、ステートメントを実行する前にアプリケーション内の変数に関連付ける、つまりバインドする必要があります。 これは、呼び出すことで、 [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md)関数。 **SQLBindParameter**ドライバーにプログラム変数 (アドレス、C データ型など) について説明します。 また、序数値を示すことでパラメーター マーカーを識別してから、そのパラメーター マーカーが表す SQL オブジェクト表現 (SQL データ型、有効桁数など) を記述します。  
  
 パラメーター マーカーは、ステートメントの実行前にいつでもバインドまたは再バインドできます。 次のいずれかの操作を行うまでは、パラメーターのバインドは有効なままです。  
  
-   呼び出し[SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md)で、*オプション*SQL_RESET_PARAMS に設定するパラメーターは、ステートメント ハンドルにバインドされているすべてのパラメーターを解放します。  
  
-   呼び出し**SQLBindParameter**で*ParameterNumber*バインドされたパラメーター マーカーの序数を設定は、前のバインディングを自動的に解放します。  
  
 アプリケーションでは、パラメーターをプログラム変数の配列にバインドし、SQL ステートメントをバッチで処理することもできます。 配列のバインドには、次の 2 種類があります。  
  
-   列方向のバインドは、各パラメーターを変数の独自の配列にバインドすることで行います。  
  
     呼び出すことによって、列方向のバインドが指定されて[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)で*属性*に SQL_ATTR_PARAM_BIND_TYPE および*ValuePtr*に sql_param_bind_by_column をそれぞれ設定します。  
  
-   行方向のバインドは、SQL ステートメント内のすべてのパラメーターを 1 単位として、パラメーターの各変数を保持する構造体の配列にバインドすることで行います。  
  
     呼び出すことによって、行方向のバインドが指定されて**SQLSetStmtAttr**で*属性*に SQL_ATTR_PARAM_BIND_TYPE および*ValuePtr*いる構造体のサイズに設定、プログラム変数。  
  
 ときに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーが文字またはバイナリ文字列パラメーターをサーバーに送信で指定した長さの値を埋めます**SQLBindParameter** *ColumnSize*パラメーター。 ODBC 2.x アプリケーションの場合は 0 を指定する場合*ColumnSize*ドライバーは、データ型の有効桁数のパラメーター値を埋めます。 有効桁数は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サーバーに接続している場合は 8,000、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続している場合は 255 です。 *ColumnSize*はバリアント型の列のバイト単位です。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ストアド プロシージャ パラメーターの名前を定義できます。 また、ODBC 3.5 では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアド プロシージャを呼び出すときに使用する名前付きパラメーターのサポートも導入されました。 このサポートは次の目的に使用します。  
  
-   ストアド プロシージャを呼び出し、そのストアド プロシージャ用に定義したパラメーターのサブセットに値を提供します。  
  
-   アプリケーション内で、ストアド プロシージャの作成時に指定した順序とは異なる順序でパラメーターを指定します。  
  
 名前付きパラメーターがサポートされるのは、[!INCLUDE[tsql](../../includes/tsql-md.md)] `EXECUTE` ステートメントまたは ODBC CALL エスケープ シーケンスを使用してストアド プロシージャを実行するときだけです。  
  
 ストアド プロシージャ パラメーターに `SQL_DESC_NAME` を設定する場合、クエリ内のすべてのストアド プロシージャ パラメーターにも `SQL_DESC_NAME` を設定する必要があります。  かどうかリテラルが呼び出しに使用するストアド プロシージャのパラメーターがある`SQL_DESC_NAME`設定すると、リテラルは形式を使用する必要があります *'名*=*値*' ここで、 *名*ストアド プロシージャのパラメーター名は、(たとえば、 @p1)。 詳細については、次を参照してください。 [(名前付きパラメーター) の名前によるパラメーターのバインド](https://go.microsoft.com/fwlink/?LinkId=167215)します。  
  
## <a name="see-also"></a>参照  
 [ステートメント パラメーターの使用](using-statement-parameters.md)  
  
  
