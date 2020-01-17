---
title: データベース メールのログ記録と監査 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- auditing [SQL Server]
- Database Mail [SQL Server], auditing
- logs [Database Mail]
- audits [SQL Server], Database Mail
- Database Mail [SQL Server], logging
ms.assetid: 846589ee-5fe5-4ab3-b335-0c253e569f99
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e500eb47af39502e1bcf59f60b3dd24fed0713fa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62872129"
---
# <a name="database-mail-log-and-audits"></a>データベース メールのログ記録と監査
  データベース メールのログ記録機能は、問題の特定および修正の手段を提供する目的でデザインされました。 データベース メールは、 **msdb** データベースにログ情報を格納します。 データベース メールの電子メールの内容、電子メールの状態、エラーなどの受信メッセージがデータベース メールによってログに記録され、トラブルシューティングや監査のために使用できます。  
  
## <a name="database-mail-logs"></a>データベース メールのログ  
 [データベース メール外部プログラム](database-mail-external-program.md)の **msdb** データベース ログ情報の表。 [データベース メール ビュー &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/database-mail-views-transact-sql) は、トラブルシューティング用のテーブルを公開します。 Service Broker によって外部プログラムをアクティブにできない場合、外部プログラムでネットワーク エラーが発生した場合、簡易メール転送プロトコル (SMTP) サーバーで電子メール メッセージが拒否された場合などに、エラーが [sysmail_event_log &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sysmail-event-log-transact-sql) ビューに表示されます。 外部プログラムが **msdb** テーブルにログを記録できない場合は、Windows アプリケーション イベント ログにエラーが記録されます。  
  
 **msdb** データベースの内部テーブルには、データベース メールから送信された電子メール メッセージと添付ファイルが各メッセージの現在の状態と共に格納されます。 メッセージが処理されるたびに、データベース メールによってこれらのテーブルが更新されます。  
  
## <a name="database-mail-auditing-tasks"></a>データベース メールの監査タスク  
  
|||  
|-|-|  
|**データベース メールのログの確認と管理**|**トピックへのリンク**|  
|個々のメッセージの配信状態の確認|[データベース メールから送信された電子メール メッセージの状態の確認](check-the-status-of-e-mail-messages-sent-with-database-mail.md)|  
|データベース メールのメッセージ、添付ファイル、およびログ エントリのクリーンアップ|[sysmail_delete_mailitems_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql)<br /><br /> [sysmail_delete_log_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql)|  
|データベース メールのメッセージとログのアーカイブ|[データベース メール メッセージやイベント ログをアーカイブする SQL Server エージェント ジョブの作成](create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)|  
  
## <a name="see-also"></a>関連項目  
 [リソースの利用状況の監視 &#40;システム モニター&#41;](../performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
