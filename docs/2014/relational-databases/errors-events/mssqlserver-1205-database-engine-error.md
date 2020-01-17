---
title: MSSQLSERVER_1205 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1205 (Database Engine error)
ms.assetid: 9fe3f67c-df3c-4642-a3a4-ccc0e138b632
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ef8a59c98bc6669a13b5a4ffeb516b4063db23c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62915900"
---
# <a name="mssqlserver1205"></a>MSSQLSERVER_1205
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|1205|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|LK_VICTIM|  
|メッセージ テキスト|トランザクション (プロセス ID %d) が、%.*ls 個のリソースで他のプロセスとデッドロックして、このトランザクションがそのデッドロックの対象となりました。 トランザクションを再実行してください。|  
  
## <a name="explanation"></a>説明  
 別々のトランザクションで、リソースへのアクセス順序が競合し、デッドロックが生じました。 以下に例を示します。  
  
-   Transaction2 が **Table2.Row2** を更新している間に、Transaction1 が **Table1.Row1** を更新しました。  
  
-   Transaction1 は **Table2.Row2** を更新しようとしましたが、Transaction2 のコミットがまだなので、ブロックされました。  
  
-   今度は Transaction2 が **Table1.Row1** を更新しようとしましたが、Transaction1 のコミットがまだなので、ブロックされました。  
  
-   Transaction1 が Transaction2 の完了を待機していますが、Transaction2 は Transaction1 の完了を待機しているので、デッドロックが生じました。  
  
 システムがこのデッドロックを検出すると、いずれか一方のトランザクションがデッドロックの対象に選ばれ、そのトランザクションがロールバックされます。  
  
## <a name="user-action"></a>ユーザーの操作  
 トランザクションを再実行します。 また、デッドロックを回避できるようにアプリケーションを修正します。 デッドロック対象として選択されたトランザクションは、再試行が可能です。同時に実行されている操作によって状況が異なりますが、再試行は成功する可能性があります。  
  
 デッドロックを回避するには、すべてのトランザクションから行に対するアクセスが、同じ順序 (**Table1** の次に **Table2** など) で行われるようにすることを検討します。こうすることで、ブロックが発生しても、デッドロックは発生しません。  
  
  
