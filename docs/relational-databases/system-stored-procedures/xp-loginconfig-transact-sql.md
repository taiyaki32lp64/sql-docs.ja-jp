---
title: xp_loginconfig (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_loginconfig_TSQL
- xp_loginconfig
dev_langs:
- TSQL
helpviewer_keywords:
- xp_loginconfig
ms.assetid: d380e799-2857-408a-bcbf-5e73a8e6aa5a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 7abf136187b4f45a03cebc92fd23ee544dddb117
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116686"
---
# <a name="xploginconfig-transact-sql"></a>xp_loginconfig (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  インスタンスのログイン セキュリティ構成を報告[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
xp_loginconfig ['config_name']  
```  
  
## <a name="arguments"></a>引数  
 **'** *config_name 付きで* **'**  
 表示する構成値を指定します。 場合*config_name 付きで*が指定されていないすべての構成値が報告されます。 *config_name 付きで*は**sysname**、既定値は null の場合、これらの値のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**ログイン モード**|ログイン セキュリティ モードです。 指定できる値は**Mixed**と**Windows 認証**します。<br /><br /> 置換されます。<br /><br /> `SELECT SERVERPROPERTY('IsIntegratedSecurityOnly'); GO`|  
|**既定のログイン**|信頼関係接続が許可されているユーザー (ログイン名が照合されないユーザー) に対する、既定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン ID の名前。 既定のログインは**ゲスト**します。 この値は、旧バージョンとの互換性のために提供されます。|  
|**既定のドメイン**|信頼関係接続のネットワーク ユーザーの既定の Windows ドメインの名前。 既定のドメインは、Windows および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているコンピューターのドメインです。 この値は、旧バージョンとの互換性のために提供されます。|  
|**監査レベル**|監査レベル。 指定できる値は**none**、**成功**、**エラー**、および**すべて**します。 監査はエラー ログや Windows イベント ビューアーに書き込まれます。|  
|**セットのホスト名**|クライアントのログイン レコードのホスト名が、Windows ネットワーク ユーザー名と置き換えられるかどうかを示します。 指定できる値は**true**または**false**します。 これを設定するからの出力で、ネットワーク ユーザー名が表示されます**sp_who**します。|  
|**マップ _**|Windows の特殊文字が有効なにマップされる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]アンダー スコア文字 (_)。 指定できる値は**ドメインの区切り記号**(既定)、**領域**、 **null**、または任意の 1 文字。 この値は、旧バージョンとの互換性のために提供されます。|  
|**マップ $**|Windows の特殊文字が有効なにマップされる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ドル記号 ($) の文字します。 指定できる値は**ドメインの区切り記号**、**領域**、 **null**、または任意の 1 文字。 既定値は**領域**します。 この値は、旧バージョンとの互換性のために提供されます。|  
|**# をマップします。**|Windows の特殊文字が有効なにマップされる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]番号記号 (#)。 指定できる値は**ドメインの区切り記号**、**領域**、 **null**、または任意の 1 文字。 既定値はハイフンです。 この値は、旧バージョンとの互換性のために提供されます。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|構成値。|  
|**構成値**|**sysname**|構成値の設定|  
  
## <a name="remarks"></a>コメント  
 **xp_loginconfig**構成値を設定するのには使用できません。  
  
 ログイン モードと監査レベルを設定するには使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]します。  
  
## <a name="permissions"></a>アクセス許可  
 に対する CONTROL 権限が必要です、**マスター**データベース。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-how-to-report-all-configuration-values"></a>A. すべての構成値を報告する方法  
 次の例では、現在構成されている設定をすべて表示します。  
  
```  
EXEC xp_loginconfig;  
GO  
```  
  
### <a name="b-how-to-report-a-specific-configuration-value"></a>B. 特定の構成値をレポートする方法  
 次の例では、ログイン モードのみの設定を示します。  
  
```  
EXEC xp_loginconfig 'login mode';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_denylogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [xp_logininfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
