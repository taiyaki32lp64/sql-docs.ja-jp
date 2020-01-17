---
title: SQL Server エージェントのプロパティ ([詳細設定] ページ) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.agent.advanced.f1
ms.assetid: a4d798ee-4c18-40d4-b6af-63d17503738c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aeb0c6c47a9203a7124fbe5d9f4739c52ae430d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63246238"
---
# <a name="sql-server-agent-properties-advanced-page"></a>[SQL Server エージェントのプロパティ] \([詳細設定] ページ)
  このページを使用すると、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスの詳細プロパティを表示および変更できます。  
  
## <a name="options"></a>および  
 **[SQL Server イベントの転送]**  
 このカテゴリのオプションを使用して、イベントの転送をアクティブにしたり、構成したりします。  
  
 **[イベントを別のサーバーに転送する]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント イベントを別のサーバーに転送します。  
  
 **[サーバー]**  
 イベントの転送先のサーバー名を選択します。  
  
 **[未処理のイベント]**  
 未処理のイベントのみを指定のサーバーに転送します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、警告が返されないイベントのみを転送します。  
  
 **[すべてのイベント]**  
 すべてのイベントを転送します。 ローカル インスタンスの警告がイベントに応答した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントはイベントの転送と警告の処理の両方を行います。  
  
 **[次のレベル以上のイベント発生時]**  
 指定された重大度レベル以上のイベントのみを転送します。  
  
 **[CPU のアイドル状態]**  
 このカテゴリのオプションは、CPU のアイドル スケジュールで実行がスケジュールされたジョブを、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行するための条件を定義します。  
  
 **[CPU のアイドル状態を定義する]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントにより CPU がアイドル状態であると見なされる条件を定義します。  
  
 **[CPU の平均使用量が次の値以下になったとき]**  
 CPU がアイドル状態であると見なされる CPU の使用量の割合です。  
  
 **[かつ、この使用率以下で次の期間を経過]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが CPU のアイドル スケジュールのジョブを実行する前に、CPU の平均使用量が指定されたレベルを下回っていなければならない時間です。  
  
## <a name="see-also"></a>参照  
 [作成し、スケジュールをジョブにアタッチ](create-and-attach-schedules-to-jobs.md)   
 [イベントの管理](manage-events.md)  
  
  
