---
title: レベル 1 API 関数 (ODBC Driver for Oracle) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC level 1 API functions [ODBC]
- ODBC driver for Oracle [ODBC], functions
- level 1 API functions [ODBC]
- API functions [ODBC]
ms.assetid: 98cced6f-41b8-43c1-a3cd-f4ea1615c0af
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cb1771f88987073b1ef0bcc106f8de28549affe6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085474"
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>レベル 1 API 関数 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用します。  
  
 このレベルの提供するコア インターフェイスの適合性の関数の他のトランザクションなどの追加機能をサポートします。  
  
|API 関数|注|  
|------------------|-----------|  
|**SQLColumns**|結果の指定したテーブルの列の一覧は、テーブルまたはテーブルのセットを作成します。 パブリック シノニムの列を要求するときに SYNONYMCOLUMNS 接続属性を設定し、空の文字列として指定された、 *szTableOwner*引数。 パブリック シノニムの列を返すときに、ドライバーはテーブル名の列を空の文字列に設定します。 結果セットには、追加の列各行の末尾の序数位置にはが含まれています。 この値は、テーブル内の列の序数位置です。|  
|**SQLDriverConnect**|既存のデータ ソースに接続します。 詳細については、次を参照してください。[接続文字列の形式と属性](../../odbc/microsoft/connection-string-format-and-attributes.md)します。|  
|**SQLGetConnectOption**|接続オプションの現在の設定を返します。 この関数は部分的にサポートされています。 ドライバーのすべての値をサポートする、 *fOption*引数がいくつかサポートしていません*vParam*の値を*fOption*引数[SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md). 詳細については、次を参照してください。[接続オプション](../../odbc/microsoft/connect-options.md)します。|  
|**SQLGetData**|指定された結果セットの現在のレコードの 1 つのフィールドの値を取得します。|  
|**SQLGetFunctions**|サポートされているすべての関数の場合は TRUE を返します。 ドライバー マネージャーによって実装されています。|  
|**SQLGetInfo**|SQLHDBC、SQLUSMALLINT、SQLPOINTER、SQLSMALLINT、SQLSMALLINT などの情報を返します\*、ODBC Driver for Oracle データ ソース、接続ハンドルに関連付けられているについて*hdbc*します。|  
|**SQLGetStmtOption**|ステートメント オプションの現在の設定を返します。 詳細については、次を参照してください。[ステートメント オプション](../../odbc/microsoft/statement-options.md)します。|  
|**SQLGetTypeInfo**|データ ソースでサポートされるデータ型に関する情報を返します。 ドライバーは、SQL 結果セット内の情報を返します。|  
|**SQLParamData**|組み合わせて使用**SQLPutData**ステートメントの実行時にパラメーターのデータを指定します。|  
|**SQLPutData**|ステートメントの実行時にドライバーをパラメーターまたは列のデータを送信するアプリケーションをできるようにします。|  
|**SQLSetConnectOption**|接続の側面を制御するオプションへのアクセスを提供します。 この関数は部分的にサポートされています。ドライバーのすべての値をサポートする、 *fOption*引数がいくつかサポートしていません*vParam*の値を*fOption*引数[SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md). 詳細については、次を参照してください。[接続オプション](../../odbc/microsoft/connect-options.md)します。|  
|**SQLSetStmtOption**|ステートメント ハンドルに関連するオプションを設定*hstmt*します。 詳細については、次を参照してください。[ステートメント オプション](../../odbc/microsoft/statement-options.md)します。|  
|**SQLSpecialColumns**|テーブルの行を一意に識別する最適な列のセットを取得します。|  
|**SQLStatistics**|1 つのテーブルとインデックス、またはテーブルに関連付けられているタグの名前に関する統計情報の一覧を取得します。 ドライバーは、その結果、情報を設定を返します。|  
|**SQLTables**|内のパラメーターで指定されたテーブル名の一覧を返します、 **SQLTables**ステートメント。 パラメーターが指定されていない場合は、現在のデータ ソースに格納されているテーブル名を返します。 ドライバーは、その結果、情報を設定を返します。<br /><br /> 列挙型の呼び出しでは、リモート ビューまたはローカルのパラメーター化されたビューの結果セットのエントリは表示されません。 ただし、呼び出しを**SQLTables**一意テーブルの名前指定子は、検索のようなビューでは、その名前を持つ、存在する場合は、これにより、新しいテーブルを作成する前に、名前の競合をチェックする API。<br /><br /> パブリック シノニムがの TABLE_OWNER 値と共に返されます""です。<br /><br /> SYS またはシステムによって所有されているビューは、システム ビューとして識別されます。|
