---
title: sys.configurations (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.configurations_TSQL
- configurations
- sys.configurations
- configurations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.configurations catalog view
ms.assetid: c4709ed1-bf88-4458-9e98-8e9b78150441
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9eb9ced4e010001f42e106ce8b1903e029f2f1c4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109564"
---
# <a name="sysconfigurations-transact-sql"></a>sys.configurations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  システムでは、サーバー全体の構成オプションの値ごとに行が含まれています。  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|構成値の一意 ID|  
|**name**|**nvarchar(35)**|構成オプションの名前。|  
|**value**|**sql_variant**|オプションの構成値|  
|**minimum**|**sql_variant**|構成オプションの最小値|  
|**maximum**|**sql_variant**|構成オプションの最大値|  
|**value_in_use**|**sql_variant**|オプションで現在有効な実行値|  
|**description**|**nvarchar (255)**|構成オプションの説明|  
|**is_dynamic**|**bit**|1 = RECONFIGURE ステートメントの実行時に影響を与える変数|  
|**is_advanced**|**bit**|1 = 変数が表示される場合にのみ、 **advancedoption を表示する**設定されます。|  
  
 すべてのサーバー構成オプションの一覧は、次を参照してください。[サーバー構成オプションの&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)します。  
  
> [!NOTE]  
>  データベース レベルの構成のオプションを参照してください[データベース スコープの構成の変更&#40;Transact SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。 ソフト NUMA を構成するのにを参照してください[ソフト NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [サーバー全体の構成に関するカタログ ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
