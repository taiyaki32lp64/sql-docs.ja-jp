---
title: 新機能 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], new features in release
- ODBC drivers [ODBC], backward compatibility
- new features [ODBC]
- compatibility [ODBC], new features in release
- ODBC [ODBC], new features
ms.assetid: a8fcdd00-6cb3-4871-9489-6018b3d0d65f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 74c9a97c2511bc9c9a738b9e63548a9179552489
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086343"
---
# <a name="new-features"></a>新機能
ODBC では、次の新しい機能が導入されました*3.x*します。 ODBC *3.x* odbc 作業アプリケーション*2.x*ドライバーでは、この機能を使用できません。 ODBC *3.x* ODBC を使用する場合に、ドライバー マネージャーでこれらの機能がマップされていない*2.x*ドライバー。  
  
-   記述子を受け取る関数は、引数として処理します。**Sqlsetdescfield による**、 **SQLGetDescField**、 **SQLSetDescRec**、 **SQLGetDescRec**、および**SQLCopyDesc**します。  
  
-   関数は、 **SQLSetEnvAttr**と**SQLGetEnvAttr**します。  
  
-   使用**SQLAllocHandle**記述子ハンドルを割り当てられません。 (使用**SQLAllocHandle**環境、接続、およびステートメント ハンドルの割り当てには、重複のない新しい機能です)。  
  
-   使用**SQLGetConnectAttr** SQL_ATTR_AUTO_IPD 接続属性を取得します。 (の使用**SQLSetConnectAttr**を設定して**SQLGetConnectAttr**を取得するその他の接続属性には重複のない新しい機能です)。  
  
-   使用**SQLSetStmtAttr**を設定して**SQLGetStmtAttr** 、次のステートメント属性を取得します。 (の使用**SQLSetStmtAttr**を設定して**SQLGetStmtAttr**を取得するその他のステートメント属性には重複のない新しい機能です)。  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_ENABLE_AUTO_IPD  
  
     SQL_ATTR_FETCH_BOOKMARK_PTR  
  
     SQL_ATTR_BIND_OFFSET  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     SQL_DESC_PARAM_STATUS_PTR  
  
     SQL_ATTR_PARAMS_PROCESSED_PTR  
  
     SQL_ATTR_PARAMSET_SIZE  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_ROW_ARRAY_SIZE  
  
-   使用**SQLGetStmtAttr**次のステートメント属性を取得します。 (使用**SQLGetStmtAttr**属性が重複している機能、いない新しい機能を他のステートメントを取得します)。  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   C interval データ型、間隔の SQL データ型、BIGINT C データ型で、SQL_C_NUMERIC データ構造体の使用。  
  
-   パラメーターの行方向のバインド。  
  
-   呼び出しなど、オフセットに基づくブックマークをフェッチ**SQLFetchScroll**で、 *FetchOrientation* SQL_FETCH_BOOKMARK と 0 以外のオフセットを指定する引数。  
  
-   **SQLFetch**行の状態配列で呼び出しを混在させないで、複数の行のフェッチ、フェッチされた行の数を返す**SQLFetchScroll**、および混在呼び出し**SQLBulkOperations**または**SQLSetPos**します。 詳細については、次のセクションを参照してください。[ブロック カーソル、スクロール可能なカーソル、および ODBC 3.x アプリケーション用の旧バージョンとの互換性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)します。  
  
-   名前付きパラメーター。  
  
-   ODBC のいずれかの*3.x*-特定**SQLGetInfo**オプション。 (場合、ODBC *3.x* odbc 作業アプリケーション*2.x*ドライバーは、いくつかの ODBC に置き換えられている SQL_XXX_CURSOR_ATTRIBUTES1 の情報の種類を呼び出す*2.x*情報の種類、一部の情報は、信頼性が高く、かもしれませんが信頼性の高いものがあります。 詳細については、次を参照してください[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)。)。  
  
-   オフセットをバインドします。  
  
-   更新、更新、およびブックマークを削除した (呼び出しを通じて**SQLBulkOperations**)。  
  
-   呼び出す**SQLBulkOperations**または**SQLSetPos** S5 状態にします。  
  
-   診断レコードの ROW_NUMBER、目のフィールド (置換関数で取得する必要が**SQLGetDiagField**または**SQLGetDiagRec**)。  
  
-   おおよその行をカウントします。  
  
-   警告情報 (から SQL_ROW_SUCCESS_WITH_INFO **SQLFetchScroll**)。  
  
-   可変長のブックマーク。  
  
-   パラメーターの配列の拡張エラー情報。  
  
-   すべてのカタログ関数によって返される結果セットに新しい列。  
  
-   使用**SQLDescribeCol**と**SQLColAttribute**列 0 にします。  
  
-   任意の ODBC を使用*3.x*-特定の列の属性への呼び出しで**SQLColAttribute**します。  
  
-   複数の環境ハンドルを使用します。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [ODBC 3.x アプリケーション用のブロック カーソル、スクロール可能なカーソル、および下位互換性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
