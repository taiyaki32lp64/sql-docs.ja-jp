---
title: '[SQL Server エージェント エラー ログの再利用] | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- messages [SQL Server], SQL Server Agent
- errors [SQL Server], logs
- SQL Server Agent, errors
ms.assetid: 0b2d6e6e-cd2d-4b8b-9fa2-2bbd2fc0da41
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1dfa6926d86fce5006e458b3738a28a8b5f467d0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63267388"
---
# <a name="sql-server-agent-error-log"></a>SQL Server エージェント エラー ログ
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントでは、既定で、警告とエラーを記録するエラー ログが作成されます。 次の警告とエラーがログに表示されます。  
  
-   警告メッセージ。"ジョブ \<*job_name*> が実行中に削除されました。" など、潜在的な問題についての情報を提供します。  
  
-   エラー メッセージ。"メール セッションを開始できません。" など、通常はシステム管理者による介入が必要となります。 エラー メッセージは、 **net send**によって、特定のユーザーまたはコンピューターに送信可能です。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、最大 9 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント エラー ログが保持されます。 アーカイブ処理された各ログには、作成順を示す拡張子が付けられます。 たとえば、拡張子 .1 は、それが最も最近アーカイブ処理されたエラー ログであり、拡張子 .9 は、それが一番古いエラー ログであることを示します。  
  
 実行トレース メッセージで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント エラー ログがいっぱいになる可能性があるので、既定では、これらのメッセージはエラー ログに書き込まれません。 エラー ログがいっぱいになった場合、より困難なエラーを選別し分析する能力が低下します。 ログによってサーバーの処理負荷が増加するので、実行トレース メッセージをエラー ログに記録する場合は、その価値を十分に検討することが重要です。 一般に、すべてのメッセージを記録するのは、特定の問題をデバッグするときのみに限定します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが停止している間に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント エラー ログの場所を変更できます。 エラー ログが空の場合は、ログを開くことができません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを停止しなくても [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ログをいつでも使い回すことができます。  
  
 **SQL Server エージェントのエラー ログを表示するには**  
  
-   [View SQL Server Agent Error Log (SQL Server Management Studio)](view-sql-server-agent-error-log-sql-server-management-studio.md) 
  
 **SQL Server エージェント エラー ログの名前を変更するには**  
  
-   [SQL Server エージェントのエラー ログの名前の変更 (SQL Server Management Studio)](rename-a-sql-server-agent-error-log-sql-server-management-studio.md)  
  
 **SQL Server エージェントのエラー メッセージを送信するには**  
  
-   [Send SQL Server Agent Error Messages](send-sql-server-agent-error-messages.md)  
  
 **SQL Server エージェントのエラー ログに実行トレース メッセージを書き込むには**  
  
-   [SQL Server エージェント エラー ログへの実行トレース メッセージの書き込み (SQL Server Management Studio)](write-execution-trace-messages-to-sql-server-agent-log-ssms.md)  
  
  
