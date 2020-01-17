---
title: 準備実行 ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- prepared execution [ODBC]
- SQL statements [ODBC], prepared execution
- SQL statements [ODBC], executing
ms.assetid: f08c8a98-31ee-48b2-9dbf-6f31c2166dbb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2107ca1eeecc6fad24311c5bce629784ae4ceff0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023284"
---
# <a name="prepared-execution-odbc"></a>準備実行 ODBC
準備実行は、ステートメントを複数回実行する効率的な方法です。 最初に、ステートメントがコンパイルされたまたは*準備、* アクセス プランにします。 アクセスの計画とは、いずれかを実行し、または後で他にもです。 アクセスの計画の詳細については、次を参照してください。 [SQL ステートメントの処理](../../../odbc/reference/processing-a-sql-statement.md)します。  
  
 準備実行は、同じ、パラメーター化された SQL ステートメントを繰り返し実行する垂直方向およびカスタム アプリケーションで通常使用されます。 たとえば、次のコードは、さまざまな部分の価格を更新するステートメントを準備します。 毎回異なるパラメーター値で複数回ステートメントを実行します。  
  
```  
SQLREAL       Price;  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd = 0, PriceInd = 0;  
  
// Prepare a statement to update salaries in the Employees table.  
SQLPrepare(hstmt, "UPDATE Parts SET Price = ? WHERE PartID = ?", SQL_NTS);  
  
// Bind Price to the parameter for the Price column and PartID to  
// the parameter for the PartID column.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 10, 0,  
                  &PartID, 0, &PartIDInd);  
  
// Repeatedly execute the statement.  
while (GetPrice(&PartID, &Price)) {  
   SQLExecute(hstmt);  
}  
```  
  
 準備実行は、ステートメントが 1 回だけコンパイルされるため、主に 2 回以上実行されるステートメントを直接実行よりも高速化直接実行されるステートメントは、実行されるたびにコンパイルされます。 準備実行もできるネットワーク トラフィックの軽減、ドライバー送信できるので、アクセス プラン識別子データ ソースに毎回、ステートメントが実行される SQL ステートメント全体ではなく場合は、データ ソースのアクセスをサポート プランの識別子。  
  
 アプリケーションでは、結果セットをステートメントが準備された後で実行される前にメタデータを取得できます。 ただし、準備のメタデータを返して、実行されていないステートメント コストがドライバーによって、相互運用可能なアプリケーションで可能であれば避ける必要があります。 詳細については、次を参照してください。[結果セットのメタデータ](../../../odbc/reference/develop-app/result-set-metadata.md)します。  
  
 準備実行は、1 回しか実行されないステートメントには使用しないでください。 このようなステートメントでは、ことが直接実行よりもわずかに遅くなります、追加の ODBC 関数呼び出しを必要とするためです。  
  
> [!IMPORTANT]  
>  コミットまたは明示的に呼び出すことによって、トランザクションをロールバック**SQLEndTran**または自動コミット モードで作業して一部のデータ ソース接続ですべてのステートメントへのアクセスの計画を削除すると発生します。 詳細については、SQL_CURSOR_COMMIT_BEHAVIOR と SQL_CURSOR_ROLLBACK_BEHAVIOR のオプションを参照してください、 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)関数の説明。  
  
 準備し、アプリケーション、ステートメントを実行します。  
  
1.  呼び出し**SQLPrepare**し、SQL ステートメントを含む文字列を渡します。  
  
2.  パラメーターの値を設定します。 パラメーターは、前に、またはステートメントを準備した後に実際に設定できます。 詳細については、次を参照してください。[ステートメント パラメーター](../../../odbc/reference/develop-app/statement-parameters.md)、このセクションで後述します。  
  
3.  呼び出し**SQLExecute**データのフェッチなど、必要な追加の処理を行うとします。  
  
4.  必要に応じて、手順 2. および 3. を繰り返します。  
  
5.  ときに**SQLPrepare**を呼び出すと、ドライバー。  
  
    -   ステートメントを解析することがなく、データ ソースの SQL 文法を使用する SQL ステートメントを変更します。 これで説明されているエスケープ シーケンスを置き換えるが含まれています。 [odbc エスケープ シーケンス](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)します。 アプリケーションが呼び出すことによって、SQL ステートメントの変更されたフォームを取得できます**SQLNativeSql**します。 SQL_ATTR_NOSCAN ステートメントの属性が設定されている場合、エスケープ シーケンスは置き換えられません。  
  
    -   ステートメントを準備、データ ソースに送信します。  
  
    -   (準備に成功した) 場合は、後で実行の返されたアクセス プラン識別子を格納または (準備が失敗した) 場合は、すべてのエラーを返します。 (構文エラーまたはアクセス違反) SQLSTATE 42000 など構文エラーとセマンティック エラー SQLSTATE 42S02 など、エラーが含まれます (ベース テーブルまたはビューが見つかりません)。  
  
        > [!NOTE]  
        >  一部のドライバーは、この時点でエラーが返されるが、代わりに、ステートメントが実行されるとき、またはカタログ関数が呼び出されたときに返すの操作を行います。 したがって、 **SQLPrepare**実際が失敗すると成功することがあります。  
  
6.  ときに**SQLExecute**を呼び出すと、ドライバー。  
  
    -   現在のパラメーター値を取得し、必要に応じてそれらを変換します。 詳細については、次を参照してください。[ステートメント パラメーター](../../../odbc/reference/develop-app/statement-parameters.md)、このセクションで後述します。  
  
    -   データ ソースにアクセス プラン識別子と変換されたパラメーターの値を送信します。  
  
    -   すべてのエラーを返します。 これらは、SQLSTATE 24000 など一般的に、ランタイム エラー (無効なカーソル状態)。 ただし、一部のドライバーは構文とセマンティック エラーをこの時点で返します。  
  
 データ ソースがステートメントの準備をサポートしていない場合、ドライバーする必要がありますをエミュレート、可能な範囲。 など、ドライバーが何もしないときに**SQLPrepare**と呼ばれ、ステートメントの直接の実行を実行時に**SQLExecute**が呼び出されます。  
  
 ドライバーがチェックするときにステートメントを送信可能性があります、データ ソースは、構文チェックが実行をサポートする場合**SQLPrepare**が呼び出され、ステートメントの実行を送信するときに**SQLExecute**はと呼ばれる。  
  
 ステートメントを格納する場合は、ドライバーは、ステートメントの準備をエミュレートすることはできません、ときに**SQLPrepare**と呼びます。 実行のために送信時に**SQLExecute**が呼び出されます。  
  
 エミュレートされたステートメントの準備は完璧ではないため**SQLExecute**によって通常返されたエラーを返すことができます**SQLPrepare**します。
