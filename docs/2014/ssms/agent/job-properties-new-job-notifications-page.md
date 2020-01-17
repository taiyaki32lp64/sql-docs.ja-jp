---
title: ジョブのプロパティ:新しいジョブ (通知 ページ) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.job.notifications.f1
ms.assetid: ed393cbd-4496-4399-a177-e5baa92fb689
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 10cee6f0d5bf62178c71d25b8eb5682c22bbbe3b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68189240"
---
# <a name="job-properties-new-job-notifications-page"></a>[ジョブのプロパティ]:[新しいジョブ] ([通知] ページ)
  このページを使用すると、ジョブの完了時に [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行するアクションを設定します。  
  
## <a name="options"></a>および  
 **[電子メール]**  
 このオプションを選択すると、ジョブの完了時に電子メールが送信されます。 このオプションを選択した後、通知先のオペレーターと、次の通知をトリガーする条件を選択します。 **[ジョブ成功時]** 、 **[ジョブ失敗時]** 、または **[ジョブ完了時]** 。  
  
 **ページ**  
 このオプションを選択すると、ジョブの完了時にオペレーターのポケットベルに電子メールが送信されます。 このオプションを選択した後、通知先のオペレーターと、次の通知をトリガーする条件を指定します。 **[ジョブ成功時]** 、 **[ジョブ失敗時]** 、または **[ジョブ完了時]** 。  
  
 **Net send**  
 このオプションを選択すると、ジョブの完了時に Net Send を使用してオペレーターに通知が送られます。 このオプションを選択した後、通知先のオペレーターと、次の通知をトリガーする条件を指定します。 **[ジョブ成功時]** 、 **[ジョブ失敗時]** 、または **[ジョブ完了時]** 。  
  
 **[Windows アプリケーション イベント ログに書き込む]**  
 このオプションを選択すると、ジョブの完了時にアプリケーション イベント ログにエントリが書き込まれます。 このオプションを選択した後、通知先のオペレーターと、次の通知をトリガーする条件を指定します。 **[ジョブ成功時]** 、 **[ジョブ失敗時]** 、または **[ジョブ完了時]** 。  
  
 **[自動的にジョブを削除]**  
 このオプションを選択すると、ジョブの完了時にジョブが削除されます。 このオプションを選択した後、ジョブの削除をトリガーする条件を指定します。 **[ジョブ成功時]** 、 **[ジョブ失敗時]** 、または **[ジョブ完了時]** 。  
  
## <a name="see-also"></a>関連項目  
 [ジョブの実装](implement-jobs.md)   
 [データベース メールを使用するように SQL Server エージェント メールを構成する](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)  
  
  
