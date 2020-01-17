---
title: '[T-SQL ステートメントの実行タスク] (メンテナンス プラン) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.tsql.f1
helpviewer_keywords:
- Execute T-SQL Statement Task dialog box
ms.assetid: fef3e259-0c47-4f6e-ade0-aee95e3d6c1a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: aac0c6b837fcd25b0e1f06344a2745c68b05dea3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206034"
---
# <a name="execute-t-sql-statement-task-maintenance-plan"></a>[T-SQL ステートメントの実行タスク] \(メンテナンス プラン)
  **[T-SQL ステートメントの実行タスク]** ダイアログを使用すると、適切な [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントをこのメンテナンス プランに追加して、メンテナンス プランをカスタマイズできます。  
  
## <a name="options"></a>および  
 **Connection**  
 このタスクを実行するときに使用するサーバー接続を選択します。  
  
 **[新規作成]**  
 このタスクを実行するときに使用する新しいサーバー接続を作成します。 **[新しい接続]** ダイアログ ボックスについては、後で説明します。  
  
 **[実行タイムアウト]**  
 タイムアウトする (タスクが終了する) までタスクの完了を待機する時間 (秒) です。  
  
 **[T-SQL ステートメント]**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 実行する  ステートメントです。  
  
 **[T-SQL の表示]**  
 選択したオプションに基づき、このタスクでサーバーに対して実行される [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを表示します。  
  
> [!NOTE]  
>  影響を受けるオブジェクトが大量にある場合は、表示にかなりの時間を要する場合があります。  
  
## <a name="new-connection-dialog-box"></a>[新しい接続] ダイアログ ボックス  
 **[接続名]**  
 新しい接続の名前を入力します。  
  
 **[サーバー名の選択または入力]**  
 このタスクを実行するときに接続するサーバーを選択します。  
  
 **[更新]**  
 使用できるサーバーの一覧を表示します。  
  
 **[サーバーにログオンするための情報の入力]**  
 サーバーの認証情報を指定します。  
  
 **[Windows NT の統合セキュリティを使用する]**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] のインスタンスに接続します。  
  
 **[特定のユーザー名とパスワードを使用する]**  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 認証を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続します。 このオプションは利用できません。  
  
 **ユーザー名**  
 認証に使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。 このオプションは利用できません。  
  
 **Password**  
 認証に使用するパスワードを指定します。 このオプションは利用できません。  
  
  
