---
title: sp_helplinkedsrvlogin (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helplinkedsrvlogin_TSQL
- sp_helplinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplinkedsrvlogin
ms.assetid: a2b1eba0-bf71-47e7-a4c7-9f55feec82a3
author: stevestein
ms.author: sstein
ms.openlocfilehash: f1728b3e5d4cd3189a8d9a01a8b72ecedaf7cb6d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122464"
---
# <a name="sphelplinkedsrvlogin-transact-sql"></a>sp_helplinkedsrvlogin (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  分散クエリやリモート ストアド プロシージャを使用する特定のリンク サーバーに対して定義されているログインのマッピングに関する情報を提供します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helplinkedsrvlogin [ [ @rmtsrvname = ] 'rmtsrvname' ]   
     [ , [ @locallogin = ] 'locallogin' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @rmtsrvname = ] 'rmtsrvname'` ログイン マッピングを適用するリンク サーバーの名前です。 *rmtsrvname*は**sysname**、既定値は NULL です。 NULL の場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行中のローカル コンピューターで定義されているすべてのリンク サーバーに対して定義された、すべてのログインのマッピングが返されます。  
  
`[ @locallogin = ] 'locallogin'` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、リンク サーバーにマップされているローカル サーバー上のログイン*rmtsrvname*します。 *locallogin*は**sysname**、既定値は NULL です。 NULL を指定ですべてのログイン マッピングが定義されている*rmtsrvname*が返されます。 ない場合 null の場合、マッピング*locallogin*に*rmtsrvname*既に存在する必要があります。 *locallogin*できます、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインまたは Windows ユーザーです。 Windows ユーザー必要がありますがへのアクセス権[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]直接またはアクセスが許可されている Windows グループのメンバーシップを使用します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**リンク サーバー**|**sysname**|リンク サーバー名。|  
|**ローカル ログイン**|**sysname**|ローカル ログインのマッピングが適用されます。|  
|**自己マッピング**|**smallint**|0 =**ローカル ログイン**にマップされて**リモート ログイン**に接続するときに**リンク サーバー**します。<br /><br /> 1 =**ローカル ログイン**に接続するときに、同じログインとパスワードにマップ**リンク サーバー**します。|  
|**リモート ログイン**|**sysname**|上のログイン名**LinkedServer**にマップされる**LocalLogin**とき**IsSelfMapping**は 0 です。 場合**IsSelfMapping**は 1 です。 **RemoteLogin**は NULL です。|  
  
## <a name="remarks"></a>コメント  
 ログインのマッピングを削除する前に使用して、 **sp_helplinkedsrvlogin**関連するリンク サーバーを決定します。  
  
## <a name="permissions"></a>アクセス許可  
 権限は確認されません。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-displaying-all-login-mappings-for-all-linked-servers"></a>A. すべてのリンク サーバーのすべてのログイン マッピングを表示します。  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行中のローカル コンピューターで定義されているすべてのリンク サーバーの、すべてのログインのマッピングを表示します。  
  
```  
EXEC sp_helplinkedsrvlogin;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Linked Server    Local Login   Is Self Mapping Remote Login   
---------------- ------------- --------------- --------------   
Accounts         NULL          1               NULL  
Sales            NULL          1               NULL  
Sales            Mary          0               sa  
Marketing        NULL          1               NULL  
  
(4 row(s) affected)  
```  
  
### <a name="b-displaying-all-login-mappings-for-a-linked-server"></a>B. リンク サーバーのすべてのログイン マッピングを表示します。  
 次の例は、すべてローカルで定義されたログインのマッピングを表示、`Sales`リンク サーバー。  
  
```  
EXEC sp_helplinkedsrvlogin 'Sales';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Linked Server    Local Login   Is Self Mapping Remote Login   
---------------- ------------- --------------- --------------   
Sales            NULL          1               NULL  
Sales            Mary          0               sa  
  
(2 row(s) affected)  
```  
  
### <a name="c-displaying-all-login-mappings-for-a-local-login"></a>C. ローカル ログインに対するすべてのログイン マッピングを表示します。  
 次の例は、ログインに対するすべてのローカルに定義されたログイン マッピングを表示`Mary`します。  
  
```  
EXEC sp_helplinkedsrvlogin NULL, 'Mary';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Linked Server    Local Login   Is Self Mapping Remote Login   
---------------- ------------- --------------- --------------   
Sales            NULL          1               NULL  
Sales            Mary          0               sa  
  
(2 row(s) affected)  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
