---
title: '[SQL Server エージェントのプロパティ] ([履歴] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.agent.history.f1
ms.assetid: dc73734c-b3c3-407f-bbd1-8714b4fa47b0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 10796dde3513e5c4b7970d1e4f6c4eedcad3c6c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63245585"
---
# <a name="sql-server-agent-properties-history-page"></a>[SQL Server エージェントのプロパティ] ([履歴] ページ)
  このページを使用すると、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス履歴ログの管理設定の表示と設定を行うことができます。  
  
## <a name="options"></a>および  
 **[ジョブ履歴ログのサイズを制限する]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがログで保持するジョブ履歴情報のサイズの上限を設定します。  
  
 **[ジョブ履歴ログの最大サイズ (行)]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによって保持される行の最大数を設定します。 ログの大きさがここで設定した行数に達すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは新しい行を入力するときにログの最も古い行を削除します。  
  
 **[ジョブごとのジョブ履歴の最大行数]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによってジョブごとに保持される行の最大数を設定します。 特定のジョブの履歴サイズがここで設定した行数に達すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは新しい行を入力するときにログの最も古い行を削除します。  
  
 **[エージェントの履歴を削除する]**  
 ログ内のエントリの保存期間が指定された期間を超えたときに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがそのエントリを削除するように指定します。 これは、履歴を削除するために、1 回だけ実行されます。 繰り返し実行する必要がある場合は、クリーンアップ ジョブのメンテナンス プランを作成してスケジュールします。  
  
 **[経過期間]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがエントリを保持する期間を設定します。  
  
## <a name="see-also"></a>参照  
 [SQL Server エージェント エラー ログ](sql-server-agent-error-log.md)  
  
  
