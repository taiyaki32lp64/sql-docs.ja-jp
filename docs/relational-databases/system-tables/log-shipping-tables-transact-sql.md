---
title: ログ配布テーブル (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- log shipping [SQL Server], system tables
- system tables [SQL Server], log shipping
ms.assetid: f8910aae-2013-4645-880c-134577cbcbe0
author: stevestein
ms.author: sstein
ms.openlocfilehash: f36b2f6f52b87fb844bbe9ccb5604f2c4056b15d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68095736"
---
# <a name="log-shipping-tables-transact-sql"></a>ログ配布テーブル (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  次のトピックでは、ログ配布操作で使用される情報を格納するシステム テーブルについて説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [log_shipping_monitor_alert](../../relational-databases/system-tables/log-shipping-monitor-alert-transact-sql.md)  
 警告のログ配布ジョブの Id を格納します。  
  
 [log_shipping_monitor_error_detail](../../relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql.md)  
 ログ配布ジョブのエラーの詳細を格納します。  
  
 [log_shipping_monitor_history_detail](../../relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql.md)  
 ログ配布ジョブの履歴の詳細を格納します。  
  
 [log_shipping_monitor_primary](../../relational-databases/system-tables/log-shipping-monitor-primary-transact-sql.md)  
 各ログ配布構成内のプライマリ データベースごとに、1 つの監視レコードを格納します。  
  
 [log_shipping_monitor_secondary](../../relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql.md)  
 ログ配布構成におけるセカンダリ データベースごとに 1 つの監視レコードを格納します。  
  
 [log_shipping_primary_databases](../../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md)  
 ログ配布構成で、プライマリ データベースの 1 つのレコードを格納します。  
  
 [log_shipping_primary_secondaries](../../relational-databases/system-tables/log-shipping-primary-secondaries-transact-sql.md)  
 各プライマリ データベースをそのセカンダリ データベースにマップします。  
  
 [log_shipping_secondary](../../relational-databases/system-tables/log-shipping-secondary-transact-sql.md)  
 セカンダリ ID ごとの 1 つのレコードを格納します。  
  
 [log_shipping_secondary_databases](../../relational-databases/system-tables/log-shipping-secondary-databases-transact-sql.md)  
 ログ配布構成のセカンダリ データベースごとに 1 つのレコードを格納します。  
  
  
