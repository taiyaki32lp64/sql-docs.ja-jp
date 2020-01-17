---
title: 動作変更および ODBC 3.x ドライバー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sql_attr_odbc_version [ODBC]
- backward compatibility [ODBC], behavioral changes
- compatibility [ODBC], behavioral changes
ms.assetid: 88a503cc-bff7-42d9-83ff-8e232109ed06
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 27b48951c6fb3be8bfe070863409d77ab760d5fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915616"
---
# <a name="behavioral-changes-and-odbc-3x-drivers"></a>動作変更および ODBC 3.x ドライバー
環境属性を SQL_ATTR_ODBC_VERSION ODBC が発生する必要があるかどうかにドライバーを示します*2.x*動作または ODBC *3.x*動作します。 SQL_ATTR_ODBC_VERSION 環境属性を設定する方法は、アプリケーションによって異なります。 ODBC *3.x*アプリケーションを呼び出す必要があります**SQLSetEnvAttr**を呼び出すことが後に、この属性を設定する**SQLAllocHandle**環境ハンドルの割り当てに呼び出しの前に、**SQLAllocHandle**接続ハンドルを割り当てられません。 これを行うよう、失敗した場合、ドライバー マネージャーは SQLSTATE HY010 を返します (関数のシーケンス エラーです)、後者の呼び出しで**SQLAllocHandle**します。  
  
> [!NOTE]  
>  動作が変更されると、アプリケーションの機能の詳細については、次を参照してください。[動作が変更される](../../../odbc/reference/develop-app/behavioral-changes.md)します。  
  
 ODBC *2.x*アプリケーションや ODBC *2.x* 、ODBC を使って再コンパイルされたアプリケーション*3.x*ヘッダー ファイルは呼び出さないでください**SQLSetEnvAttr**します。 ただし、呼び出す**SQLAllocEnv**の代わりに**SQLAllocHandle**環境ハンドルを割り当てられません。 そのため、アプリケーションを呼び出すと**SQLAllocEnv**ドライバー マネージャーは、ドライバー マネージャーで、 **SQLAllocHandle**と**SQLSetEnvAttr**ドライバー。 したがって、ODBC *3.x*ドライバー常に信頼性のこの属性が設定されています。  
  
 呼び出し、ODBC_STD コンパイル フラグでコンパイルされた標準に準拠したアプリケーションの場合**SQLAllocEnv** (ために発生する可能性があります**SQLAllocEnv** ISO で非推奨ではない)、呼び出しにマップされて**SQLAllocHandleStd**コンパイル時にします。 実行時に、アプリケーション呼び出し**SQLAllocHandleStd**します。 ドライバー マネージャーは、SQL_ATTR_ODBC_VERSION 環境属性を SQL_OV_ODBC3 に設定します。 呼び出し**SQLAllocHandleStd**への呼び出しに相当**SQLAllocHandle**で、 *HandleType* sql_handle_env としてとへの呼び出しの**SQLSetEnvAttr**を SQL_ATTR_ODBC_VERSION を SQL_OV_ODBC3 に設定します。  
  
 特定ドライバーのアーキテクチャでは、ODBC のいずれかとして表示するドライバーが必要である*2.x*ドライバーまたは ODBC *3.x*接続に応じて、ドライバー。 ドライバーここで実際にはありますが、ドライバー、ドライバー マネージャーと他のドライバーの間に存在するレイヤー。 たとえば、ODBC スパイのように、ドライバーを模倣こと可能性があります。 別の例では、EDA]/[SQL のように、ゲートウェイとして機能、可能性があります。 ODBC として表示する*3.x*ドライバーでは、このようなドライバーは、エクスポートすることである必要があります**SQLAllocHandle**、および ODBC として表示する*2.x*ドライバーはエクスポートできる必要があります**SQLAllocConnect**、 **SQLAllocEnv**、および**SQLAllocStmt**します。 ドライバー マネージャーが、このドライバーのエクスポートを確認します、環境、接続、またはステートメントは、割り当てられるが、 **SQLAllocHandle**します。 ドライバーは、ドライバー マネージャーの呼び出しから**SQLAllocHandle**ドライバー。 Odbc ドライバーが動作して場合*2.x*ドライバー、ドライバーはへの呼び出しをマップする必要があります**SQLAllocHandle**に**SQLAllocConnect**、 **SQLAllocEnv**、または**SQLAllocStmt**必要に応じて、します。 何も行う必要がありますも、 **SQLSetEnvAttr** ODBC どおりに動作するときに呼び出す*2.x*ドライバー。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [Datetime データ型](../../../odbc/reference/appendixes/datetime-data-types.md)  
  
-   [C データ型の下位互換性](../../../odbc/reference/appendixes/backward-compatibility-of-c-data-types.md)  
  
-   [固定長のブックマーク](../../../odbc/reference/appendixes/fixed-length-bookmarks.md)  
  
-   [SQLGetInfo のサポート](../../../odbc/reference/appendixes/sqlgetinfo-support.md)  
  
-   [SQL_NO_DATA を返す](../../../odbc/reference/appendixes/returning-sql-no-data.md)  
  
-   [データを挿入するための SQLSetPos の呼び出し](../../../odbc/reference/appendixes/calling-sqlsetpos-to-insert-data.md)  
  
-   [序数での読み込み](../../../odbc/reference/appendixes/loading-by-ordinal.md)
