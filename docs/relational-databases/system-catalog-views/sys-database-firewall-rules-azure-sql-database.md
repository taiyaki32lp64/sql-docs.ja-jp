---
title: database_firewall_rules (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.database_firewall_rules_TSQL
- database_firewall_rules_TSQL
- sys.database_firewall_rules
- database_firewall_rules
dev_langs:
- TSQL
helpviewer_keywords:
- database_firewall_rules
- sys.database_firewall_rules
ms.assetid: 2e821593-3b9f-43d6-a99b-1ceffe177faf
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 61402b762b7a6b4d944214d59e187e1457e93f93
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155771"
---
# <a name="sysdatabase_firewall_rules-azure-sql-database"></a>sys.database_firewall_rules (Azure SQL データベース)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]に関連付けられているデータベースレベルのファイアウォール設定に関する情報を返します。 データベースレベルのファイアウォール設定は、包含データベースユーザーを使用する場合に特に便利です。 詳細については、「[包含データベース ユーザー - データベースの移植を行う](../../relational-databases/security/contained-database-users-making-your-database-portable.md)」を参照してください。  
  
 `sys.database_firewall_rules` ビューには、次の列があります。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|id|**INTEGER**|データベースレベルのファイアウォール設定の識別子。|  
|name|**NVARCHAR (128)**|データベース レベルのファイアウォール設定を説明し、区別するために選択した名前。|  
|start_ip_address|**VARCHAR (45)**|データベースレベルのファイアウォール設定の範囲の最小の IP アドレス。 これ以上の IP アドレスは、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] インスタンスへの接続を試みることができます。 使用可能な最小 IP アドレスは `0.0.0.0`です。|  
|end_ip_address|**VARCHAR (45)**|ファイアウォール設定の範囲の最上位の IP アドレス。 IP アドレスが次の値以下である場合は、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] インスタンスに接続しようとする可能性があります。 可能な最大 IP アドレスは `255.255.255.255`です。<br /><br /> 注: このフィールドと**start_ip_address**フィールドの両方が `0.0.0.0`に等しい場合は、Azure の接続試行が許可されます。|  
|create_date|**/**|データベース レベルのファイアウォール設定が作成された UTC 日時。|  
|modify_date|**/**|データベース レベルのファイアウォール設定が最後に変更された UTC 日時。|  
  
## <a name="remarks"></a>Remarks  
 Microsoft Azure SQL Database に関連付けられているサーバーレベルのファイアウォール設定に関する情報を返すには、 [firewall_rules (Azure SQL Database)](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 このビューは、 **master**データベースと各ユーザーデータベースで使用できます。 このビューへの読み取り専用アクセスは、データベースに接続する権限を持つすべてのユーザーが使用できます。  
  
## <a name="see-also"></a>参照
[sp_set_database_firewall_rule &#40;Azure SQL データベース&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)  
[sp_delete_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)  
[sp_set_firewall_rule &#40;Azure SQL データベース&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)  
[sp_delete_firewall_rule &#40;Azure SQL Database&#41; ](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)   
[firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)  
[データベースエンジンアクセスのための Windows ファイアウォールの構成](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)     
[FILESTREAM アクセスのためのファイアウォールの構成](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)  
[レポート サーバー アクセスに対するファイアウォールの構成](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
