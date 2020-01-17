---
title: カーソルを閉じる |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], closing
- closing cursors [ODBC]
ms.assetid: 4f19bf5e-6d8c-40ae-a975-cfd62a0790ec
author: MightyPen
ms.author: genemi
ms.openlocfilehash: de22797bdcf4ff526a8c17aee313567da3114b60
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036546"
---
# <a name="closing-the-cursor"></a>カーソルを閉じる
アプリケーションは、カーソルの使用が完了したら、それを呼び出す**SQLCloseCursor**カーソルを閉じます。 以下に例を示します。  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 アプリケーションがカーソルを閉じるまで、別の SQL ステートメントの実行など、カーソルを開かれているステートメントは他のほとんどの操作に使用できません。 カーソルが開いているときに呼び出すことができる関数の完全な一覧については、[付録 B:ODBC の状態遷移テーブル](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md) を参照してください。  
  
> [!NOTE]  
>  カーソルを閉じるために、アプリケーションは **SQLCloseCursor** を呼び出す必要があります。 **SQLCancel** ではありません。  
  
 カーソルを開いたままが明示的に閉じるまでトランザクションがコミットまたはロールバック時に一部のデータ ソース、カーソルを閉じる点が異なります。 具体的には、結果の最後に到達した場合に設定、 **SQLFetch** sql_no_data が返されます、カーソルを閉じられません。 空の結果セット (結果セットが正常に実行されたステートメントが行を返さなかった場合に作成された) であってもカーソルは、明示的に終了する必要があります。
