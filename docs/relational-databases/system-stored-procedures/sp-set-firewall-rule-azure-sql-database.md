---
title: sp_set_firewall_rule (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 07/28/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_set_firewall_rule
- sp_set_firewall_rule_TSQL
- sys.sp_set_firewall_rule
- sys.sp_set_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_firewall_rule
- firewall_rules, setting server rules
ms.assetid: a974a561-5382-4039-8499-3a56767bcefe
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 9bc37626879b743eb3a5d0864490dc3543a8d8a9
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70152063"
---
# <a name="sp_set_firewall_rule-azure-sql-database"></a>sp_set_firewall_rule (Azure SQL データベース)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssSDS](../../includes/sssds-md.md)] サーバーのサーバーレベルのファイアウォール設定を作成または更新します。 このストアドプロシージャを使用できるのは、master データベースで、サーバーレベルプリンシパルログインまたは Azure Active Directory プリンシパルが割り当てられている場合のみです。  
  
  
## <a name="syntax"></a>構文  
  
```
sp_set_firewall_rule [@name =] 'name', 
    [@start_ip_address =] 'start_ip_address', 
    [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 次の表は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]でサポートされている引数とオプションを示しています。  
  
|[オブジェクト名]|Datatype|[説明]|  
|----------|--------------|-----------------|  
|[@name =]指定|**NVARCHAR (128)**|サーバーレベルのファイアウォール設定を説明し、区別するために使用される名前。|  
|[@start_ip_address =]' start_ip_address '|**VARCHAR (50)**|サーバーレベルのファイアウォール設定の範囲の最小の IP アドレス。 IP アドレスが次の値以上の場合は、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] サーバーに接続を試みることができます。 使用可能な最小 IP アドレスは `0.0.0.0`です。|  
|[@end_ip_address =]' end_ip_address '|**VARCHAR (50)**|サーバーレベルのファイアウォール設定の範囲の最上位の IP アドレス。 これ以下の IP アドレスは、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] サーバーへの接続を試みることができます。 可能な最大 IP アドレスは `255.255.255.255`です。<br /><br /> 注: このフィールドと*start_ip_address*フィールドの両方が `0.0.0.0`に等しい場合は、Azure の接続試行が許可されます。|  
  
## <a name="remarks"></a>Remarks  
 サーバー レベルのファイアウォール設定の名前は一意である必要があります。 ストアドプロシージャに対して指定された設定の名前がファイアウォール設定テーブルに既に存在する場合は、開始 IP アドレスと終了 IP アドレスが更新されます。 そうでない場合は、新しいサーバー レベルのファイアウォール設定が作成されます。  
  
 開始 IP アドレスと終了 IP アドレスが `0.0.0.0`に等しいサーバーレベルのファイアウォール設定を追加すると、Azure から [!INCLUDE[ssSDS](../../includes/sssds-md.md)] サーバーにアクセスできるようになります。 *Name*パラメーターに値を指定します。これは、サーバーレベルのファイアウォール設定の内容を思い出すのに役立ちます。  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] では、接続の認証に必要なログイン データおよびサーバー レベルのファイアウォール規則は、各データベースで一時的にキャッシュされます。 このキャッシュは定期的に更新されます。 認証キャッシュを強制的に更新し、データベースにログイン テーブルの最新バージョンがあることを確認するには、[DBCC FLUSHAUTHCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md) を実行します。  
  
## <a name="permissions"></a>アクセス許可  
 サーバーレベルのファイアウォールルールを作成または変更できるのは、プロビジョニング処理によって作成されたサーバーレベルのプリンシパルログイン、または管理者として割り当てられた Azure Active Directory プリンシパルだけです。 Sp_set_firewall_rule を実行するには、ユーザーが master データベースに接続されている必要があります。  
  
## <a name="examples"></a>使用例  
 次のコードでは、Azure からのアクセスを可能にする `Allow Azure` という名前のサーバーレベルのファイアウォール設定を作成します。 仮想 master データベースで次のを実行します。  
  
```  
-- Enable Azure connections.  
exec sp_set_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 次のコードでは、IP アドレス `0.0.0.2`に対してのみ `Example setting 1` という名前のサーバーレベルのファイアウォール設定を作成します。 次に、`sp_set_firewall_rule` のストアドプロシージャを再度呼び出して、そのファイアウォール設定で `0.0.0.4`に終了 IP アドレスを更新します。 これにより、IP アドレス `0.0.0.2`、`0.0.0.3`、および `0.0.0.4` サーバーへのアクセスを許可する範囲が作成されます。  
  
```  
-- Create server-level firewall setting for only IP 0.0.0.2  
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.2';  
  
-- Update server-level firewall setting to create a range of allowed IP addresses
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.4';  
  
```  
  
## <a name="see-also"></a>参照  
 [Azure SQL Database ファイアウォール](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [方法: ファイアウォール設定を構成する (Azure SQL Database)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)
