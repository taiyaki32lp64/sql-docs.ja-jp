---
title: sysmail_event_log (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_event_log
- sysmail_event_log_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_event_log database mail view
ms.assetid: 440bc409-1188-4175-afc4-c68e31e44fed
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4241ac9a457aa51f32ec12e9b1d8b83aa534995e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060226"
---
# <a name="sysmaileventlog-transact-sql"></a>sysmail_event_log (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベース メール システムから返される、Windows または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のメッセージごとに 1 行のデータを格納します。 (このコンテキストでメッセージが電子メール メッセージではなく、エラー メッセージなどのメッセージを参照)。構成、**ログ記録レベル**パラメーターを使用して、**システム パラメーターの構成**、データベース メール構成ウィザードのダイアログ ボックスまたは[sysmail_configure_sp](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md)ストアド プロシージャをどのメッセージを返すかを判断します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**Log_id**|**int**|ログ内のアイテムの識別子。|  
|**event_type**|**varchar(11)**|ログに挿入された通知の種類。 使用可能な値は、エラー、警告、情報メッセージ、成功メッセージ、およびその他の内部メッセージです。|  
|**log_date**|**datetime**|ログ エントリが作成された日時。|  
|**description**|**nvarchar(max)**|記録されたメッセージのテキスト。|  
|**process_id**|**int**|データベース メール外部プログラムのプロセス id。 通常、データベース メール外部プログラムが起動するたびに変更されます。|  
|**mailitem_id**|**int**|メール キュー内のメール アイテムの識別子。 メッセージが特定の電子メール アイテムに関係していない場合は NULL になります。|  
|**account_id**|**int**|**Account_id**のイベントに関連するアカウント。 メッセージが特定のアカウントに関連付けられていない場合は NULL です。|  
|**last_mod_date**|**datetime**|行が最後に変更された日時。|  
|**last_mod_user**|**sysname**|行を最後に変更したユーザー。 電子メールの場合、メールを送信したユーザーになります。 データベース メール外部プログラムによって生成されたメッセージの場合これは、プログラムのユーザー コンテキストです。|  
  
## <a name="remarks"></a>コメント  
 データベース メールのトラブルシューティングを行うときは、検索、 **sysmail_event_log**電子メールの失敗に関連のイベントを表示します。 データベース メール外部プログラムの障害など、一部のメッセージは、特定の電子メールに関連付けられていません。 特定の電子メールに関連するエラーを検索するを検索、 **mailitem_id**に失敗した電子メールの**sysmail_faileditems**を表示し、検索、 **sysmail_event_log**に関連するメッセージの**mailitem_id**します。 エラーが返される場合**sp_send_dbmail**、データベース メール システムに電子メールが送信されていないと、エラーは、このビューでは表示されません。  
  
 個々のアカウントで配信試行が失敗した場合は、再試行の間、メール アイテムの配信が成功または失敗するまで、データベース メールでエラー メッセージが保持されます。 含む個別の警告として記録されるすべての蓄積されたエラー、成功した場合、 **account_id**します。 電子メールは送信されても警告が表示される場合、原因になります。 せず 1 つのエラー メッセージとして記録されるまでの警告はすべて最終的な配信の失敗した場合、 **account_id**、すべてのアカウントが失敗したためです。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーである必要がありますが、 **sysadmin**固定サーバー ロールまたは**DatabaseMailUserRole**このビューにアクセスするデータベース ロール。 メンバーの**DatabaseMailUserRole**のメンバーでないユーザー、 **sysadmin**ロールは送信メールのイベントのみを表示できます。  
  
## <a name="see-also"></a>関連項目  
 [sysmail_faileditems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [データベース メール外部プログラム](../../relational-databases/database-mail/database-mail-external-program.md)  
  
  
