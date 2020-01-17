---
title: '手順 4a: 結果が得られない |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], fetching results
- fetches [ODBC], fetching results
ms.assetid: 77d30142-c774-473c-96fb-b364bb92ac60
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3ab0bdabe8b2d66bf054f07ea51056a4044b4ae8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114185"
---
# <a name="step-4a-fetch-the-results"></a>手順 4a: 結果をフェッチする
次の手順は、次の図に示すように、結果を取得します。  
  
 ![ODBC アプリケーションで結果のフェッチ](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 場合に、ステートメントが実行される"手順 3。ビルドして SQL ステートメントを実行する"が、**選択**ステートメントまたはカタログ関数の場合は、アプリケーションを呼び出す最初**SQLNumResultCols**結果セット内の列の数を決定します。 この手順は、アプリケーションが既に SQL ステートメントを垂直方向またはカスタム アプリケーションにハードコーディングする場合など、列の設定の結果の数を把握している場合は、必要ではありません。  
  
 次に、アプリケーションは、名前、データ型、有効桁数、および各結果セット列の小数点以下桁数を取得**SQLDescribeCol**します。 ここでも、この情報を知っている垂直方向およびカスタムのアプリケーションなどのアプリケーションの必要はありません。 アプリケーションは、この情報を渡す**SQLBindCol**、アプリケーション変数、結果セット内の列にバインドします。  
  
 アプリケーションの現在の呼び出し**SQLFetch**データの最初の行を取得し、その行からデータにバインドされた変数内に配置する**SQLBindCol**します。 行に、長い形式のデータがある場合を呼び出して**SQLGetData**データを取得します。 アプリケーションの継続を呼び出す**SQLFetch**と**SQLGetData**追加データを取得します。 これには、データのフェッチが完了したら、後に呼び出す**SQLCloseCursor**カーソルを閉じます。  
  
 結果の取得の詳細については、次を参照してください。 [(Basic) を取得する結果](../../../odbc/reference/develop-app/retrieving-results-basic.md)と[(詳細) を取得する結果](../../../odbc/reference/develop-app/retrieving-results-advanced.md)します。  
  
 これでアプリケーションに返す"手順 3。ビルドして SQL ステートメントを実行する"と同じトランザクションで別のステートメントを実行するには進みますまたは"手順 5。トランザクションをコミットするには"コミットまたはトランザクションをロールバックします。
