---
title: sp_set_database_firewall_rule
titleSuffix: Azure SQL Database
ms.date: 08/04/2017
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_set_database_firewall_rule
- sp_set_database_firewall_rule_TSQL
- sys.sp_set_database_firewall_rule
- sys.sp_set_database_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_database_firewall_rule
- firewall_rules, setting database rules
ms.assetid: 8f0506b6-a4ac-4e4d-91db-8077c40cb17a
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: dfe41ee68412414df24bc7f0bd583bbb0109b3db
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74055088"
---
# <a name="sp_set_database_firewall_rule-azure-sql-database"></a>sp_set_database_firewall_rule (Azure SQL データベース)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]のデータベースレベルのファイアウォール規則を作成または更新します。 データベースファイアウォール規則は、 **master**データベースと、[!INCLUDE[ssSDS](../../includes/sssds-md.md)]のユーザーデータベースに対して構成できます。 データベースファイアウォールルールは、包含データベースユーザーを使用する場合に特に便利です。 詳細については、「[包含データベース ユーザー - データベースの移植を行う](../../relational-databases/security/contained-database-users-making-your-database-portable.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_set_database_firewall_rule [@name = ] [N]'name'  
, [@start_ip_address =] 'start_ip_address'  
, [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
データベースレベルのファイアウォール設定を記述および区別するために使用される名前 `[ @name = ] [N]'name'` ます。 *名前*は**nvarchar (128)** で、既定値はありません。 Unicode 識別子 `N` は [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]では省略可能です。 
  
データベースレベルのファイアウォール設定の範囲で最も低い IP アドレスを `[ @start_ip_address = ] 'start_ip_address'` します。 これ以上の IP アドレスは、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] インスタンスへの接続を試みることができます。 使用可能な最小 IP アドレスは `0.0.0.0`です。 *start_ip_address*は**varchar (50)** で、既定値はありません。  
  
データベースレベルのファイアウォール設定の範囲の最大 IP アドレスを `[ @end_ip_address = ] 'end_ip_address'` します。 IP アドレスが次の値以下である場合は、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] インスタンスに接続しようとする可能性があります。 可能な最大 IP アドレスは `255.255.255.255`です。 *end_ip_address*は**varchar (50)** で、既定値はありません。  
  
 次の表は、[!INCLUDE[ssSDS](../../includes/sssds-md.md)]でサポートされている引数とオプションを示しています。  
  
> [!NOTE]  
>  Azure の接続試行は、このフィールドと*start_ip_address*フィールドの両方が `0.0.0.0`と等しい場合に許可されます。  
  
## <a name="remarks"></a>Remarks  
 データベースレベルのファイアウォール設定の名前は、一意である必要があります。 ストアド プロシージャに提供されるデータベース レベルのファイアウォール設定の名前がデータベース レベルのファイアウォール設定のテーブルに既に存在する場合は、開始 IP アドレスと終了 IP アドレスが更新されます。 それ以外の場合は、新しいデータベースレベルのファイアウォール設定が作成されます。  
  
 開始 IP アドレスと終了 IP アドレスが `0.0.0.0`に等しいデータベースレベルのファイアウォール設定を追加すると、任意の Azure リソースから [!INCLUDE[ssSDS](../../includes/sssds-md.md)] サーバー内のデータベースにアクセスできるようになります。 *名前*パラメーターに値を指定すると、ファイアウォール設定の内容を覚えやすくなります。  
  
## <a name="permissions"></a>アクセス許可  
 データベースに対する **CONTROL** 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次のコードでは、Azure からデータベースにアクセスできるようにする `Allow Azure` というデータベースレベルのファイアウォール設定を作成します。  
  
```  
-- Enable Azure connections.  
EXECUTE sp_set_database_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 次のコードでは、IP アドレス `0.0.0.4`に対してのみ `Example DB Setting 1` というデータベースレベルのファイアウォール設定を作成します。 次に、`sp_set_database firewall_rule` のストアドプロシージャを再度呼び出して、そのファイアウォール設定で `0.0.0.6`に終了 IP アドレスを更新します。 これにより、`0.0.0.4`、`0.0.0.5`、および `0.0.0.6` の IP アドレスがデータベースにアクセスできるようになる範囲が作成されます。
  
```  
-- Create database-level firewall setting for only IP 0.0.0.4  
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.4';  
  
-- Update database-level firewall setting to create a range of allowed IP addresses
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.6';  
  
```  
  
## <a name="see-also"></a>参照  
 [Azure SQL Database ファイアウォール](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [方法: ファイアウォール設定を構成する (Azure SQL Database)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40;Azure SQL Database&#41; ](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sp_delete_database_firewall_rule &#40;Azure SQL Database&#41; ](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)   
 [database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
  
