---
title: disallow results from triggers サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], result sets
- result sets [SQL Server], triggers
- disallow results from triggers option
ms.assetid: 47149073-307d-47a5-b7d2-66a737d3231d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 28bf3b201d54798f26c9e887e86a9d0bed78ee15
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68011862"
---
# <a name="disallow-results-from-triggers-server-configuration-option"></a>disallow results from triggers サーバー構成オプション
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **disallow results from triggers** オプションは、トリガーによって結果セットを返すかどうかを制御する場合に使用します。 結果セットを返すトリガーは、それと連動するように設計されていないアプリケーションでは予期しない動作を起こすことがあります。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]この値は 1 に設定することをお勧めします。  
  
 1 に設定すると、 **disallow results from triggers** オプションが ON になります。 このオプションの既定値は 0 (OFF) です。 このオプションを 1 (ON) に設定した場合は、トリガーによって結果セットを返そうとするとエラーになり、次のエラー メッセージが出力されます。  
  
 "メッセージ 524、レベル 16、状態 1、プロシージャ \<プロシージャ名>、行 \<行番号>  
  
 "トリガーから結果セットが返されましたが、サーバー オプション 'disallow_results_from_triggers' は true です。"  
  
 **disallow results from triggers** オプションは [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス レベルで適用され、インスタンス内のすべての既存のトリガーの動作を決定します。  
  
 **disallow results from triggers** は拡張オプションです。 **sp_configure** システム ストアド プロシージャを使用して disallow results from triggers の設定を変更するには、 **show advanced options** を 1 に設定する必要があります。 新しい設定は、サーバーを再起動しなくてもすぐに有効になります。  
  
## <a name="see-also"></a>参照  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
