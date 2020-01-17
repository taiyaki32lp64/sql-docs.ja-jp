---
title: c2 audit mode サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- auditing [SQL Server]
- audits [SQL Server], C2 Audit Mode option
- C2 auditing
- C2 Audit Mode option
- recording attempts
ms.assetid: 5a8d73a6-c4f6-4967-ba11-ecbcfc90b9cc
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 52e39eda53e08a4267ac97faa3b691ffcd7acaad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68013002"
---
# <a name="c2-audit-mode-server-configuration-option"></a>c2 audit mode サーバー構成オプション
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  C2 audit mode は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用するか、 **sp_configure** の **c2 audit mode**オプションを使用して構成できます。 このオプションを選択すると、ステートメントやオブジェクトへの失敗したアクセス試行と成功したアクセス試行の両方が記録されるようにサーバーが構成されます。 この情報は、システムの利用状況を把握し、発生する可能性のあるセキュリティ ポリシー違反を追跡するのに役立ちます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] C2 セキュリティ標準に代わって Common Criteria 認定が使用されるようになりました。 「 [common criteria compliance enabled サーバー構成オプション](../../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md)」を参照してください。  
  
## <a name="audit-log-file"></a>監査ログ ファイル  
 C2 audit mode のデータは、インスタンスの既定のデータ ディレクトリにあるファイルに保存されます。 監査ログ ファイルがファイル サイズの上限である 200 (MB) に達すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により新しいファイルが作成され、古いファイルが閉じられて、新しい監査レコードはすべて新しいファイルに書き込まれます。 この処理は、監査データ ディレクトリがいっぱいになるか、または監査が無効になるまで続行されます。 C2 トレースの状態を確認するには、sys.traces カタログ ビューに対してクエリを実行します。  
  
> [!IMPORTANT]  
>  C2 audit mode は、ログ ファイルに大量のイベント情報を保存しますが、このファイルのサイズはすぐに大きくなってしまう可能性があります。 ログ ファイルの保存先データ ディレクトリの領域が不足すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がシャットダウンされます。 監査が自動的に開始するように設定されている場合、(監査をバイパスする) **-f** フラグを指定してインスタンスを再起動するか、または監査ログ用に追加のディスク領域を解放する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="example"></a>例  
 C2 audit mode を有効にする例を次に示します。  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
  
sp_configure 'c2 audit mode', 1 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
## <a name="see-also"></a>参照  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
