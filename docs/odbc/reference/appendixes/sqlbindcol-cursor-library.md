---
title: SQLBindCol (カーソル ライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocStmt function [ODBC], Cursor Library
ms.assetid: f4dd546a-0a6c-4397-8ee7-fafa6b9da543
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 71afc3c0bac0ea64285c450640d96fe5f5d709b0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064975"
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックの使用、 **SQLBindCol**カーソル ライブラリ内の関数。 に関する一般的な情報**SQLBindCol**を参照してください[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)します。  
  
 アプリケーションでは、カーソル ライブラリで現在の行セットを返すには、1 つまたは複数のバッファーを割り当てます。 呼び出す**SQLBindCol**結果セットにこれらのバッファーをバインドする 1 つ以上の時間。  
  
 アプリケーションが呼び出すことができます**SQLBindCol**結果を再バインドするには列を呼び出した後設定**SQLExtendedFetch**、 **SQLFetch**、または**SQLFetchScroll**C データ型、列のサイズ、およびバインドされた列の 10 進数字の同じ残っている限り、します。 アプリケーションでは、異なるアドレスに列を再バインドする、カーソルは閉じられません必要があります。  
  
 カーソル ライブラリでは、バインドのオフセットを使用する SQL_ATTR_ROW_BIND_OFFSET_PTR ステートメント属性の設定をサポートします。 (**SQLBindCol**呼び出しが発生するこの再バインドする必要はありません)。Odbc カーソル ライブラリが使用されている場合*3.x*ドライバー、バインドのオフセットがない場合に使用**SQLFetch**が呼び出されます。 場合、バインドのオフセットが使用される**SQLFetch** odbc カーソル ライブラリが使用されるときに呼び出される*2.x*ドライバーのため**SQLFetch**にマップされ**SQLExtendedFetch**します。  
  
 カーソル ライブラリ呼び出しをサポートする**SQLBindCol**ブックマーク列をバインドします。  
  
 ODBC を使用する場合*2.x*ドライバー、カーソル ライブラリは、SQLSTATE HY090 を返します (無効な文字列長またはバッファー長) と**SQLBindCol**が呼び出されない値にブックマーク列に対してバッファーの長さを設定するには4 に等しい。 ODBC を使用する場合*3.x*ドライバー、カーソル ライブラリにより、バッファーのサイズを変更します。
