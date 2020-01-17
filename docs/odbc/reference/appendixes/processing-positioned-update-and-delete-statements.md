---
title: 処理には、Update および Delete ステートメントが配置されている |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- ODBC cursor library [ODBC], statement processing
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- SQL statements [ODBC], cursor library
- ODBC cursor library [ODBC], positioned update or delete
- cursor library [ODBC], statement processing
ms.assetid: 2975dd97-48e6-4d0a-a9c7-40759a7d94c8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 41b4fe248f815e63c48a8da70edc88a1cc173667
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028427"
---
# <a name="processing-positioned-update-and-delete-statements"></a>位置指定更新と Delete ステートメントの処理
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 配置カーソル ライブラリのサポートが更新し、delete ステートメントを置き換えることで、 **WHERE CURRENT OF**でこのようなステートメントに句を**WHERE**句のキャッシュに格納されている値を列挙します。バインドされた各列。 カーソル ライブラリを新しく構築された渡します**UPDATE**と**DELETE**のドライバーを実行するステートメント。 位置指定の update ステートメントでは、カーソル ライブラリはし、行セットのバッファー内の値からそのキャッシュを更新、SQL_ROW_UPDATED 行の状態配列内の対応する値を設定します。 位置指定の delete ステートメントの場合に、SQL_ROW_DELETED 行の状態配列内の対応する値を設定します。  
  
> [!CAUTION]  
>  **WHERE**任意の行を識別する、別の行を特定または複数の行を識別する、現在の行を識別するために、カーソル ライブラリによって構築された句が失敗することができます。 詳細については、次を参照してください。[検索ステートメントの構築](../../../odbc/reference/appendixes/constructing-searched-statements.md)、この付録で後述します。  
  
 位置指定更新と delete ステートメントが、次の制限を受けます。  
  
-   位置指定更新と削除ステートメントは、次の場合にのみ使用できます: ときに、**SELECT**ステートメントには、結果セットが生成されたときに、**を選択**ステートメントに、結合が含まれていない、 **共用体**句、または**GROUP BY**句; ときに、選択リストで、別名または式を使用するすべての列にバインドされていないと**SQLBindCol**します。  
  
-   位置指定の update または delete ステートメントをアプリケーションを準備する場合に行う必要がありますを呼び出した後**SQLFetch**または**SQLFetchScroll**します。 ステートメントを閉じ、アプリケーションを呼び出すときに直接実行しますが、カーソル ライブラリでは、ドライバーの準備をするステートメントを送信する**SQLExecute**します。  
  
-   ドライバーは、1 つだけアクティブ ステートメントをサポートする場合、結果の残りの部分が設定され、位置指定の実行前に、キャッシュから現在の行セットを変わりませんカーソル ライブラリのフェッチが update または delete ステートメント。 その後、アプリケーションが結果セットのメタデータを返す関数を呼び出す場合 (たとえば、 **SQLNumResultCols**または**SQLDescribeCol**)、カーソル ライブラリ エラーが返されます。  
  
-   後続のすべての位置指定の update または delete ステートメントには、タイムスタンプ列がある場合が失敗するが、更新プログラムが実行されるたびに自動的に更新されるタイムスタンプ列が含まれているテーブルの列の位置指定の update または delete ステートメントが実行される場合バインドされています。 これは、カーソル ライブラリを作成するステートメントが更新する行を正しく識別されませんが、検索結果を更新または削除するために発生します。 Timestamp 列の検索結果のステートメントの値では、自動的に更新されたタイムスタンプ列の値は一致しません。
