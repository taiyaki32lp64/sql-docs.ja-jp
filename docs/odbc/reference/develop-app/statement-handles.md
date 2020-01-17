---
title: ステートメント ハンドル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 65d6d78b-a8c8-489a-9dad-f8d127a44882
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 730ead7bf90af3b6e6906fe184e0fa3312212137
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107257"
---
# <a name="statement-handles"></a>ステートメント ハンドル
A*ステートメント*が最も簡単に考えるの SQL ステートメントなど**SELECT\*FROM Employee**します。 ただし、ステートメントが SQL ステートメントでは単 - のすべての結果セットが、ステートメントによって作成された、ステートメントの実行で使用されるパラメーターなど、その SQL ステートメントに関連付けられた情報で構成されます。 ステートメントは、アプリケーション定義の SQL ステートメントもは必要ありません。 カタログなどの関数とではたとえば、 **SQLTables**が実行されるステートメントでテーブル名の一覧を返す定義済みの SQL ステートメントを実行します。  
  
 各ステートメントは、ステートメント ハンドルによって識別されます。 ステートメントが 1 つの接続に関連付けられていると、その接続で複数のステートメントがあります。 一部のドライバー サポート; のアクティブなステートメントの数を制限します。オプション、SQL_MAX_CONCURRENT_ACTIVITIES **SQLGetInfo**ドライバーが 1 つの接続でサポートする数のアクティブなステートメントを指定します。 ステートメントは、定義*active*結果保留中の場合は、結果が結果セットまたは影響を受ける行の数、**INSERT**、 **UPDATE**、または**DELETE**ステートメント、またはデータが複数の呼び出しに送信される**SQLPutData**します。  
  
 ODBC ドライバー マネージャー (ドライバー) を実装するコード内では、ステートメント ハンドルは、ステートメントの情報を含む構造体を識別します。  
  
-   ステートメントの状態  
  
-   現在のステートメント レベルの診断  
  
-   アプリケーション変数のアドレスは、ステートメントのパラメーターにバインドされ、結果セット列  
  
-   各ステートメント属性の現在の設定  
  
 ステートメント ハンドルは、ほとんどの ODBC 関数で使用されます。 特に、パラメーターをバインドし、結果セット列、関数で使用されます (**SQLBindParameter**と**SQLBindCol**)、準備し、ステートメントの実行 (**SQLPrepare**、 **SQLExecute**、および**SQLExecDirect**)、メタデータの取得 (**SQLColAttribute**と**SQLDescribeCol**)、フェッチ結果 (**SQLFetch**)、および診断の取得 (**SQLGetDiagField**と**SQLGetDiagRec**)。 カタログ関数でも使用されます (**SQLColumns**、 **SQLTables**など) とその他の関数の番号。  
  
 ステートメント ハンドルがで割り当てられた**SQLAllocHandle**およびに解放された**SQLFreeHandle**します。
