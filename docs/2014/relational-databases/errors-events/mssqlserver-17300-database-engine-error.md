---
title: MSSQLSERVER_17300 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17300 (Database Engine error)
ms.assetid: c1d6bfb6-28af-4df6-8087-25807602d282
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a6577ec13cc990eb65d66eb2975d61b5f1147201
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62915351"
---
# <a name="mssqlserver17300"></a>MSSQLSERVER_17300
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|17300|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|PROC_OUT_OF_SYSTASK_SESSIONS|  
|メッセージ テキスト|メモリが不足しているか、構成されているセッション数がこのサーバーで許可されている最大数を超えているので、SQL Server で新しいシステム タスクを実行できませんでした。 サーバーに十分なメモリがあることを確認してください。 ユーザー接続の許容最大数を確認するにはオプション 'user connections' を指定して sp_configure を使用してください。 ユーザー プロセスを含めた現在のセッション数を確認するには sys.dm_exec_sessions を使用してください。|  
  
## <a name="explanation"></a>説明  
 メモリが不足しているか、サーバーに構成されているセッション数を超えたため、新しいシステム タスクを実行できませんでした。  
  
## <a name="user-action"></a>ユーザーの操作  
 サーバーに十分なメモリがあることを確認してください。 sys.dm_exec_sessions を使用して現在のシステム タスク数を確認し、sp_configure を使用してユーザー接続の最大数の構成値を確認します。  
  
 必要に応じて、次のタスクを実行します。  
  
-   サーバーにメモリを追加します。  
  
-   1 つ以上のセッションを終了します。  
  
-   サーバー上で許可されるユーザー接続の最大数を増やします。  
  
## <a name="see-also"></a>関連項目  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql)   
 [User connections サーバー構成オプションを構成します。](../../database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md)   
 [KILL &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/kill-transact-sql)  
  
  
