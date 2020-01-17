---
title: ODBC のトランザクション |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], about transactions
- transactions [ODBC]
ms.assetid: b4ca861a-c164-4e87-8672-d5de15e3823c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 521a2ffbf0f8eb5e2590ae6e42d50dc71d536683
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086040"
---
# <a name="transactions-odbc"></a>トランザクション (ODBC)
A*トランザクション*作業単位は、1 つのアトミック操作として行われます。 は、操作の成功や全体が失敗しました。 たとえば、1 つの銀行口座から資金の転送を検討してください。 これは、2 つの手順: 最初のアカウントからお金を現金との 1 秒間のデポジットします。 重要です。 両方の手順が成功します。1 つのステップが成功して失敗するその他の余裕がないです。 トランザクションをサポートするデータベースは、これを保証できます。  
  
 いずれかでトランザクションを完了できます*コミット*中または*ロールバック*します。 トランザクションがコミットされた場合、トランザクションは永続的なものに変更します。 トランザクションがロールバックされるときは、トランザクションの開始前に、の状態に影響を受けた行が返されます。 アカウント転送の例を拡張するには、アプリケーションを最初のアカウントを引き落とすための 1 つの SQL ステートメントと 2 番目のアカウントのクレジットを別の SQL ステートメントを実行します。 2 つのステートメントが成功した場合、その後、アプリケーションは、トランザクションをコミットします。 何らかの理由でいずれかのステートメントが失敗した場合、アプリケーション、トランザクションをロールバックします。 どちらの場合は、アプリケーションは、トランザクションの最後に一貫性のある状態を保証します。  
  
 1 つのトランザクションには、異なるタイミングで複数のデータベース操作は含まれています。 で他のトランザクションが、中間結果に完全にアクセスを持っている場合は、トランザクションが互いに干渉可能性があります。 たとえば、1 つのトランザクションでは、行を挿入したとします 2 番目のトランザクション、行と、最初のトランザクションがロールバックを読み取ります。 2 番目のトランザクションを今すぐには、存在しない行のデータがあります。  
  
 この問題を解決するには、1 つ別のトランザクションを分離するさまざまなパターンがあります。 *トランザクション分離*一般にによって実装されるロックの行を同時に同じ行を使用して 1 つ以上のトランザクションを適応します。 一部のデータベースで行をロックには他の行をロック可能性がありますはもできます。  
  
 トランザクション分離は削減*同時実行性、* または同時に同じデータを使用する 2 つのトランザクションの機能です。 詳細については、次を参照してください。[トランザクション分離レベルの設定](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md)します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ODBC でのトランザクション](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [トランザクション分離](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [コンカレンシー制御](../../../odbc/reference/develop-app/concurrency-control.md)
