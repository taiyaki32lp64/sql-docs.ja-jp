---
title: レプリケーション ビュー (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- distribution databases [SQL Server replication], system views
- metadata [SQL Server], views
- views [SQL Server], replication
- replication views [SQL Server]
- publications [SQL Server replication], system views
- articles [SQL Server replication], system views
- replication metadata [SQL Server]
- subscriptions [SQL Server replication], system views
- system views [SQL Server], replication
ms.assetid: 93e5056d-0d93-4a48-ba33-72762eb995d8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 51cc9434805fbd14204d74edae1594ae01c06bb2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129565"
---
# <a name="replication-views-transact-sql"></a>レプリケーション ビュー (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  これらのビューでのレプリケーションで使用される情報を含む[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 ビュー内のデータに簡単にアクセスを有効にする[レプリケーション システム テーブル](../../relational-databases/system-tables/replication-tables-transact-sql.md)します。 ビューは、そのデータベースはパブリケーションまたはサブスクリプション データベースとして有効にすると、ユーザー データベースで作成されます。 すべてのレプリケーション オブジェクトは、レプリケーション トポロジから、データベースが削除されると、ユーザー データベースから削除されます。 使用してレプリケーション メタデータにアクセスするための推奨される方法は、[レプリケーションのストアド プロシージャ](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)します。  
  
> [!IMPORTANT]  
>  すべてのユーザーによって直接システム ビューを変更しないようにします。  
  
## <a name="replication-views"></a>レプリケーション ビュー  
 次にデータベースでグループ化されたレプリケーションで使用されるシステム ビューの一覧を示します。  
  
### <a name="replication-views-in-the-msdb-database"></a>msdb データベースのレプリケーション ビュー  
  
|||  
|-|-|  
|[MSdatatype_mappings &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/msdatatype-mappings-transact-sql.md)|[sysdatatypemappings &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/sysdatatypemappings-transact-sql.md)|  
  
### <a name="replication-views-in-the-distribution-database"></a>ディストリビューション データベースのレプリケーション ビュー  
  
|||  
|-|-|  
|[IHextendedArticleView &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/ihextendedarticleview-transact-sql.md)|[sysarticles&#40;システム ビュー&#41; &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)|  
|[IHextendedSubscriptionView &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/ihextendedsubscriptionview-transact-sql.md)|[sysextendedarticlesview &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/sysextendedarticlesview-transact-sql.md)|  
|[IHsyscolumns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/ihsyscolumns-transact-sql.md)|[syspublications &#40;システム ビュー&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/syspublications-system-view-transact-sql.md)|  
|[MSdistribution_status &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/msdistribution-status-transact-sql.md)|[syssubscriptions &#40;システム ビュー&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/syssubscriptions-system-view-transact-sql.md)|  
|[sysarticlecolumns&#40;システム ビュー&#41; &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)||  
  
### <a name="replication-views-in-the-publication-database"></a>パブリケーション データベースのレプリケーション ビュー  
  
|||  
|-|-|  
|[sysmergeextendedarticlesview &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/sysmergeextendedarticlesview-transact-sql.md)|[sysmergepartitioninfoview &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/sysmergepartitioninfoview-transact-sql.md)|  
|[systranschemas &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/systranschemas-transact-sql.md)||  
  
### <a name="replication-views-in-the-subscription-database"></a>サブスクリプション データベースのレプリケーション ビュー  
  
|||  
|-|-|  
|[sysmergeextendedarticlesview &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/sysmergeextendedarticlesview-transact-sql.md)|[sysmergepartitioninfoview &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/sysmergepartitioninfoview-transact-sql.md)|  
|[systranschemas &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/systranschemas-transact-sql.md)||  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
