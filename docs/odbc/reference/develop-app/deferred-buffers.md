---
title: 遅延バッファー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- buffers [ODBC], deferred
- deferred buffers [ODBC]
ms.assetid: 02c9a75c-2103-4f68-a1db-e31f7e0f1f03
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1f7c90dacc375877b4e449b8d59533ce75ff8a4e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076831"
---
# <a name="deferred-buffers"></a>遅延バッファー
A*遅延バッファー*はいくつかの時点で使用される値の 1 つ*後*関数呼び出しで指定されています。 たとえば、 **SQLBindParameter**に関連付けるには、使用または*バインド、* SQL ステートメント内のパラメーターを使用して、データ バッファー。 アプリケーションは、パラメーターの数を指定し、アドレス、バイトの長さ、およびバッファーの型を渡します。 ドライバーは、この情報を保存しますが、バッファーの内容を確認できません。 後で、アプリケーションでは、ステートメントを実行するときにドライバーが情報を取得し、パラメーター データを取得して、データ ソースに送信するには。 そのため、バッファー内のデータの入力は遅延されます。 遅延バッファーは 1 つの関数で指定された、他で使用されるため、これは、プログラミング エラー アプリケーション、ドライバーがまだ期待した; が存在するときに、遅延のバッファーを解放するには詳細については、次を参照してください。[割り当ておよび解放バッファー](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)、このセクションで後述します。  
  
 入力と出力の両方のバッファーを延期できます。 次の表は、遅延のバッファーの用途をまとめたものです。 結果セット列にバインドされている遅延バッファーがで指定されたことに注意してください。 **SQLBindCol**、SQL ステートメントのパラメーターにバインドされている遅延バッファーがで指定されたと**SQLBindParameter**。  
  
|バッファーの使用|型|指定されました。|使用元|  
|----------------|----------|--------------------|-------------|  
|入力パラメーターのデータを送信します。|遅延入力|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|更新または結果の行を挿入するデータの送信の設定|遅延入力|**SQLBindCol**|**SQLSetPos**|  
|出力および入力/出力パラメーターのデータを返す|遅延出力|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|データを設定して結果を返す|遅延出力|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
