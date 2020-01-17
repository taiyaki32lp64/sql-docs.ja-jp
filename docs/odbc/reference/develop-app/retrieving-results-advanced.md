---
title: (詳細) 結果の取得 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- offsets [ODBC]
- result sets [ODBC], about result sets
- bind offsets [ODBC]
ms.assetid: bc00c379-71a7-407a-975c-898243f39bb6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22a88a96b856ba0976dcb8600d26f78b772654bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020504"
---
# <a name="retrieving-results-advanced"></a>結果の取得 (詳細)
アプリケーションがバインドされたデータ バッファーのアドレスおよび対応する長さ/インジケーターにオフセットを追加することを指定できますバッファー アドレスとき**SQLBulkOperations**、 **SQLFetch**、 **SQLFetchScroll**、または**SQLSetPos**が呼び出されます。 これらの追加の結果は、これらの操作で使用されるアドレスを決定します。  
  
 バインドのオフセットを呼び出さずにバインドを変更するアプリケーションを許可する**SQLBindCol**以前にバインドされた列。 呼び出し**SQLBindCol**データを再バインドするバッファーのアドレスと長さ/インジケーターのポインターを変更します。 単位のオフセットを再バインドその一方で、単にオフセットを追加、既存のバインドされたデータ バッファーのアドレスと長さ/インジケーター バッファーのアドレス。 オフセットを使用している場合、バインドは、アプリケーションのバッファーのレイアウトの「テンプレート」と、アプリケーションは、オフセットを変更することでメモリの異なる領域にこの"template"を移動することができます。 新しいオフセットは、いつでも指定することができは常に最初にバインドされた値に追加します。  
  
 バインドのオフセットを指定するには、アプリケーションは、SQLINTEGER バッファーのアドレスに SQL_ATTR_ROW_BIND_OFFSET_PTR ステートメント属性を設定します。 アプリケーションなど、バインドを使用する関数を呼び出す前に**SQLBulkOperations**、 **SQLFetch**、 **SQLFetchScroll**、または**SQLSetPos**、バインドされた列は、結果セットとしてとが 0 の場合のデータ バッファーのアドレスも長さ/インジケーター バッファーのアドレスでもない限り、このバッファー内のバイトのオフセットに配置します。 アドレスとオフセットの合計は、有効なアドレスである必要があります。 (このいずれかまたは両方のオフセットとオフセットを追加するアドレスできますしないことを示します有効な場合は、その合計が有効なアドレスである限り。)SQL_ATTR_ROW_BIND_OFFSET_PTR ステートメント属性は、1 つのオフセット値を変更することによって変更されたすべてのデータ バインディングの 1 つ以上のセットにオフセット値を適用できるようにポインターです。 アプリケーションは、カーソルが閉じられるまで、ポインターが有効にすることを確認してください。  
  
> [!NOTE]  
>  ODBC 2 では、バインディングのオフセットはサポートされていません。*x*ドライバー。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ブロック カーソル](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [スクロール可能なカーソル](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [ODBC カーソル ライブラリ](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [複数の結果](../../../odbc/reference/develop-app/multiple-results.md)
