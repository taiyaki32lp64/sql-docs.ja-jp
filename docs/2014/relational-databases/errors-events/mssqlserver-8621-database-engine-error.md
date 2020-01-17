---
title: MSSQLSERVER_8621 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8621 (Database Engine error)
ms.assetid: 67f59865-becd-4999-8bb0-90aedd7effbf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e4aa55a321f4eea99643ec39cbf5b72682ec7929
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62912882"
---
# <a name="mssqlserver8621"></a>MSSQLSERVER_8621
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|8621|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|OPTIMIZER_STACK_OVERFLOW_ERR|  
|メッセージ テキスト|クエリ プロセッサはクエリ最適化実行中にスタック領域不足になりました。 クエリを簡単にしてください。|  
  
## <a name="explanation"></a>説明  
 このエラーの原因として最も多いのは、クエリのサイズが大きくなったことです。 大きくなったクエリでは、各ビューの定義、計算列、[!INCLUDE[tsql](../../includes/tsql-md.md)] 関数、参照している共通テーブル式や、セカンダリ インデックス、ビュー、およびトリガーの更新などの連鎖動作が、元のクエリに置き換わっています。  
  
 ビュー定義で参照しているテーブルの数や、非常に大きなスカラー式など、特定の項目によりクエリのサイズが大きくなっていることが考えられます。  
  
## <a name="user-action"></a>ユーザーの操作  
 最も大きい項目に関してクエリを複数に分割することにより、クエリを単純化します。 まず不要なクエリ要素を削除し、次に一時テーブルを追加して、クエリを 2 つに分割します。  クエリの一部をサブクエリまたは関数や共通テーブルに移動するだけでは、十分ではありません。これらは [!INCLUDE[tsql](../../includes/tsql-md.md)] コンパイラを実行すると結合されるからです。  
  
  
