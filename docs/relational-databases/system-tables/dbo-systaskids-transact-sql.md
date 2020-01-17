---
title: dbo.systaskids (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- systaskids_TSQL
- dbo.systaskids
- systaskids
- dbo.systaskids_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- systaskids system table
ms.assetid: 45c56d89-4160-4d84-80bf-a7a05488792d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9ed9ac8e81abaf6367d3a9c5518f1f18cb94ef8b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990400"
---
# <a name="dbosystaskids-transact-sql"></a>dbo.systaskids (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で作成されたタスクと、現在のバージョンの [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ジョブとのマッピングを格納します。 このテーブルに格納されます、 **msdb**データベース。  
  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**task_id**|**int**|タスクの ID|  
|**job_id**|**uniqueidentifier**|タスクがマップされているジョブの ID|  
  
  
