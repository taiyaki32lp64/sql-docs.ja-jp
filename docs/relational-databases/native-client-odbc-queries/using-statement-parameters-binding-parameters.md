---
title: パラメーターのバインド |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 340a3a0f44201c81eafe8717962b2894709eb65d
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779537"
---
# <a name="using-statement-parameters---binding-parameters"></a>ステートメント パラメーターの使用 - パラメーターのバインド
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL ステートメントの各パラメーター マーカーは、ステートメントを実行する前にアプリケーション内の変数に関連付ける、つまりバインドする必要があります。 これは、 [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)関数を呼び出すことによって行われます。 **SQLBindParameter**は、ドライバーへのプログラム変数 (Address、C データ型など) を記述します。 また、序数値を示すことでパラメーター マーカーを識別してから、そのパラメーター マーカーが表す SQL オブジェクト表現 (SQL データ型、有効桁数など) を記述します。  
  
 パラメーター マーカーは、ステートメントの実行前にいつでもバインドまたは再バインドできます。 次のいずれかの操作を行うまでは、パラメーターのバインドは有効なままです。  
  
-   *Option*パラメーターをに設定して[SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md)を呼び出すと、ステートメントハンドルにバインドされているすべてのパラメーターが SQL_RESET_PARAMS 解放されます。  
  
-   *Parameternumber*をバインドされたパラメーターマーカーの序数に設定して**SQLBindParameter**を呼び出すと、前のバインドが自動的に解放されます。  
  
 アプリケーションでは、パラメーターをプログラム変数の配列にバインドし、SQL ステートメントをバッチで処理することもできます。 配列のバインドには、次の 2 種類があります。  
  
-   列方向のバインドは、各パラメーターを変数の独自の配列にバインドすることで行います。  
  
     列方向のバインドは、*属性*を SQL_ATTR_PARAM_BIND_TYPE に設定し、 *valueptr*を SQL_PARAM_BIND_BY_COLUMN に設定して、 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)を呼び出すことによって指定します。  
  
-   行方向のバインドは、SQL ステートメント内のすべてのパラメーターを 1 単位として、パラメーターの各変数を保持する構造体の配列にバインドすることで行います。  
  
     行方向のバインドは、*属性*を SQL_ATTR_PARAM_BIND_TYPE に設定し、 *valueptr*をプログラム変数を保持する構造体のサイズに設定して、 **SQLSetStmtAttr**を呼び出すことによって指定します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーが文字またはバイナリ文字列パラメーターをサーバーに送信すると、 **SQLBindParameter** *columnsize*パラメーターで指定された長さに値が埋め込まれます。 ODBC 2.x アプリケーションで*Columnsize*に0が指定されている場合、ドライバーは、パラメーター値をデータ型の有効桁数に埋め込みます。 有効桁数は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サーバーに接続している場合は 8,000、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続している場合は 255 です。 バリアント型の列の場合、 *Columnsize*はバイト単位です。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ストアド プロシージャ パラメーターの名前を定義できます。 また、ODBC 3.5 では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアド プロシージャを呼び出すときに使用する名前付きパラメーターのサポートも導入されました。 このサポートは次の目的に使用します。  
  
-   ストアド プロシージャを呼び出し、そのストアド プロシージャ用に定義したパラメーターのサブセットに値を提供します。  
  
-   アプリケーション内で、ストアド プロシージャの作成時に指定した順序とは異なる順序でパラメーターを指定します。  
  
 名前付きパラメーターは、[!INCLUDE[tsql](../../includes/tsql-md.md)] **execute**ステートメントまたは ODBC CALL エスケープシーケンスを使用してストアドプロシージャを実行する場合にのみサポートされます。  
  
 ストアドプロシージャパラメーターに**SQL_DESC_NAME**が設定されている場合は、クエリ内のすべてのストアドプロシージャパラメーターで**SQL_DESC_NAME**も設定する必要があります。  ストアドプロシージャの呼び出しでリテラルが使用されている場合、パラメーターに**SQL_DESC_NAME**が設定されている場合、リテラルでは *' name*=*value*' の形式を使用する必要があります。ここで、 *NAME*はストアドプロシージャのパラメーター名です (たとえば、@p1). 詳細については、「[名前によるパラメーターのバインド (名前付きパラメーター)](https://go.microsoft.com/fwlink/?LinkId=167215)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ステートメント パラメーターの使用](../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)  
  
  
