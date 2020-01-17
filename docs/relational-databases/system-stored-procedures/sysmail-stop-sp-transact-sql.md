---
title: sysmail_stop_sp (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_stop_sp_TSQL
- sysmail_stop_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_stop_sp
ms.assetid: 045ee36f-5bf0-4626-b5ee-e84db06ce16f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 753375d139a03d5c0cec20dc994d83399e04f094
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037401"
---
# <a name="sysmailstopsp-transact-sql"></a>sysmail_stop_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  停止することで、データベース メールを停止、[!INCLUDE[ssSB](../../includes/sssb-md.md)]外部プログラムが使用するオブジェクト。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_stop_sp  
```  
  
## <a name="arguments"></a>引数  
 なし  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 このストアド プロシージャは、 **msdb**データベース。  
  
 このストアド プロシージャは、送信メッセージ要求を保持し、オフにするデータベース メール キューを停止します。[!INCLUDE[ssSB](../../includes/sssb-md.md)]外部プログラムのライセンス認証します。  
  
 キューが停止したら、データベース メール外部プログラムはメッセージを処理しません。 このストアド プロシージャを使用すると、トラブルシューティングやメンテナンスの目的でデータベース メールを停止できます。  
  
 データベース メールを開始するには使用**sysmail_start_sp**します。 注意**sp_send_dbmail**もメール、[!INCLUDE[ssSB](../../includes/sssb-md.md)]オブジェクトを停止します。  
  
> [!NOTE]  
>  このストアド プロシージャでは、データベース メールのキューのみ停止します。 このストアド プロシージャは非アクティブ化できません[!INCLUDE[ssSB](../../includes/sssb-md.md)]メッセージ データベースに配信します。 このストアド プロシージャは、画面の領域を削減するデータベース メール拡張ストアド プロシージャを無効にできません。 拡張ストアド プロシージャを無効にするを参照してください、 [Database Mail XPs オプション](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md)の**sp_configure**システム ストアド プロシージャ。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの既定のメンバーへのアクセス許可を実行、 **sysadmin**固定サーバー ロール。  
  
## <a name="examples"></a>使用例  
 データベース メールを停止する次の例を示しています、 **msdb**データベース。 例では、データベース メールが有効になっていると仮定します。  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sysmail_stop_sp ;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [sysmail_start_sp &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql.md)   
 [データベース メール ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
