---
title: データベース メール メッセージング オブジェクト | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], host databases
- Database Mail [SQL Server], messaging objects
- mail host databases [SQL Server]
- host databases [Database Mail]
ms.assetid: 5aa2886e-1db1-4066-85df-57ccf4538c54
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8eb132920a6b51303e5725ecdb770dd742972f42
ms.sourcegitcommit: df1f71231f8edbdfe76e8851acf653c25449075e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2019
ms.locfileid: "70809949"
---
# <a name="database-mail-messaging-objects"></a>データベース メール メッセージング オブジェクト
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **msdb** データベースはデータベース メール ホスト データベースです。 このデータベースには、データベース メールのストアド プロシージャやメッセージング オブジェクトが格納されます。 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] にはデータベース メール構成ウィザードが付属していて、データベース メールの有効化、プロファイルとアカウントの作成と管理、およびデータベース メール オプションの構成をこのウィザードから行うことができます。  
  
##  <a name="ComponentsAndConcepts"></a>**msdb** データベース内にあるオブジェクト  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] msdb **データベースで、** を有効にする必要があります。 ただし、データベース メールでは [!INCLUDE[ssSB](../../includes/sssb-md.md)] ネットワークを使用しません。 そのため、ユーザーはデータベース メールを使用するための [!INCLUDE[ssSB](../../includes/sssb-md.md)] エンドポイントを作成する必要はありません。 データベース メールの外部プロセスでは、 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] との通信に標準の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]接続が使用されます。  
  
 データベース メールが有効になっていると、 **msdb** データベース内の次のオブジェクトがデータベース メールによって公開されます。  
  
 これらのオブジェクトは、メール ホスト データベース内のデータベース メールのインターフェイスです。 上記で一覧したオブジェクトによって提供される機能を実装するために、他のオブジェクトがインストールされます。 ただし、このようなオブジェクトは内部使用のために予約されています。  
  
|[オブジェクト名]|型|[説明]|  
|----------|----------|-----------------|  
|[sysmail_allitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)|**[表示]**|データベース メールに送信されたすべてのメッセージの一覧を表示します。|  
|[sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)|**[表示]**|[Database Mail External Program](../../relational-databases/database-mail/database-mail-external-program.md)の動作に関するメッセージの一覧を表示します。|  
|[sysmail_faileditems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)|**[表示]**|データベース メールで送信できなかったメッセージに関する情報を表示します。|  
|[sysmail_mailattachments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md)|**[表示]**|データベース メール メッセージの添付ファイルに関する情報を表示します。|  
|[sysmail_sentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)|**表示**|データベース メールを使用して送信されたメッセージに関する情報を表示します。|  
|[sysmail_unsentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md)|**[表示]**|データベース メールで現在送信が試行されているメッセージに関する情報を表示します。|  
|[sp_send_dbmail &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)|**ストアド プロシージャ**|データベース メールを使用して、電子メール メッセージを送信します。|  
|[sysmail_delete_log_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md)|**ストアド プロシージャ**|データベース メール ログからメッセージを削除します。|  
|[sysmail_delete_mailitems_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)|**ストアド プロシージャ**|メール アイテムをデータベース メール キューから削除します。|  
|[sysmail_help_status_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-help-status-sp-transact-sql.md)|**ストアド プロシージャ**|データベース メールが開始されているかどうかを示します。|  
|[sysmail_start_sp (Transact-SQL)](../../relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql.md)|**ストアド プロシージャ**|外部プログラムによって使用される Service Broker オブジェクトを開始します。 これらのオブジェクトは、既定で開始されます。|  
|[sysmail_stop_sp (Transact-SQL)](../../relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql.md)|**ストアド プロシージャ**|外部プログラムによって使用される Service Broker オブジェクトを停止します。|  
  
  
## <a name="see-also"></a>参照  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [SQL Server Service Broker (SQL Server Service Broker)](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
