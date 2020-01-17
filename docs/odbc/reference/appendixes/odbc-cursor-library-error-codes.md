---
title: ODBC カーソル ライブラリのエラー コード |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursor library [ODBC], error codes
- error codes [ODBC], cursor library
- ODBC cursor library [ODBC], error codes
ms.assetid: 9713480e-8744-4f37-a630-20871590d4a1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a3fb86e1332e3b7e4d89003ccf6421151e5d9cec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100669"
---
# <a name="odbc-cursor-library-error-codes"></a>ODBC カーソル ライブラリのエラー コード
> [!IMPORTANT]  
>  この機能は、Microsoft Data Access Component の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 代わりに、ドライバーとサーバー カーソルを使用します。  
  
 ODBC カーソル ライブラリは、次について記載されているだけでなくを返します[ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
> [!NOTE]  
>  カーソル ライブラリが状態レコードは順序付けしませんドライバー マネージャーと ODBC 3。*x*ドライバーが状態レコードの順序を担当します。  
  
|SQLSTATE|説明|を返されることができます。|  
|--------------|-----------------|--------------------------|  
|01000|カーソルは更新できません。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|カーソル ライブラリが使用されません。 読み込みに失敗しました。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|カーソル ライブラリが使用されません。 不足しているドライバーのサポート。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|カーソル ライブラリが使用されません。 バージョンのドライバー マネージャーが一致しません。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|ドライバーには、SQL_SUCCESS_WITH_INFO が返されます。 警告メッセージが失われました。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000|一般的なエラー:ファイル バッファーを作成できません。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|一般的なエラー:ファイル バッファーから読み取ることができません。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|一般的なエラー:ファイル バッファーに書き込めませんでした。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|一般的なエラー:閉じるか、ファイル バッファーを削除できません。|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|検索可能な列にバインドされていないために、位置指定の要求を実行できません。|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|結合条件によって結果セットが作成されたので、位置指定の要求を実行できませんでした。|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|バインドされたバッファーは、最大セグメント サイズを超えています。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|によって結果セットが生成されませんでした、**選択**ステートメント。|**SQLGetData**|  
|SL005|**選択**ステートメントに GROUP BY 句が含まれています。|**SQLGetData**|  
|SL006|位置指定の要求では、パラメーター配列はサポートされていません。|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|**SQLGetData** (セクタの境界) 順方向専用カーソルでは許可されていません。|**SQLGetData**|  
|SL009|呼び出しの前に列にバインドされていない**SQLFetch**または**SQLFetchScroll**します。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|**SQLBindCol**しようとする内部バッファーをバインドする SQL_ERROR が返されます。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|ステートメントのオプションは、呼び出した後にだけ有効な**SQLFetch**または**SQLFetchScroll**します。|**SQLGetStmtAttr**|  
|SL012|カーソルが開いている間、ステートメントのバインドを変更できません。|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|位置指定の要求が発行され、バッファーに格納されたすべての列数のフィールド。|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**SQLFetch**と**SQLFetchScroll**混在させることはできません。|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|
