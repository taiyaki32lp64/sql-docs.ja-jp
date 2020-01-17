---
title: SQLGetInfo (カーソル ライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Cursor Library
ms.assetid: 1b4d220d-2c07-4f56-987e-36813bb1a6ce
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6f115ded8392ddc3dcac32c2477794c007d5eb81
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073924"
---
# <a name="sqlgetinfo-cursor-library"></a>SQLGetInfo (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックの使用、 **SQLGetInfo**カーソル ライブラリ内の関数。 に関する一般的な情報**SQLGetInfo**を参照してください[SQLGetInfo 関数](../../../odbc/reference/syntax/sqlgetinfo-function.md)します。  
  
 カーソル ライブラリは、次の値の値を返します*情報の種類*(&#124; OR 演算を表す) の他のすべての値です*情報の種類*、呼び出します**SQLGetInfo** 。ドライバー。  
  
|*情報の種類*|戻り値|  
|----------------|--------------------|  
|SQL_BOOKMARK_PERSISTENCE|SQL_BP_SCROLL|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|0|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|0|  
|SQL_FETCH_DIRECTION[1]|SQL_FD_FETCH_ABSOLUTE &#124; です。SQL_FD_FETCH_FIRST &#124; です。SQL_FD_FETCH_LAST &#124; です。SQL_FD_FETCH_NEXT &#124; です。SQL_FD_FETCH_PRIOR &#124; です。SQL_FD_FETCH_RELATIVE &#124; です。SQL_FD_FETCH_BOOKMARK|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|SQL_CA1_NEXT、&#124; です。SQL_CA1_ABSOLUTE &#124; です。SQL_CA1_RELATIVE &#124; です。SQL_CA1_LOCK_NO_CHANGE、&#124; です。SQL_CA1_POS_POSITION &#124; です。SQL_CA1_POSITIONED_DELETE &#124; です。SQL_CA1_POSITIONED_UPDATE、&#124; です。SQL_CA1_SELECT_FOR_UPDATE|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|SQL_CA2_READ_ONLY_CONCUR &#124; です。SQL_CA2_OPT_VALUES_CONCURRENCY、&#124; です。SQL_CA2_SENSITIVITY_UPDATES|  
|SQL_GETDATA_EXTENSIONS|SQL_GD_BLOCK&#124;ドライバーによって返された値**に注意してください。** データを取得するときに**SQLFetchScroll**、 **SQLGetData** SQL_GD_ANY_COLUMN と SQL_GD_BOUND ビットマスクを指定された機能をサポートしています。|  
|SQL_KEYSET_DRIVEN_CURSOR_ATTRIBUTES1|0|  
|SQL_KEYSET_DRIVEN_CURSOR_ATTRIBUTES2|0|  
|SQL_LOCK_TYPES[1]|SQL_LCK_NO_CHANGE|  
|SQL_STATIC_CURSOR_ATTRIBUTES1|SQL_CA1_NEXT、&#124; です。SQL_CA1_ABSOLUTE &#124;です。SQL_CA1_RELATIVE &#124; です。SQL_CA1_BOOKMARK &#124; です。SQL_CA1_LOCK_NO_CHANGE、&#124; です。SQL_CA1_POS_POSITION &#124; です。SQL_CA1_POSITIONED_DELETE &#124; です。SQL_CA1_POSITIONED_UPDATE、&#124; です。SQL_CA1_SELECT_FOR_UPDATE|  
|SQL_STATIC_CURSOR_ATTRIBUTES2|SQL_CA2_READ_ONLY_CONCUR &#124; です。SQL_CA2_OPT_VALUES_ 同時実行 &#124; です。SQL_CA2_SENSITIVITY_UPDATES|  
|SQL_POS_OPERATIONS[1]|SQL_POS_POSITION|  
|SQL_POSITIONED_STATEMENTS [1]|SQL_PS_POSITIONED_DELETE &#124; です。SQL_PS_POSITIONED_UPDATE &#124; です。SQL_PS_SELECT_FOR_UPDATE|  
|SQL_ROW_UPDATES|"Y"|  
|SQL_SCROLL_CONCURRENCY[1]|SQL_SCCO_READ_ONLY &#124; です。SQL_SCCO_OPT_VALUES|  
|SQL_SCROLL_OPTIONS|SQL_SO_FORWARD_ONLY &#124; です。SQL_SO_STATIC|  
|SQL_STATIC_SENSITIVITY [1]|SQL_SS_UPDATES|  
  
 [1]、ODBC 2.x のドライバーを使用したカーソル ライブラリが使用される場合にのみを使用します。  
  
> [!IMPORTANT]  
>  カーソル ライブラリは、トランザクションがコミットまたはデータ ソースとしてロールバック時に、同じカーソルの動作を実装します。 つまり、コミットまたはいずれかを呼び出して、トランザクションのロールバック**SQLEndTran** SQL_ATTR_AUTOCOMMIT の接続属性を使用する可能性がありますをアクセス プランを削除し、すべてのステートメントのカーソルを閉じてデータ ソースまたは接続します。 詳細についてで SQL_CURSOR_COMMIT_BEHAVIOR と SQL_CURSOR_ROLLBACK_BEHAVIOR 情報の種類を参照してください。 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)します。
