---
title: Common Criteria Compliance Enabled 構成 | Microsoft Docs
ms.custom: ''
ms.date: 08/21/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- common criteria compliance
helpviewer_keywords:
- CC (common criteria) [Database Engine]
- common criteria compliance [Database Engine]
- Risidual Information Protection [Database Engine]
- RIP (Residual Information Protection)
ms.assetid: 61766eea-c450-408d-af33-fbe7ef8c9ff2
author: craigg-msft
ms.author: craigg
ms.openlocfilehash: f072ed3e73b7dacd10254c04aaa34e5466b582b8
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262218"
---
# <a name="common-criteria-compliance-enabled-server-configuration"></a>Common Criteria Compliance Enabled サーバー構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[情報セキュリティ国際評価基準 (Common Criteria) への準拠] オプションを使用すると、[情報技術セキュリティ評価のためのコモンクライテリア](https://www.commoncriteriaportal.org/)で必要とされる次の要素を有効にできます。  
  
|[抽出条件]|[説明]|  
|--------------|-----------------|  
|残存情報保護 (RIP)|RIP の要件とは、新しいリソースにメモリを再度割り当てる前に、メモリ割り当てを既知のビット パターンで上書きすることです。 RIP 標準を満たすとセキュリティの向上が図れますが、メモリ割り当てを上書きすることによってパフォーマンスが低下する場合があります。 [情報セキュリティ国際評価基準 (Common Criteria) への準拠を有効にする] を有効にすると、この上書きが行われます。|  
|ログインの統計を表示する機能|[情報セキュリティ国際評価基準 (Common Criteria) への準拠を有効にする] を有効にすると、ログイン監査が有効になります。 ユーザーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]へのログインに成功するたびに、最後にログインに成功した時間、最後にログインに失敗した時間、最後にログインした時間から現在のログイン時間までのログイン試行回数について、情報を確認できます。 このログインに関する統計情報は、 [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) 動的管理ビューにクエリを実行すると表示できます。|  
|列の `GRANT` がテーブルの `DENY` をオーバーライドしないこと|[common criteria compliance enabled] オプションを有効にすると、テーブル レベルの `DENY` が列レベルの `GRANT` より優先されます。 このオプションが有効でない場合は、列レベルの `GRANT` がテーブル レベルの `DENY` より優先されます。|  
  
 [Common Criteria Compliance Enabled] オプションは拡張オプションです。 情報セキュリティ国際評価基準は、Enterprise Edition と Datacenter Edition についてのみ評価され、認定されています。 情報セキュリティ国際評価基準の最新の状況については、 [Microsoft SQL Server の情報セキュリティ国際評価基準](https://go.microsoft.com/fwlink/?LinkId=616319) の Web サイトを参照してください。  
  
> [!IMPORTANT]  
>  情報セキュリティ国際評価基準の評価保証レベル 4+ (EAL4+) に準拠するには、[情報セキュリティ国際評価基準 (Common Criteria) への準拠を有効にする] オプションを有効にすることのほかに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の構成を完了するためのスクリプトをダウンロードして実行する必要があります。 このスクリプトは、 [Microsoft SQL Server 情報セキュリティ国際評価基準](https://go.microsoft.com/fwlink/?LinkId=616319) Web サイトからダウンロードできます。  
  
 `sp_configure` システム ストアド プロシージャを使用してこの設定を変更する場合、[common criteria compliance enabled] を変更できるのは、show advanced options が 1 に設定されているときだけです。 この設定は、サーバーを再起動した後に有効になります。 有効値は、0 および 1 です。  
  
-   0 は [情報セキュリティ国際評価基準 (Common Criteria) への準拠を有効にする] が有効でないことを表します。 これは既定値です。  
  
-   1 は [情報セキュリティ国際評価基準 (Common Criteria) への準拠を有効にする] が有効であることを表します。  
  
## <a name="examples"></a>使用例  
 次の例では、情報セキュリティ国際評価基準への準拠を有効にしています。  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'common criteria compliance enabled', 1;  
GO  
RECONFIGURE WITH OVERRIDE; 
GO  
```  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]を再起動します。
  
## <a name="see-also"></a>参照  
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
