---
title: 関数マッピングでは、ドライバー マネージャー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], functions
- driver manager [ODBC], function mapping
- functions [ODBC], Unicode functions
ms.assetid: ff093b29-671a-4fc0-86c9-08a311a98e54
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2bfa535d4175c109e96098dd1e40e93be9521de2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069687"
---
# <a name="function-mapping-in-the-driver-manager"></a>ドライバー マネージャーの関数マッピング
ドライバー マネージャーは、文字列引数を受け取る関数の 2 つのエントリ ポイントをサポートします。 装飾されていない関数 (**SQLDriverConnect**) は、関数の ANSI 形式です。 Unicode 形式がで修飾された、 *W* (**SQLDriverConnectW**)。  
  
 ODBC ヘッダー ファイルで修飾された関数もサポートしています、 *A、* (**SQLDriverConnectA**) 混合 ANSI または Unicode アプリケーションが使いやすいようにします。 呼び出し、 **A**関数呼び出しは、装飾されていないエントリ ポイントを実際には、(**SQLDriverConnect**)。  
  
 アプリケーションをコンパイル、_UNICODE した場合 **#define**、ODBC ヘッダー ファイルが装飾されていない関数の呼び出しにマップされます (**SQLDriverConnect**) Unicode バージョン (**SQLDriverConnectW**.)  
  
 場合 Unicode ドライバーとして認識されるドライバーをドライバー マネージャー **SQLConnectW**ドライバーでサポートされています。  
  
 ドライバーが Unicode ドライバーの場合は、ドライバー マネージャーがとおり関数呼び出しを行います。  
  
-   文字列引数またはパラメーターなしの関数に、ドライバーを通じて直接渡します。  
  
-   Unicode 関数に渡します (で、 *W*サフィックス) 経由で直接ドライバーにします。  
  
-   ANSI の関数に変換します (で、 *A*サフィックス) Unicode 関数 (で、 *W*サフィックス) 文字列引数を Unicode に変換して文字と、ドライバーに、Unicode 関数。  
  
 場合は、ドライバーは、ANSI ドライバー、ドライバー マネージャーがとおり関数呼び出しを行います。  
  
-   文字列引数またはから直接使用するパラメーターなしの関数は、ドライバーに渡します。  
  
-   Unicode 関数に変換 (で、 *W*サフィックス)、ANSI に関数呼び出しをドライバーに渡します。  
  
-   ドライバーに直接、ANSI 関数を渡します。  
  
 ドライバー マネージャーが Unicode 対応の内部でします。 その結果、最適なパフォーマンスは、ドライバー マネージャーは、ドライバーを使用して Unicode 関数を渡すだけであるために、Unicode アプリケーションの場合、Unicode ドライバーを使用して取得されます。 ANSI アプリケーションは、ANSI ドライバーを操作するとき、ドライバー マネージャーする必要があります文字列 ANSI から Unicode に変換など、一部の関数を処理するときに**SQLDriverConnect**します。 関数を処理した後は、関数を ANSI ドライバーに送信する前に ANSI に Unicode 文字列をドライバー マネージャーがし、変換する必要があります。  
  
 アプリケーションの変更またはドライバーに SQL_STILL_EXECUTING または SQL_NEED_DATA が返されるときに、バインドされたパラメーターのバッファーを読み取る必要がありますできません。 ドライバー マネージャーは、ドライバーが SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、または SQL_ERROR に戻るまでに、ANSI にバインドされているバッファーを残します。 マルチ スレッド アプリケーションでは、別のスレッドは、SQL ステートメントを実行するのには任意のバインドされたパラメーター値にアクセスできないようにする必要があります。 ドライバー マネージャーは、Unicode との間でデータを"、"その場での ANSI に変換し、その他のスレッド、ドライバーには、SQL ステートメントがまだ処理中にこれらのバッファーに ANSI データが表示可能性があります。 ANSI のドライバーに Unicode データにバインドするアプリケーションは、同じアドレスに 2 つの異なる列をバインドしない必要があります。
