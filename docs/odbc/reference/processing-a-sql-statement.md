---
title: SQL ステートメントの処理 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], processing
- SQL [ODBC], processing statements
- statement processing [ODBC]
- SQL statements [ODBC]
- ODBC [ODBC], SQL
ms.assetid: 96270c4f-2efd-4dc1-a985-ed7fd5658db2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dfbf23f0be369ae540dac33d33a3e3c1505d5ebe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076280"
---
# <a name="processing-a-sql-statement"></a>SQL ステートメントの処理
プログラムによる SQL の使用方法を説明する前に、SQL ステートメントの処理方法を説明する必要があります。 必要な手順は、各手法を実行したら、その異なる時刻では、3 つすべての手法に共通です。 次の図では、このセクションの残りの部分で説明する、SQL ステートメントの処理に関連する手順を示します。  
  
 ![SQL ステートメントを処理する手順を](../../odbc/reference/media/pr01.gif "pr01")  
  
 SQL ステートメントを処理するには、DBMS は、次の 5 つの手順を実行します。  
  
1.  DBMS は、まず、SQL ステートメントを解析します。 これは、ステートメントをトークンと呼ばれる個々 の単語に分割、有効な動詞と有効な句は、という具合に、ステートメントがあることを確認します。 この手順では、構文エラーおよびスペル ミスを検出できます。  
  
2.  DBMS は、ステートメントを検証します。 システム カタログに対して、ステートメントを確認します。 ステートメントで指定したすべてのテーブルにデータベースにも存在しますか。 存在のすべての列と、あいまいな列名がありませんか。 ステートメントの実行に必要な特権があるか。 この手順では、特定のセマンティック エラーを検出できます。  
  
3.  DBMS は、アクセス ステートメントのプランを生成します。 アクセスの計画は、ステートメントを実行するために必要な手順のバイナリ表現です。実行可能コードの DBMS と同じになります。  
  
4.  DBMS は、アクセス プランが最適化されます。 これには、アクセスの計画を実行するさまざまな方法について説明します。 インデックスは、検索を高速化に使用できますか。 必要があります、DBMS まずテーブルを検索条件を適用し、し、テーブル B への参加またはする必要があります、結合で始まるし、検索条件を使用して、その後でしょうか。 テーブルを順次検索を回避したり、テーブルのサブセットに縮小しますか。 その他の方法を学習した後は、DBMS は、うち 1 つを選択します。  
  
5.  DBMS は、アクセスの計画を実行して、ステートメントを実行します。  
  
 必要なデータベースへのアクセスと、必要な時間の量の量、SQL ステートメントを処理するための手順が異なります。 SQL ステートメントを解析し、データベースへのアクセスが必要としない、非常に簡単に行うことができます。 最適化は、CPU を大量に消費一方では処理し、システム カタログへのアクセスが必要です。 だけで複雑なクエリの場合、オプティマイザーが何千もの同じクエリを実行するさまざまな方法を探索できます。 ただし、非効率なクエリの実行のコストは非常に高いため、最適化に費やされた時間が増加したクエリの実行速度の回復は複数のでは、通常は。 これは、反復的なクエリを実行する同じプランが最適化されたアクセスを繰り返し使用できる場合は、さらに大きな。
