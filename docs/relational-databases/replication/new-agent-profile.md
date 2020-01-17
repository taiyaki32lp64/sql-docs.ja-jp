---
title: '[新しいエージェント プロファイル] | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.profiles.newperfprofile.f1
helpviewer_keywords:
- New Agent Profile dialog box
ms.assetid: ebf59330-a421-45a5-9020-0484a96852bc
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 10ddecc4e3c81d48a2824eb48e48495e4f2dec1d
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68764939"
---
# <a name="new-agent-profile"></a>[新しいエージェント プロファイル]
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **[新しいエージェント プロファイル]** ダイアログ ボックスを使用すると、新しいプロファイルを作成できます。 新しいプロファイルは常に既存のプロファイルに基づきますが、アプリケーション要件に一致するように変更することもできます。 プロファイルを作成したら、 **[エージェント プロファイル]** ダイアログ ボックスで、既存のエージェントおよび今後のエージェントのジョブに適用できます。 エージェントのパラメーター値は、[\<**AgentProfileName> のプロパティ]** ダイアログ ボックスで編集できます。  
  
## <a name="options"></a>オプション  
 **[名前]**  
 プロファイルの名前を入力します。  
  
 **[説明]**  
 プロファイルの説明を入力します。  
  
 **パラメーター**  
 プロファイルに含まれるエージェント パラメーターです。 新しいプロファイルが基づくプロファイルは、必ずしもパラメーターごとの値を指定する必要はありません。 指定されたエージェントで有効なパラメーターをすべて表示するには、 **[このプロファイルに使用されているパラメーターのみ表示する]** チェック ボックスをオフにします。 各パラメーターの詳細については、次を参照してください。  
  
-   [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
-   [レプリケーション ログ リーダー エージェント](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
-   [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
-   [レプリケーション マージ エージェント](../../relational-databases/replication/agents/replication-merge-agent.md)  
  
-   [レプリケーション キュー リーダー エージェント](../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
 **既定値**  
 各エージェント パラメーターの既定値です。  
  
 **値**  
 新しいプロファイルが基づくプロファイル内のパラメーターに対して指定された値です。 パラメーター値を変更するには、このフィールドを編集します。  
  
 **[このプロファイルに使用されているパラメーターのみ表示する]**  
 指定されたエージェントに有効なパラメーターをすべて表示するにはオフにします。  
  
## <a name="see-also"></a>参照  
 [レプリケーション エージェント プロファイルの操作](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [レプリケーション エージェントの概要](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [レプリケーション エージェント プロファイル](../../relational-databases/replication/agents/replication-agent-profiles.md)  
  
  
