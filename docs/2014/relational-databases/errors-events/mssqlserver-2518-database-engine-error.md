---
title: MSSQLSERVER_2518 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2518 (Database Engine error)
ms.assetid: 54a13abc-4c33-43f0-b55d-e2e74a1381c8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: df810e28070c797cb24aa3faa308b5419c877139
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914701"
---
# <a name="mssqlserver2518"></a>MSSQLSERVER_2518
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|2518|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC_NO_EXPRESSION_EVAL_CLR_DISABLED|  
|メッセージ テキスト|Object ID O_ID (object "O_NAME"):計算列とユーザー定義型は、共通言語ランタイム (CLR) が無効になっているために、このオブジェクトのチェックできません。|  
  
## <a name="explanation"></a>説明  
 この情報メッセージは、クエリ プロセッサが、計算列と共通言語ランタイム (CLR) のユーザー定義型を評価するための内部オブジェクトを DBCC に提供できなかったことを示しています。 この問題は、いずれかの列に CLR が関係しているにもかかわらず、CLR が有効化されていないために発生しました。 内部オブジェクトはすべての列に及んでいます。 このため、1 つの列を評価できないと、内部オブジェクトの作成ができなくなります。 つまり、計算列の正当性チェックが行われなかったり、DBCC でインデックスとベース テーブルの整合性をチェックする際に計算列が使用されないことを意味します。  
  
## <a name="user-action"></a>ユーザーの操作  
 CLR を有効にして、DBCC ステートメントを再実行します。  
  
## <a name="see-also"></a>参照  
 [CLR 統合の有効化](../clr-integration/clr-integration-enabling.md)  
  
  
