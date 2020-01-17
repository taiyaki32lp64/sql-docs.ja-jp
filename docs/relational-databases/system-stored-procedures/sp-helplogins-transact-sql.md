---
title: sp_helplogins (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helplogins_TSQL
- sp_helplogins
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplogins
ms.assetid: f9ad3767-5b9f-420d-8922-b637811404f7
author: stevestein
ms.author: sstein
ms.openlocfilehash: b4c3d6ded5d85e5d38556792aaa7ea71dd9f42fa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122451"
---
# <a name="sp_helplogins-transact-sql"></a>sp_helplogins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ログインと各データベースに関連付けられているユーザーに関する情報を提供します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helplogins [ [ @LoginNamePattern = ] 'login' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @LoginNamePattern = ] 'login'` ログイン名です。 *login* のデータ型は **sysname** で、既定値は NULL です。 *ログイン*指定されている場合に存在する必要があります。 場合*ログイン*が指定されていないすべてのログインに関する情報が返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 最初のレポートには、次の表に示すとおり、指定した各ログインに関する情報が含まれます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|ログイン名です。|  
|**SID**|**varbinary(85)**|ログイン セキュリティ識別子 (SID)。|  
|**DefDBName**|**sysname**|既定のデータベースを**LoginName**のインスタンスに接続するときは[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。|  
|**DefLangName**|**sysname**|既定の言語で使用される**LoginName**します。|  
|**Auser**|**char (5)**|Yes = **LoginName**データベースに関連付けられているユーザー名を持っています。<br /><br /> No = **LoginName**関連付けられているユーザー名がありません。|  
|**ARemote**|**char (7)**|Yes = **LoginName**が関連付けられたリモート ログインします。<br /><br /> No = **LoginName**関連付けられたログインはありません。|  
  
 2 番目のレポートには、次の表に示すとおり、各ログインにマップされているユーザーに関する情報、およびログインのロール メンバーシップが含まれています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|ログイン名です。|  
|**DBName**|**sysname**|既定のデータベースを**LoginName**のインスタンスに接続するときは[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。|  
|**UserName**|**sysname**|ユーザー アカウントは、 **LoginName**でマップが**DBName**、およびロールを**LoginName**でのメンバーである**DBName**します。|  
|**UserOrAlias**|**char (8)**|MemberOf = **UserName**は、ロールです。<br /><br /> User = **UserName**はユーザー アカウントです。|  
  
## <a name="remarks"></a>コメント  
 ログインを削除する前に、使用して**sp_helplogins**ログインにマップされているユーザー アカウントを特定します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **securityadmin**固定サーバー ロール。  
  
 指定されたログインにマップされているすべてのユーザー アカウントを識別するために**sp_helplogins**サーバー内のすべてのデータベースを確認する必要があります。 そのため、サーバー上の各データベースの次の条件の少なくとも 1 つ注意してください。  
  
-   実行しているユーザー **sp_helplogins**データベースへのアクセス権があります。  
  
-   **ゲスト**ユーザー アカウントが、データベースで有効にします。  
  
 場合**sp_helplogins** 、データベースにアクセスできない**sp_helplogins**およびエラー メッセージ 15622 が表示できる限り多くの情報を返します。  
  
## <a name="examples"></a>使用例  
 次の例は、ログイン情報を報告`John`します。  
  
```  
EXEC sp_helplogins 'John';  
GO  
  
LoginName SID                        DefDBName DefLangName AUser ARemote   
--------- -------------------------- --------- ----------- ----- -------   
John      0x23B348613497D11190C100C  master    us_english  yes   no  
  
(1 row(s) affected)  
  
LoginName   DBName   UserName   UserOrAlias   
---------   ------   --------   -----------   
John        pubs     John       User          
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_helpdb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [sp_helpuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
