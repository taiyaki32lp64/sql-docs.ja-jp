---
title: sp_msx_set_account (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_msx_set_account
- sp_msx_set_account_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_set_account
ms.assetid: 314ec720-3a37-48f7-bb6b-8d5b894bf843
author: stevestein
ms.author: sstein
ms.openlocfilehash: 22372412f9c3f905b8978741b556724ca880568c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108019"
---
# <a name="spmsxsetaccount-transact-sql"></a>sp_msx_set_account (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ターゲット サーバーに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのマスター サーバーのアカウント名とパスワードを設定します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_msx_set_account [ @credential_name = ] 'credential_name'  | [ @credential_id = ] credential_id  
```  
  
## <a name="arguments"></a>引数  
`[ @credential_name = ] 'credential_name'` マスター サーバーへのログインに使用する資格情報の名前。 既存の資格情報の名前を指定する必要があります。 いずれか*credential_name*または*credential_id*指定する必要があります。  
  
`[ @credential_id = ] credential_id` マスター サーバーへのログインに使用する資格情報の識別子。 既存の資格情報の識別子を指定する必要があります。 いずれか*credential_name*または*credential_id*指定する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 [なし] :  
  
## <a name="remarks"></a>コメント  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資格情報を使用して、ターゲット サーバーはマスター サーバーにログインを使用してユーザー名とパスワード情報を格納します。 このプロシージャでは、ターゲット サーバーの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがマスター サーバーへのログインで使用する資格情報を設定します。  
  
 既存の資格情報を指定する必要があります。 資格情報の作成の詳細については、次を参照してください。 [CREATE CREDENTIAL &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)します。  
  
## <a name="permissions"></a>アクセス許可  
 実行権限**sp_msx_set_account**既定のメンバーに、 **sysadmin**固定サーバー ロール。  
  
## <a name="examples"></a>使用例  
 次の例では、マスター サーバーへのログインで資格情報 `MsxAccount` を使用するように、サーバーを設定します。  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sp_msx_set_account @credential_name = MsxAccount ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [SQL Server エージェント ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sp_msx_get_account &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-msx-get-account-transact-sql.md)  
  
  
