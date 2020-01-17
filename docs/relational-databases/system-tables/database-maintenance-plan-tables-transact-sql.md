---
title: データベース メンテナンス プラン テーブル (TRANSACT-SQL) |Microsoft Docs
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
- database maintenance plans [SQL Server]
- maintenance plans [SQL Server], system tables
- system tables [SQL Server], database maintenance plans
ms.assetid: f264554c-5514-4df2-aadb-6dcdc2dfcfea
author: stevestein
ms.author: sstein
ms.openlocfilehash: f6fe1c0734864f8bde8b579ced77dc8106cb80ab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084754"
---
# <a name="database-maintenance-plan-tables-transact-sql"></a>データベース メンテナンス プラン テーブル (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  このセクションのトピックでは、データベース メンテナンス プランで使用される情報を格納するシステム テーブルについて説明します。 これらのテーブルの情報を保持するインスタンスの以前のバージョンからアップグレードした[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  
## <a name="in-this-section"></a>このセクションの内容  
 [sysdbmaintplan_databases](../../relational-databases/system-tables/sysdbmaintplan-databases-transact-sql.md)  
 関連付けられているアップグレードされたデータベースのメンテナンス プランのあるデータベースごとに 1 つの行が含まれています。  
  
 [sysdbmaintplan_history](../../relational-databases/system-tables/sysdbmaintplan-history-transact-sql.md)  
 アップグレードされたデータベース メンテナンス プランで実行したアクションごとに 1 行のデータを格納します。  
  
 [sysdbmaintplan_jobs](../../relational-databases/system-tables/sysdbmaintplan-jobs-transact-sql.md)  
 アップグレードされたデータベース メンテナンス プランのジョブごとに 1 つの行が含まれています。  
  
 [sysdbmaintplans](../../relational-databases/system-tables/sysdbmaintplans-transact-sql.md)  
 各アップグレードされたデータベース メンテナンス プランの 1 つの行が含まれています。  
  
## <a name="see-also"></a>関連項目  
 [のオブジェクト エクスプローラーの](../../relational-databases/maintenance-plans/maintenance-plans.md)  
  
  
