---
title: RECONFIGURE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/20/2016
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RECONFIGURE
- RECONFIGURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- reconfiguring configuration options
- configuration options [SQL Server], reconfiguring
- updating configuration options
- RECONFIGURE, RECONFIGURE statement
- RECONFIGURE
- RECONFIGURE, WITH OVERRIDE statement
ms.assetid: 2e6e4eeb-b70b-4f45-a253-28ac4e595d75
author: rothja
ms.author: jroth
ms.openlocfilehash: 6ee52f585af8930afcba301a5aba12df4eb47173
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072379"
---
# <a name="reconfigure-transact-sql"></a>RECONFIGURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **sp_configure** システム ストアド プロシージャで変更された構成オプションの現在の構成値 (**sp_configure** 結果セット内の **config_value** 列) に基づいて更新を行います。 構成オプションによっては、サーバーをいったん停止し、再起動しないと、現在実行中の値を更新できません。このため RECONFIGURE では、変更された構成値に対応する現在実行中の値 (**sp_configure** 結果セット内の **run_value** 列) は常に更新されるわけではありません。    
    
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>構文    
    
```    
    
RECONFIGURE [ WITH OVERRIDE ]    
```    
    
## <a name="arguments"></a>引数    
 RECONFIGURE    
 構成の設定でサーバーの停止と再起動を必要としない場合、現在実行中の値を更新することを指定します。 また RECONFIGURE では、新しい構成値が、無効な値 (**syscharsets** に存在しない並べ替え順など) や非推奨値になっていないかがチェックされます。 構成オプションでサーバーの停止と再起動を必要としない場合、RECONFIGURE を指定すると、構成オプションに関する現在実行中の値と現在の構成値は同じになります。    
    
 WITH OVERRIDE    
 **recovery interval** 詳細構成オプションに関する、構成値のチェック (無効な値や非推奨値のチェック) を無効にします。    
    
 WITH OVERRIDE オプションを使用してほとんどすべての構成オプションを再構成できますが、それでも一部の致命的なエラーは防止されています。 たとえば、**min server memory** 構成オプションを、**max server memory** 構成オプションで指定されている値よりも大きい値を使用して構成することはできません。
      
## <a name="remarks"></a>Remarks    
 **sp_configure** では、各構成オプションに定義されている有効値の範囲外の値を新しい構成オプションの値として使用することはできません。    
    
 RECONFIGURE は、明示的または暗黙的なトランザクションでは使用できません。 複数のオプションを同時に再構成すると、いずれかの再構成オプションが失敗した場合に、すべての再構成オプションが無効になります。    
    
 リソース ガバナンスを最高する場合は、[ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md) の RECONFIGURE オプションを参照してください。    
    
## <a name="permissions"></a>アクセス許可    
 RECONFIGURE 権限は、既定では ALTER SETTINGS 権限が与えられているユーザーに与えられます。 **sysadmin** および **serveradmin** 固定サーバー ロールでは、この権限が暗黙的に保持されます。    
    
## <a name="examples"></a>使用例    
 次の例では、`recovery interval` 構成オプションの上限を `75` 分に設定し、`RECONFIGURE WITH OVERRIDE` を使用してインストールします。 60 分より長い復旧間隔は推奨されず、既定では許可されせんが、 `WITH OVERRIDE` オプションが指定されているので、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では指定の値 (`75`) が `recovery interval` 構成オプションに対して有効かどうかはチェックされません。    
    
```    
EXEC sp_configure 'recovery interval', 75    
RECONFIGURE WITH OVERRIDE;    
GO    
```    
    
## <a name="see-also"></a>参照    
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)     
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)    
    
  
