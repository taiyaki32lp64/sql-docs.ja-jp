---
title: ODBC ステートメント ハンドルの解放 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
- freeing statement handles [ODBC]
ms.assetid: ee18e2f1-2690-4cc1-9e5c-e20244e5d480
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 638cf9fb3c7af73130cf1413559b9baee2a354c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069777"
---
# <a name="freeing-a-statement-handle-odbc"></a>ステートメント ハンドルの解放 (ODBC)
前述のようよりにドロップし、新しいものを割り当てるステートメントを再利用するより効率的です。 ステートメントで新しい SQL ステートメントを実行する前にアプリケーションを現在のステートメントの設定が適切であることを確認する必要があります。 確認する設定には、ステートメント属性、パラメーター バインド、結果セットのバインドがあります。 パラメーターと、古い SQL ステートメントの結果セットが一般に、バインドする必要が (呼び出して**SQLFreeStmt** SQL_RESET_PARAMS と SQL_UNBIND オプションを使用して) と、新しい SQL ステートメントの再バインドします。  
  
 呼び出しステートメントを使用するが、アプリケーションが完了したら、 **SQLFreeHandle**ステートメントを解放します。 これは、ステートメントを解放した後、ODBC 関数呼び出しでステートメントのハンドルを使用するアプリケーション プログラミング エラーこれには結果が未定義であるが、致命的な可能性があります。  
  
 ときに**SQLFreeHandle**を呼び出すと、ドライバーのリリースのステートメントについての情報を格納する構造体を使用します。  
  
 **SQLDisconnect**接続ですべてのステートメントを自動的に解放します。
