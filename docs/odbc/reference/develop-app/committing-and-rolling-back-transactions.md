---
title: コミットして、トランザクションをロールバック |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- transactions [ODBC], committing
ms.assetid: 800f2c1a-6f79-4ed1-830b-aa1a62ff5165
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c7c028ca7e89378e959b11f59cad4119cef5086a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083306"
---
# <a name="committing-and-rolling-back-transactions"></a>トランザクションのコミットとロールバック
手動コミット モードでのトランザクションをロールバックまたはコミットは、アプリケーションが呼び出す**SQLEndTran**します。 通常のトランザクションをサポートする Dbms 用のドライバーを実行してこの関数の実装を**コミット**または**ロールバック**ステートメント。 ドライバー マネージャーは呼び出しません**SQLEndTran**場合でも、アプリケーションが、トランザクションをロールバックしようとしています。 単に SQL_SUCCESS、が返された、接続は自動コミット モードであるとします。 実装できるため、トランザクションをサポートしない Dbms 用のドライバーは、自動コミット モードでは常に、 **SQLEndTran**を何もせずに関係なく SQL_SUCCESS を返しますまたは、まったく実装しません。  
  
> [!NOTE]  
>  アプリケーションのコミットまたはを実行して、トランザクションをロールバックする必要がありますいない**コミット**または**ロールバック**ステートメントと**SQLExecute**または**SQLExecDirect**. この効果は定義されていません。 考えられる問題には、不要になったトランザクションがアクティブな場合を知ること、ドライバーとトランザクションをサポートしないデータ ソースに対する失敗したこれらのステートメントが含まれます。 これらのアプリケーションを呼び出す必要があります**SQLEndTran**代わりにします。  
  
 アプリケーションは、環境ハンドルを渡す場合**SQLEndTran**が概念的には、ドライバー マネージャー、接続ハンドルに渡さないを呼び出す**SQLEndTran**ドライバーごとに、環境ハンドルを使用します。環境内の 1 つまたは複数のアクティブな接続があります。 ドライバーは、環境内の各接続でトランザクションをコミットします。 ただし、ドライバーでも、ドライバー マネージャーが、環境での接続で 2 フェーズ コミットを実行することに注意がこれは、プログラミングの便宜を同時に呼び出すだけで**SQLEndTran**環境内のすべての接続。  
  
 (A *2 フェーズ コミット*一般に複数のデータ ソースが分散トランザクションをコミットするために使用します。 その最初のフェーズで、トランザクションの一部をコミットできるかどうかについて、データ ソースがポーリングされます。 2 番目のフェーズは、すべてのデータ ソースで実際には、トランザクションがコミットされました。 データ ソースは、トランザクションをコミットすることはできません、最初のフェーズで返信する場合、2 番目のフェーズは発生しません。)
