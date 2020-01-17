---
title: firewall_rules (Azure SQL Database) |Microsoft Docs
ms.date: 03/26/2019
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.firewall_rules
- firewall_rules
- sys.firewall_rules_TSQL
- firewall_rules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- firewall_rules
- sys.firewall_rules
ms.assetid: 140d2cd8-9aa1-4cc5-870d-e1dbc873b3fe
author: CarlRabeler
ms.author: carlrab
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 91c3a4101f19afe4a986514fea8dab207c6d9b48
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155551"
---
# <a name="sysfirewall_rules-azure-sql-database"></a>sys.firewall_rules (Azure SQL データベース)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]に関連付けられているサーバーレベルのファイアウォール設定に関する情報を返します。  
  
 `sys.firewall_rules` ビューには、次の列があります。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|id|**INT**|サーバー レベルのファイアウォール設定の識別子。|  
|name|**NVARCHAR (128)**|サーバーレベルのファイアウォール設定を説明し、区別するために選択した名前。|  
|start_ip_address|**VARCHAR (45)**|サーバーレベルのファイアウォール設定の範囲の最小の IP アドレス。 IP アドレスが次の値以上の場合は、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] サーバーに接続を試みることができます。 使用可能な最小 IP アドレスは `0.0.0.0`です。|  
|end_ip_address|**VARCHAR (45)**|サーバーレベルのファイアウォール設定の範囲の最上位の IP アドレス。 これ以下の IP アドレスは、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] サーバーへの接続を試みることができます。 可能な最大 IP アドレスは `255.255.255.255`です。<br /><br /> 注: このフィールドと**start_ip_address**フィールドの両方が `0.0.0.0`に等しい場合は、Azure の接続試行が許可されます。|  
|create_date|**/**|サーバーレベルのファイアウォール設定が作成された UTC 日時。<br /><br /> 注: UTC は、協定世界時の頭字語です。|  
|modify_date|**/**|サーバーレベルのファイアウォール設定が最後に変更された UTC 日時。|  
  
## <a name="remarks"></a>Remarks

 Microsoft Azure SQL Database に関連付けられているデータベースレベルのファイアウォール設定に関する情報を返すには、 [database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)を使用します。  
  
## <a name="permissions"></a>アクセス許可

 このビューへの読み取り専用アクセスは、 **master**データベースに接続する権限を持つすべてのユーザーが使用できます。  
  
## <a name="see-also"></a>参照

[sp_set_firewall_rule &#40;Azure SQL データベース&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)  
[sp_delete_firewall_rule &#40;Azure SQL Database&#41; ](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)   
[sp_set_database_firewall_rule &#40;Azure SQL データベース&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)  
[sp_delete_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)  
[database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
[データベースエンジンアクセスのための Windows ファイアウォールの構成](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)     
[FILESTREAM アクセスのためのファイアウォールの構成](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)  
[レポート サーバー アクセスに対するファイアウォールの構成](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md) 
