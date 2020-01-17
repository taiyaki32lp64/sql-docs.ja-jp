---
title: sp_helpremotelogin (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpremotelogin_TSQL
- sp_helpremotelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpremotelogin
ms.assetid: 93f50869-2627-4642-899f-8f626f8833f4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 11d71139786ac1442588f016bf8c576b92853cf3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997581"
---
# <a name="sphelpremotelogin-transact-sql"></a>sp_helpremotelogin (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  特定のリモート サーバー、またはローカル サーバーで定義されたすべてのリモート サーバーのリモート ログインに関する情報を報告します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]代わりに、リンク サーバーとリンク サーバー ストアド プロシージャを使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpremotelogin [ [ @remoteserver = ] 'remoteserver' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>引数  
 [ @remoteserver **=** ] **'***remoteserver***'**  
 リモート ログイン情報を返すリモート サーバーを指定します。 *remoteserver*は**sysname**、既定値は NULL です。 場合*remoteserver*が指定されていない場合、ローカル サーバーで定義されたすべてのリモート サーバーに関する情報が返されます。  
  
 [ @remotename **=** ] **'***remote_name***'**  
 リモート サーバー上の特定のリモート ログインです。 *remote_name*は**sysname**、既定値は NULL です。 場合*remote_name*が指定されていないのすべてのリモート ユーザーに関する情報が定義されている*remoteserver*が返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|server|**sysname**|ローカル サーバーで定義されたリモート サーバーの名前です。|  
|local_user_name|**sysname**|サーバーからのリモート ログインにマップするローカル サーバーにログインします。|  
|remote_user_name|**sysname**|Local_user_name にマップされるリモート サーバーにログインします。|  
|options|**sysname**|信頼された = リモート ログインがリモート サーバーからローカル サーバーに接続するときにパスワードを入力する必要はありません。<br /><br /> 信頼されていない (または空) = リモート ログインは、リモート サーバーからローカル サーバーに接続するときに、パスワードを要求します。|  
  
## <a name="remarks"></a>コメント  
 Sp_helpserver を使用して、ローカル サーバーで定義されたリモート サーバーの名前を一覧します。  
  
## <a name="permissions"></a>アクセス許可  
 権限は確認されません。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-reporting-help-on-a-single-server"></a>A. 単一のサーバー上のヘルプをレポートします。  
 次の例では、すべてのリモート ユーザーに関する情報を表示、リモート サーバーで`Accounts`します。  
  
```  
EXEC sp_helpremotelogin 'Accounts';  
```  
  
### <a name="b-reporting-help-on-all-remote-users"></a>B. すべてのリモート ユーザーに関するヘルプをレポートする  
 次の例では、ローカル サーバーに認識するすべてのリモート サーバー上ですべてのリモート ユーザーに関する情報が表示されます。  
  
```  
EXEC sp_helpremotelogin;  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_addremotelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)   
 [sp_dropremotelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_remoteoption &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
