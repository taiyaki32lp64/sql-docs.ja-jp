---
title: SQL Server エージェント テーブル (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server Agent, system tables
- system tables [SQL Server], SQL Server Agent
ms.assetid: 6cb39bfd-079e-4be4-9c42-2fa234c65ce1
author: stevestein
ms.author: sstein
ms.openlocfilehash: fcc811542ad0b7884b703a02b4c983b8752ba200
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130585"
---
# <a name="sql-server-agent-tables-transact-sql"></a>SQL Server エージェントのテーブル (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  ここでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントで使用される情報を格納するシステム テーブルについて説明します。 すべてのテーブルは、msdb データベースの dbo スキーマにです。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [dbo.sysalerts](../../relational-databases/system-tables/dbo-sysalerts-transact-sql.md)  
 警告 1 件につき 1 行のデータを格納します。  
  
 [dbo.syscategories](../../relational-databases/system-tables/dbo-syscategories-transact-sql.md)  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で、ジョブ、警告、オペレーターの分類に使用されるカテゴリを格納します。  
  
 [dbo.sysdownloadlist](../../relational-databases/system-tables/dbo-sysdownloadlist-transact-sql.md)  
 すべてのターゲット サーバーに対するダウンロード命令のキューを格納します。  
  
 [dbo.sysjobactivity](../../relational-databases/system-tables/dbo-sysjobactivity-transact-sql.md)  
 現在の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブに関する利用状況と状態の情報を格納します。  
  
 [dbo.sysjobhistory](../../relational-databases/system-tables/dbo-sysjobhistory-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントで実行予定のジョブに関する情報を格納します。  
  
 [dbo.sysjobs](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによる実行が予定されているジョブに関する情報を格納します。  
  
 [dbo.sysjobschedules](../../relational-databases/system-tables/dbo-sysjobschedules-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによって実行されるジョブのスケジュール情報を格納します。  
  
 [dbo.sysjobservers](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)  
 特定のジョブと 1 つ以上のターゲット サーバーとの関連付けまたはリレーションシップを格納します。  
  
 [dbo.sysjobsteps](../../relational-databases/system-tables/dbo-sysjobsteps-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによって実行されるジョブ内の各ステップに関する情報を格納します。  
  
 [dbo.sysjobstepslogs](../../relational-databases/system-tables/dbo-sysjobstepslogs-transact-sql.md)  
 ジョブ ステップ ログに関する情報を格納します。  
  
 [dbo.sysnotifications](../../relational-databases/system-tables/dbo-sysnotifications-transact-sql.md)  
 通知ごとに 1 行のデータを格納します。  
  
 [dbo.sysoperators](../../relational-databases/system-tables/dbo-sysoperators-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのオペレーターごとに 1 行のデータを格納します。  
  
 [dbo.sysproxies](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのプロキシ アカウントに関する情報を格納します。  
  
 [dbo.sysproxylogin](../../relational-databases/system-tables/dbo-sysproxylogin-transact-sql.md)  
 各 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント プロキシ アカウントに関連付けられている、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のログインを記録します。  
  
 [dbo.sysproxysubsystem](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)  
 各プロキシ アカウントで、どの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのサブシステムが使用されているかを記録します。  
  
 [dbo.sysschedules](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブ スケジュールに関する情報を格納します。  
  
 [dbo.syssessions](../../relational-databases/system-tables/dbo-syssessions-transact-sql.md)  
 各 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのセッションに対する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの開始日を格納します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのサービスが開始されるたびに、セッションが作成されます。  
  
 [dbo.syssubsystems](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)  
 使用可能なすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのプロキシ サブシステムに関する情報を格納します。  
  
 [dbo.systargetservergroupmembers](../../relational-databases/system-tables/dbo-systargetservergroupmembers-transact-sql.md)  
 マルチサーバー グループに現在参加しているターゲット サーバーを記録します。  
  
 [dbo.systargetservergroups](../../relational-databases/system-tables/dbo-systargetservergroups-transact-sql.md)  
 マルチサーバー環境に現在参加しているターゲット サーバー グループを記録します。  
  
 [dbo.systargetservers](../../relational-databases/system-tables/dbo-systargetservers-transact-sql.md)  
 マルチサーバー操作ドメインに現在参加しているターゲット サーバーを記録します。  
  
 [dbo.systaskids](../../relational-databases/system-tables/dbo-systaskids-transact-sql.md)  
 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で作成されたタスクと、現在のバージョンの [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ジョブとのマッピングを格納します。  
  
  
