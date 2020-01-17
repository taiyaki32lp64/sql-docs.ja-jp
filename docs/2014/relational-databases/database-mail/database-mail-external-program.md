---
title: データベース メール外部プログラム | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- external programs [Database Mail]
- DatabaseMail90.exe
- Database Mail [SQL Server], external programs
ms.assetid: bc124164-eb6e-4b7f-bf66-98a3113d02f7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6c617e4f7c069a869935fa4ed83d28c02d0b0b9a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62917643"
---
# <a name="database-mail-external-program"></a>データベース メール外部プログラム
  データベース メール外部実行可能ファイルは **DatabaseMail.exe**です。このファイルは、 **インストール環境の** MSSQL\Binn ディレクトリ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にあります。 データベース メールでは、処理する電子メール メッセージがあるときに、Service Broker のアクティブ化を使用して外部プログラムが起動されます。 次に、データベース メールによって外部プログラムの 1 つのインスタンスが開始されます。 外部プログラムは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のサービス アカウントのセキュリティ コンテキストで実行されます。  
  
 **このトピックの内容**  
  
-   [データベース メール外部プログラムの概念](#ComponentsAndConcepts)  
  
-   [データベース メール外部プログラムの構成に関連するタスク](#RelatedTasks)  
  
##  <a name="ComponentsAndConcepts"></a> データベース メール外部プログラムの概念  
 外部プログラムが開始されるときに、プログラムによって Windows 認証を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続が行われ、電子メール メッセージの処理が開始されます。 指定されたタイムアウト期間内に送信するメッセージがなくなると、プログラムが終了します。 データベース メール構成ウィザードまたはデータベース メール ストアド プロシージャのいずれかを使用して、プログラムが終了するまでの時間を構成できます。 詳細については、「 [sysmail_configure_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql)のサービス アカウントのセキュリティ コンテキストで実行されます。  
  
 外部プログラムは、 **msdb** データベースのシステム テーブルに情報を保存します。 外部プログラムが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と通信できない場合は、プログラムによって、Microsoft Windows アプリケーション イベント ログにエラーが記録されます。 **データベース メール構成ウィザード** の **[システム パラメーターの構成]** ダイアログ ボックスでログのレベルを **[詳細]** に設定している場合、詳細なメッセージ ログが記録されます。  
  
 外部プログラムでは、効率を上げるために、アカウントやプロファイルに関する情報がキャッシュされることに注意してください。 そのため、アカウントやプロファイルの構成を変更しても、その変更が数分間、外部プログラムに反映されないことがあります。  
  
##  <a name="RelatedTasks"></a> データベース メール外部プログラムの構成に関連するタスク  
  
|構成タスク|トピック|  
|------------------------|----------------|  
|外部プログラムが終了するまでの時間を指定します。|[sysmail_configure_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql)|  
  
## <a name="see-also"></a>参照  
 [SQL Server Service Broker (SQL Server Service Broker)](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [データベース メールのログ記録と監査](database-mail-log-and-audits.md)   
 [データベース メール](database-mail.md)  
  
  
