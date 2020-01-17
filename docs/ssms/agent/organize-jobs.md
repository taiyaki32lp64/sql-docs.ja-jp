---
title: ジョブの整理 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job category
- organize jobs
ms.assetid: 629c3e06-f933-483b-8621-280dbb7a7bd1
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b2167ec7aaf1656312e81abc842c3910a5522947
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68260028"
---
# <a name="organize-jobs"></a>ジョブの整理
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

ジョブ カテゴリを使用してジョブを管理すると、フィルター操作やグループ化を簡単に行うことができます。 たとえば、データベース バックアップに関するすべてのジョブを [データベースのメンテナンス] カテゴリとしてまとめます。 ジョブ カテゴリは、独自に作成することもできます。  
  
> [!WARNING]  
> マルチサーバー カテゴリは、マスター サーバー上だけに存在します。 マスター サーバー上で使用できるのは、 **[未カテゴリ化 (マルチサーバー)]** という既定のジョブ カテゴリだけです。 マルチサーバー ジョブがダウンロードされると、ターゲット サーバー上ではそのカテゴリが **[MSX からのジョブ]** に変更されます。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**[説明]**|**トピック**|  
|ジョブ カテゴリを作成する方法について説明します。|[ジョブ カテゴリの作成](../../ssms/agent/create-a-job-category.md)|  
|ジョブ カテゴリを削除する方法について説明します。|[ジョブ カテゴリの削除](../../ssms/agent/delete-a-job-category.md)|  
|ジョブをジョブ カテゴリに割り当てる方法について説明します。|[ジョブ カテゴリへのジョブの割り当て](../../ssms/agent/assign-a-job-to-a-job-category.md)|  
|ジョブ カテゴリのメンバーシップを変更する方法について説明します。|[Change the Membership of a Job Category](../../ssms/agent/change-the-membership-of-a-job-category.md)|  
|カテゴリ情報の一覧を表示する方法について説明します。|[ジョブ カテゴリ情報の一覧の表示](../../ssms/agent/list-job-category-information.md)|  
  
