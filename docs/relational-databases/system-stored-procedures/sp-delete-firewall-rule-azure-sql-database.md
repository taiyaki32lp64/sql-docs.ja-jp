---
title: sp_delete_firewall_rule
titleSuffix: Azure SQL Database
ms.custom: seo-dt-2019
ms.date: 07/27/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_firewall_rule_TSQL
- sp_delete_firewall_rule
- sys.sp_delete_firewall_rule
- sys.sp_delete_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_firewall_rule procedure
ms.assetid: cf93eed1-ba97-4850-9fcc-b9c5a9317908
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: b012b118d16b2bf15194eb2fe515936abf6e6f80
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844385"
---
# <a name="sp_delete_firewall_rule-azure-sql-database"></a>sp_delete_firewall_rule (Azure SQL データベース)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssSDS](../../includes/sssds-md.md)] サーバーからサーバー レベルのファイアウォール設定を削除します。 このストアドプロシージャは、サーバーレベルプリンシパルログインの master データベースでのみ使用できます。  

  
## <a name="syntax"></a>構文  
  
```  
sp_delete_firewall_rule [@name =] 'name' 
[ ; ] 
```  
  
## <a name="arguments"></a>引数  
 ストアドプロシージャの引数は次のとおりです。  
  
 [@name =]'*name*'  
 削除されるサーバーレベルのファイアウォール設定の名前。 *名前*は**nvarchar (128)** で、既定値はありません。  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] では、接続の認証に必要なログイン データおよびサーバー レベルのファイアウォール規則は、各データベースで一時的にキャッシュされます。 このキャッシュは定期的に更新されます。 認証キャッシュを強制的に更新し、データベースにログイン テーブルの最新バージョンがあることを確認するには、[DBCC FLUSHAUTHCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md) を実行します。  
  
## <a name="permissions"></a>アクセス許可  
 サーバーレベルのファイアウォールルールを削除できるのは、プロビジョニングプロセスによって作成されたサーバーレベルのプリンシパルログインだけです。 Sp_delete_firewall_rule を実行するには、ユーザーが master データベースに接続されている必要があります。  
  
## <a name="example"></a>例  
 次の例では、"Example setting 1" という名前のサーバーレベルのファイアウォール設定を削除します。 仮想 master データベースでステートメントを実行します。  
  
```   
EXEC sp_delete_firewall_rule N'Example setting 1';   
```  
  
## <a name="see-also"></a>参照  
 [Azure SQL Database ファイアウォール](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [方法: ファイアウォール設定を構成する (Azure SQL Database)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40;Azure SQL Database&#41; ](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)  
  
  


