---
title: sp_monitor (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_monitor_TSQL
- sp_monitor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_monitor
ms.assetid: cb628496-2f9b-40e4-b018-d0831c4cb018
author: stevestein
ms.author: sstein
ms.openlocfilehash: d91f774973588096ea73675d9b0e9ebf6368f1ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022319"
---
# <a name="sp_monitor-transact-sql"></a>sp_monitor (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  に関する統計情報を表示します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_monitor  
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|説明|  
|-----------------|-----------------|  
|**last_run**|時間**sp_monitor**が最後に実行します。|  
|**current_run**|時間**sp_monitor**が実行されています。|  
|**seconds**|経過秒数**sp_monitor**を実行します。|  
|**cpu_busy**|サーバー コンピューターの CPU が実行されている秒数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]動作します。|  
|**io_busy**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が入出力操作に費やした秒数|  
|**アイドル状態します。**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がアイドル状態だった秒数|  
|**packets_received**|入力パケットの数によって読み取られた[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。|  
|**packets_sent**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が書き込んだ出力パケット数|  
|**\@packet_errors**|発生したエラーの数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パケットを読み書き中にします。|  
|**total_read**|読み取り回数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。|  
|**total_write**|書き込み回数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。|  
|**total_errors**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の読み書き中に発生したエラー数|  
|**接続**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] へのログインまたはログイン試行の回数|  
  
## <a name="remarks"></a>コメント  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、いくつかの関数によって処理量が追跡されます。 実行**sp_monitor**これらの関数によって返される現在の値を表示し、プロシージャが実行された最終時刻から変更されている量を示します。  
  
 フォームで、各列の統計情報を印刷*数*(*数*)-*数*% または*数*(*数*). 最初の*数*の秒数を示します (の**cpu_busy**、 **io_busy**、および**アイドル**) または (用、もう一方の合計数変数) ため[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]が再起動されました。 *数*かっこで囲まれた秒数または前回の合計数を指します**sp_monitor**を実行します。 割合からの経過時間の割合が、 **sp_monitor**が最後に実行します。 たとえば、レポートに表示**cpu_busy**として 4250 (215) 68% の場合は、CPU がされてから 4250 ビジー状態の秒[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]から 215 の秒数を最後に起動されて**sp_monitor**最後の実行、およびの 68% が、経過時間の合計**sp_monitor**が最後に実行します。  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のビジー状況に関する情報をレポートします。  
  
```  
USE master  
EXEC sp_monitor  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
||||  
|-|-|-|  
|**last_run**|**current_run**|**seconds**|  
|1998 年 3 月 29 日午前 11:55|1998 年 4 月 4 日午後 2:22|561|  
  
||||  
|-|-|-|  
|**cpu_busy**|**io_busy**|**アイドル状態します。**|  
|190 (0)-0%|187 (0)-0%|148 (556) ~ 99%|  
  
||||  
|-|-|-|  
|**packets_received**|**packets_sent**|**\@packet_errors**|  
|16(1)|20(2)|0(0)|  
  
|||||  
|-|-|-|-|  
|**total_read**|**total_write**|**total_errors**|**接続**|  
|141(0)|54920(127)|0(0)|4(0)|  
  
## <a name="see-also"></a>関連項目  
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
