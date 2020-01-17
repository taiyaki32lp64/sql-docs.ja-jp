---
title: アプリケーションを宣言する&#39;s ODBC バージョン |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- declaring ODBC version [ODBC]
- data sources [ODBC], declaring ODBC version
- ODBC drivers [ODBC], declaring ODBC version
- connecting to driver [ODBC], declaring ODBC version
- connecting to data source [ODBC], declaring ODBC version
- version declaration [ODBC]
ms.assetid: 083a1ef5-580a-4979-9cf3-50f4549a080a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ea97e3cd7a8fee3b3397524bf2c48c428d6a0be0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076841"
---
# <a name="declaring-the-application39s-odbc-version"></a>アプリケーションを宣言する&#39;s ODBC のバージョン
アプリケーションが接続によって割り当てられる前に、SQL_ATTR_ODBC_VERSION 環境属性を設定があります。 この属性は、アプリケーションが ODBC に従うことを示す*2.x*または ODBC *3.x*仕様、次のものを使用する場合。  
  
-   **SQLSTATEs**します。 多くの SQLSTATE 値は、ODBC では異なる*2.x*および ODBC *3.x*します。  
  
-   **日付、時刻、および Timestamp 型識別子**します。 次の表は、ODBC の日付、時刻、タイムスタンプ データ型識別子を示します*2.x*および ODBC *3.x*します。  
  
    |ODBC *2.x*|ODBC *3.x*|  
    |----------------|----------------|  
    |**SQL の型識別子**||  
    |SQL_DATE|SQL_TYPE_DATE|  
    |SQL_TIME|SQL_TYPE_TIME|  
    |SQL_TIMESTAMP|SQL_TYPE_TIMESTAMP|  
    |**C 型識別子**||  
    |SQL_C_DATE|SQL_C_TYPE_DATE|  
    |SQL_C_TIME|SQL_C_TYPE_TIME|  
    |SQL_C_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|  
  
-   _CatalogName_  **SQLTables 引数**します。 ODBC で*2.x*でワイルドカード文字 (「%」および「_」)、 *CatalogName*引数が文字どおり扱われます。 ODBC で*3.x*、ワイルドカード文字として扱われます。 したがって、ODBC に続くアプリケーション*2.x*仕様ワイルドカード文字し、エスケープしないにそれらをリテラルとして使用する場合に使用これらにできません。 アプリケーションの ODBC に続く*3.x*仕様はまたはワイルドカード文字として使用して、エスケープする、およびリテラルとして使用します。 詳細については、次を参照してください。[カタログ関数の引数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)します。  
  
 ODBC *3.x*ドライバー マネージャーと ODBC *3.x*ドライバーは、アプリケーションの書き込み先となる、ODBC 仕様のバージョンを確認し、適宜応答します。 たとえば、アプリケーションに依存して、ODBC *2.x*仕様と呼び出し**SQLExecute**呼び出す前に**SQLPrepare**、ODBC *3.x*ドライバー マネージャーは、SQLSTATE S1010 を返します (関数のシーケンス エラーです)。 アプリケーションが ODBC に従う場合*3.x*仕様、ドライバー マネージャーは、SQLSTATE HY010 を返します (関数のシーケンス エラーです)。 詳細については、次を参照してください。[旧バージョンとの互換性と標準準拠](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)します。  
  
> [!IMPORTANT]  
>  次の ODBC アプリケーション*3.x*仕様で条件付きのコードを使用して ODBC に新しい機能を使用しないようにする必要があります*3.x* ODBC を使用する場合*2.x*ドライバー。 ODBC *2.x*ドライバーは ODBC に新しい機能をサポートしていません*3.x*アプリケーションが ODBC に従っていることを宣言していって*3.x*仕様。 さらに、ODBC *3.x*ドライバーは ODBC に新しい機能をサポートするためを停止していない*3.x*アプリケーションが ODBC に従っていることを宣言していって*2.x*指定。
