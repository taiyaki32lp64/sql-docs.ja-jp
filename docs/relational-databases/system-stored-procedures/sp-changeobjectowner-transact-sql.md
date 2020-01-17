---
title: sp_changeobjectowner (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_changeobjectowner_TSQL
- sp_changeobjectowner
dev_langs:
- TSQL
helpviewer_keywords:
- sp_changeobjectowner
ms.assetid: 45b3dc1c-1cde-45b7-a248-5195c12973e9
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6f00b788ecf6b6e4c02d4b8343ba14fa2c345e6b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056582"
---
# <a name="spchangeobjectowner-transact-sql"></a>sp_changeobjectowner (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在のデータベース内のオブジェクトの所有者を変更します。  
  
> [!IMPORTANT]
>  このストアド プロシージャで使用可能なオブジェクトでのみ動作[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]します。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER SCHEMA](../../t-sql/statements/alter-schema-transact-sql.md)または[ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)代わりにします。 **sp_changeobjectowner**スキーマと所有者の両方を変更します。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] との互換性を維持するために、現在の所有者と新しい所有者がデータベースのユーザー名と同じ名前のスキーマを所有している場合は、このストアド プロシージャはオブジェクトの所有者だけを変更します。  
> 
> [!IMPORTANT]
>  このストアド プロシージャには、新しい権限要件が追加されています。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changeobjectowner [ @objname = ] 'object' , [ @newowner = ] 'owner'  
```  
  
## <a name="arguments"></a>引数  
`[ @objname = ] 'object'` 既存のテーブル、ビュー、ユーザー定義関数、または現在のデータベース内のストアド プロシージャの名前です。 *オブジェクト*は、 **nvarchar (776)** 、既定値はありません。 *オブジェクト*形式で、既存のオブジェクトの所有者で修飾できます_existing_owner_ **.** _オブジェクト_場合は、スキーマとその所有者が同じ名前を指定します。  
  
`[ @newowner = ] 'owner_ '` オブジェクトの新しい所有者となるセキュリティ アカウントの名前です。 *所有者*は**sysname**、既定値はありません。 *所有者*有効なデータベース ユーザー、サーバーの役割をする必要があります[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows ログイン、または現在のデータベースへのアクセス権を持つ Windows グループ。 新しい所有者は、Windows ユーザーまたは Windows グループが対象の対応するデータベース レベルのプリンシパルはありませんが、データベース ユーザーが作成されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_changeobjectowner**オブジェクトからすべての既存のアクセス許可を削除します。 実行後に保持するすべてのアクセス許可を再適用する必要があります**sp_changeobjectowner**します。 実行する前に既存のアクセス許可をスクリプト出力すること勧めそのため、 **sp_changeobjectowner**します。 オブジェクトの所有権が変更された後は、アクセス許可を再適用するのにスクリプトを使用することができます。 権限スクリプトを実行する前に、そのスクリプトでオブジェクトの所有者を変更する必要があります。  
  
 セキュリティ保護可能なオブジェクトの所有者を変更するには、ALTER AUTHORIZATION を使用します。 スキーマを変更するには、ALTER SCHEMA を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **db_owner**両方の固定データベース ロールのメンバーシップまたは、 **db_ddladmin**固定データベース ロール、および**db_securityadmin**固定データベース ロールオブジェクトに対する権限を制御したりします。  
  
## <a name="examples"></a>使用例  
 次の例では、`authors` テーブルの所有者を `Corporate\GeorgeW` に変更します。  
  
```  
EXEC sp_changeobjectowner 'authors', 'Corporate\GeorgeW';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [ALTER SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/alter-schema-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
