---
title: カーソル | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- forward-only cursors [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], about cursors
- cursors [ODBC]
- fetches [ODBC], cursors
- result sets [ODBC], fetching
- block cursors [ODBC]
ms.assetid: 0b114352-3c63-4d33-9220-182ede90e4aa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3c9179506ac96c1902c40de271f6024ed7e5c54d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002008"
---
# <a name="cursors"></a>カーソル
アプリケーションを使用してデータのフェッチ、*カーソル*します。 カーソルは、結果セットと異なります。結果セットは、カーソルは、アプリケーションにこれらの行を返しますのソフトウェアの特定の検索条件に一致する行のセットです。 名前*カーソル、* データベースに適用される、コンピューターのターミナルで、点滅するカーソルから発生した可能性があります。 カーソルでは、画面と型指定された単語が次で表示される場所の現在の位置を示すと同様、カーソル結果セットでは、結果セットとどのような行が次に返される現在の位置を示します。  
  
 ODBC のカーソル モデルは、embedded SQL のカーソル モデルに基づきます。 これらのモデルの大きな違いの 1 つは、方法カーソルが開かれます。 Embedded sql の場合は、カーソルをする必要がありますが明示的に宣言され、開かを使用します。 ODBC では、結果セットを作成するステートメントが実行されたときにカーソルを暗黙的に開きます。 カーソルが開かれたときに、結果セットの最初の行の前に配置されます。 埋め込み SQL と ODBC の両方でこれを使用して、アプリケーションが終了した後、カーソルを閉じてください。  
  
 別のカーソルでは、さまざまな特性があります。 カーソルと呼ばれるの最も一般的な種類、*順方向専用カーソルでは、* のみできる結果セットに移動します。 前の行を返すには、アプリケーションする必要がありますを閉じるカーソルを再度開きますおよび必要な行に達するまで、結果セットの先頭から行を読み取る。 順方向専用カーソルでは、1 回の結果セットをパススルーを行うための高速なメカニズムを提供します。  
  
 順方向専用カーソルは、小さい画面ベースのアプリケーション、ユーザーが逆方向にスクロールするのに役立ちますし、データを転送します。 このようなアプリケーションでは、設定、ローカルにデータをキャッシュおよびスクロール自体を実行すると、結果を読み取ることによって、順方向専用カーソルを使用できます。 ただし、これは、少量のデータでのみ機能します。 優れたソリューションが使用するには、*スクロール可能なカーソル、* 結果セットへのランダム アクセスを提供します。 このようなアプリケーションも、パフォーマンスが向上、時に、データの 1 つ以上の行をフェッチと呼ばれるものを使用して、*カーソルをブロックします。* ブロック カーソルの詳細については、次を参照してください。[ブロック カーソルを使用して](../../../odbc/reference/develop-app/using-block-cursors.md)します。  
  
 順方向専用カーソルは、ODBC の既定のカーソルの種類でについては、次のセクションで説明します。 ブロック カーソルとスクロール可能なカーソルの詳細については、次を参照してください。[ブロック カーソル](../../../odbc/reference/develop-app/block-cursors.md)と[スクロール可能なカーソル](../../../odbc/reference/develop-app/scrollable-cursors.md)します。  
  
> [!IMPORTANT]  
>  コミットまたは明示的に呼び出すことによって、トランザクションをロールバック**SQLEndTran**または自動コミット モードで運用してにより一部のデータ ソース接続ですべてのステートメントのすべてのカーソルを閉じます。 詳細についてで SQL_CURSOR_COMMIT_BEHAVIOR と SQL_CURSOR_ROLLBACK_BEHAVIOR 属性を参照してください、 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)関数の説明。
