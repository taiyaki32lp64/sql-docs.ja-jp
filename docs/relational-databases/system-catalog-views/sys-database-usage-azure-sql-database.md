---
title: database_usage (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- database_usage
- database_usage_TSQL
- sys.database_usage_TSQL
- sys.database_usage
dev_langs:
- TSQL
helpviewer_keywords:
- database_usage
- sys.database_usage
ms.assetid: be6820de-60bf-4ddd-ace7-4077893d630f
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 0a0789ebd9a5aa4bd10605d69afa59a586ce75b2
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155540"
---
# <a name="sysdatabase_usage-azure-sql-database"></a>sys.database_usage (Azure SQL データベース)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **注: これは Azure SQL Database V11 にのみ適用されます。**  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] サーバー上のデータベースの数、種類、および期間を一覧表示します。  
  
 **Database_usage**ビューには、次の列が含まれています。  
  
|列名|[説明]|  
|-----------------|-----------------|  
|time|使用状況イベントが発生した日付。|  
|sku|データベースのサービス階層の種類: **Web**、 **Business**、 **Basic**、 **Standard**、 **Premium**|  
|quantity|その日に存在していた SKU の種類のデータベースの最大数。|  
  
## <a name="permissions"></a>アクセス許可  
 このビューへの読み取り専用アクセスは、 **master**データベースに接続する権限を持つすべてのユーザーが使用できます。  
  
## <a name="remarks"></a>Remarks  
 **Database_usage**ビューでは、サブスクリプションの日ごとに1つの行が返されます。  
  
## <a name="see-also"></a>参照  
 [SQL Database 料金の詳細](https://go.microsoft.com/fwlink/?LinkID=394978)   
 [Azure SQL Database のアカウントと課金](https://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  
