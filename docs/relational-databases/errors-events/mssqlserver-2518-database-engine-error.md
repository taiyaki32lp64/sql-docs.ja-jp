---
title: MSSQLSERVER_2518 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2518 (Database Engine error)
ms.assetid: 54a13abc-4c33-43f0-b55d-e2e74a1381c8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ca6a654894304197357cbe244be60f9b9a58f789
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138511"
---
# <a name="mssqlserver2518"></a>MSSQLSERVER_2518
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|2518|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC_NO_EXPRESSION_EVAL_CLR_DISABLED|  
|メッセージ テキスト|オブジェクト ID O_ID (オブジェクト "O_NAME"):共通言語ランタイム (CLR) が無効になっているので、このオブジェクトでは計算列とユーザー定義型を確認できません。|  
  
## <a name="explanation"></a>説明  
この情報メッセージは、クエリ プロセッサが、計算列と共通言語ランタイム (CLR) のユーザー定義型を評価するための内部オブジェクトを DBCC に提供できなかったことを示しています。 この問題は、いずれかの列に CLR が関係しているにもかかわらず、CLR が有効化されていないために発生しました。 内部オブジェクトはすべての列に及んでいます。 このため、1 つの列を評価できないと、内部オブジェクトの作成ができなくなります。 つまり、計算列の正当性チェックが行われなかったり、DBCC でインデックスとベース テーブルの整合性をチェックする際に計算列が使用されないことを意味します。  
  
## <a name="user-action"></a>ユーザーの操作  
CLR を有効にして、DBCC ステートメントを再実行します。  
  
## <a name="see-also"></a>参照  
[CLR 統合の有効化](~/relational-databases/clr-integration/clr-integration-enabling.md)  
  
