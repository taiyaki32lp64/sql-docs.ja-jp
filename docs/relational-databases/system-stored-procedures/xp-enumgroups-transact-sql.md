---
title: xp_enumgroups (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_enumgroups_TSQL
- xp_enumgroups
dev_langs:
- TSQL
helpviewer_keywords:
- xp_enumgroups
ms.assetid: 0bd3ed36-e260-469c-a5ff-b033fb9ea59d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 885e29f8abbeb185017bc2472566e41596a56900
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116768"
---
# <a name="xpenumgroups-transact-sql"></a>xp_enumgroups (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定した Windows ドメインで定義されているグローバル グループの一覧またはローカルの Microsoft Windows グループの一覧を提供します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
xp_enumgroups [ 'domain_name' ]  
```  
  
## <a name="arguments"></a>引数  
 **'** *domain_name* **'**  
 グローバル グループの一覧を列挙する Windows ドメインの名前を指定します。 *domain_name*は**sysname**、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**group**|**sysname**|Windows グループの名前|  
|**comment**|**sysname**|Windows で提供される Windows グループの説明|  
  
## <a name="remarks"></a>コメント  
 場合*domain_name* Windows ベースのコンピューターの名前を指定するのインスタンス[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で実行されている、またはドメイン名を指定すると、 **xp_enumgroups**コンピューターからローカル グループを列挙実行している[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
 **xp_enumgroups**場合のインスタンスは使用できません[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]が Windows 98 で実行されています。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **db_owner**固定データベース ロール、**マスター**メンバーシップまたは、データベース、 **sysadmin**固定サーバー ロール。  
  
## <a name="examples"></a>使用例  
 次の例のグループを一覧表示、`sales`ドメイン。  
  
```  
EXEC xp_enumgroups 'sales';  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [汎用拡張ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_loginconfig &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
