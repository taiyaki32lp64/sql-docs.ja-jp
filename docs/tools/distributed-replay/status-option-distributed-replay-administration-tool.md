---
title: status オプション (分散再生管理ツール) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ea89386e-1598-4412-8b37-680d14b2a5b6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6370d68b3575e80c4094aa2df82aa4bf6c0b4dd2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949846"
---
# <a name="status-option-distributed-replay-administration-tool"></a>status オプション (Distributed Replay 管理ツール)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 管理ツールである **DReplay.exe** は、Distributed Replay Controller と通信するために使用できるコマンド ライン ツールです。 このトピックでは、 **status** コマンド ライン オプションとそれに対応する構文について説明します。  
  
 **status** オプションは、コントローラーに照会し、現在の状態を表示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") 管理ツールの構文で使用される構文表記規則の詳細については、「[Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
dreplay status [-m controller] [-f status_interval]  
```  
  
#### <a name="parameters"></a>パラメーター  
 **-m** _controller_  
 コントローラーのコンピューターの名前を指定します。 "`localhost`" または "`.`" を使用してローカル コンピューターを参照できます。  
  
 **-m** パラメーターが指定されていない場合、ローカル コンピューターが使用されます。  
  
 **-f** _status_interval_  
 状態を表示する頻度 (秒単位) を指定します。  
  
 **-f** パラメーターを指定しない場合は、既定の間隔は 30 秒です。  
  
## <a name="examples"></a>使用例  
 次の例では、現在の状態は 60 秒ごとに表示されます。 値 `localhost` は、コントローラー サービスが管理ツールと同じコンピューターで実行されていることを示します。  
  
```  
dreplay status -m localhost -f 60  
```  
  
## <a name="permissions"></a>アクセス許可  
 対話ユーザー (ローカル ユーザーまたはドメイン ユーザー アカウント) として、管理ツールを実行する必要があります。 ローカル ユーザー アカウントを使用するには、管理ツールとコントローラーが同じコンピューター上で実行されている必要があります。  
  
 詳細については、「 [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Transact-SQL デバッガー](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  
