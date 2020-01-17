---
title: sysmail_unsentitems (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_unsentitems_TSQL
- sysmail_unsentitems
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_unsentitems database mail view
ms.assetid: 993c12da-41e5-4e53-a188-0323feb70c67
author: stevestein
ms.author: sstein
ms.openlocfilehash: f84e84ed7801beb20bdaca5c92d333133fad3b63
ms.sourcegitcommit: a97d551b252b76a33606348082068ebd6f2c4c8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70745352"
---
# <a name="sysmail_unsentitems-transact-sql"></a>sysmail_unsentitems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  **未送信**または**再試行**中の状態のデータベースメールメッセージごとに1行の情報を格納します。 状態が unsent または retrying のメッセージは、メール キューに残っており、いつでも送信される可能性があります。 メッセージは、次の理由により、**未送信**状態になることがあります。  
  
-   メッセージが新しく、メール キューに挿入されていても、データベース メールが他のメッセージの処理中でこのメッセージに達していない。  
  
-   データベース メール外部プログラムが実行されておらず、メールが送信されていない  
  
 メッセージの**再試行**の状態は次のようになります。  
  
-   データベース メールでメッセージの送信が試行されたが、SMTP メール サーバーに接続できなかった。 この場合、データベース メールでは、メッセージを送信したプロファイルに割り当てられている他のデータベース メール アカウントを使用して、メッセージの送信が引き続き試行されます。 メールを送信できるアカウントがない場合、データベースメールは、**アカウントの再試行待ち時間**パラメーターに構成されている時間が経過するまで待機してから、メッセージの送信を再試行します。 データベースメールは、**アカウントの再試行**回数のパラメーターを使用して、メッセージの送信を試行する回数を決定します。 データベースメールがメッセージを送信しようとしている間は、メッセージの**再試行**状態が保持されます。  
  
 このビューは、送信待ちメッセージの数と、それらのメール キューでの待機時間を確認する場合に使用できます。 通常、**未送信**のメッセージの数は少なくなります。 通常の運用中にベンチマーク テストを行って、その運用に適切な、メッセージ キュー内のメッセージの数を判断してください。  
  
 データベースメールによって処理されるすべてのメッセージを表示するには、 [ &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)を使用します。 失敗した状態のメッセージだけを表示するには、 [ &#40;sysmail_faileditems&#41;transact-sql](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)を使用します。 送信されたメッセージだけを表示するには、 [ &#40;sysmail_sentitems&#41;transact-sql](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**int**|メール キュー内のメール アイテムの識別子。|  
|**profile_id**|**int**|メッセージの送信に使用されたプロファイルの識別子。|  
|**recipients**|**varchar(max)**|メッセージ受信者の電子メール アドレス。|  
|**copy_recipients**|**varchar(max)**|CC としてメッセージのコピーを受け取る受信者の電子メール アドレス。|  
|**blind_copy_recipients**|**varchar(max)**|BCC としてメッセージのコピーを受け取る受信者の電子メール アドレス。この受信者の名前は、メッセージ ヘッダーには表示されません。|  
|**subject**|**nvarchar(510)**|メッセージの件名。|  
|**body**|**varchar(max)**|メッセージの本文。|  
|**body_format**|**varchar(20)**|メッセージの本文の書式。 指定できる値は、 **TEXT**と**HTML**です。|  
|**importance**|**varchar(6)**|メッセージの**重要度**パラメーター。|  
|**sensitivity**|**varchar(12)**|メッセージの**感度**パラメーター。|  
|**file_attachments**|**varchar(max)**|電子メール メッセージに添付されたファイル名の、セミコロン区切りの一覧。|  
|**attachment_encoding**|**varchar(20)**|添付ファイルの種類。|  
|**query**|**varchar(max)**|メール プログラムによって実行されたクエリ。|  
|**execute_query_database**|**sysname**|メール プログラムによってクエリが実行されたデータベース コンテキスト。|  
|**attach_query_result_as_file**|**bit**|値が 0 の場合、クエリの結果が電子メール メッセージ本文内に取り込まれ、本文内容の後に追加されていることを示します。 値が 1 の場合、結果が添付ファイルとして返されたことを示します。|  
|**query_result_header**|**bit**|値が 1 の場合、クエリの結果に列のヘッダーが含まれていることを示します。 値が 0 の場合、クエリの結果に列のヘッダーが含まれていないことを示します。|  
|**query_result_width**|**int**|メッセージの**query_result_width**パラメーター。|  
|**query_result_separator**|**char(1)**|クエリの出力で列の区切りに使用された文字。|  
|**exclude_query_output**|**bit**|メッセージの**exclude_query_output**パラメーター。 詳細については、「 [sp_send_dbmail &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)」を参照してください。|  
|**append_query_error**|**bit**|メッセージの**append_query_error**パラメーター。 0 は、クエリにエラーがあった場合、データベース メールで電子メール メッセージが送信されないことを示します。|  
|**send_request_date**|**datetime**|メッセージがメール キューに挿入された日時。|  
|**send_request_user**|**sysname**|メッセージを送信したユーザー。 これは、メッセージの **[差出人]** フィールドではなく、データベースメールプロシージャのユーザーコンテキストです。|  
|**sent_account_id**|**int**|メッセージの送信に使用されたデータベース メール アカウントの識別子。 このビューでは常に NULL になります。|  
|**sent_status**|**varchar(8)**|データベースメールがメールを送信しようとしていない場合は、**送信**されません。 データベースメールがメッセージの送信に失敗したが、再試行している場合は、**再試行**されます。|  
|**sent_date**|**datetime**|データベース メールでメールの送信が試行された日時。 データベース メールでメッセージの送信が試行されていない場合は NULL になります。|  
|**last_mod_date**|**datetime**|行が最後に変更された日時。|  
|**last_mod_user**|**sysname**|行を最後に変更したユーザー。|  
  
## <a name="remarks"></a>コメント  
 データベース メールのトラブルシューティングを行うとき、このビューでは送信済みのメッセージ数とメッセージの待機時間を確認できるので、問題の性質を特定するのに役立ちます。 メッセージが 1 つも送信されていない場合は、データベース メール外部プログラムが動作していないか、ネットワークの問題によってデータベース メールから SMTP サーバーへの接続に障害が発生している可能性があります。 未送信のメッセージの多くが同じ**profile_id**を持っている場合は、SMTP サーバーに問題がある可能性があります。 この場合は、プロファイルへのアカウントの追加を検討してください。 メッセージが送信されているにもかかわらず、メッセージがキューに過剰[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に時間を費やしている場合は、必要なメッセージの量を処理するためにより多くのリソースが必要になることがあります。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定サーバーロールおよび**databasemailuserrole**データベースロールに付与されます。 **Sysadmin**固定サーバーロールのメンバーによって実行されると、このビューにはすべての**未送信**または**再試行**中のメッセージが表示されます。 他のすべてのユーザーには、送信した**未送信**または**再試行**中のメッセージのみが表示されます。  
  
  
