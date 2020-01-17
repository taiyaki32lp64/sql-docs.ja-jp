---
title: sp_change_users_login (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 12/13/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_users_login
- sp_change_users_login_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_users_login
ms.assetid: 1554b39f-274b-4ef8-898e-9e246b474333
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0594066f044288757e5e31f8e078fabb4c2f3775
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120227"
---
# <a name="sp_change_users_login-transact-sql"></a>sp_change_users_login (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  マップする既存のデータベース ユーザー、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインします。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER USER](../../t-sql/statements/alter-user-transact-sql.md)代わりにします。  
  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_change_users_login [ @Action = ] 'action'   
    [ , [ @UserNamePattern = ] 'user' ]   
    [ , [ @LoginName = ] 'login' ]   
    [ , [ @Password = ] 'password' ]  
[;]  
```  
  
## <a name="arguments"></a>引数  
 [ @Action=] '*アクション*'  
 プロシージャにより実行されるアクションの説明です。 *アクション*は**varchar (10)** します。 *アクション*値は次のいずれかであることができます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**Auto_Fix**|現在のデータベース内の sys.database_principals システム カタログ ビューにあるユーザー エントリを、同じ名前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインにリンクします。 同じ名前のログインが存在しない場合は、新しく作成されます。 結果を**Auto_Fix**ステートメントを正しいリンクが実際に作成されたことを確認します。 使用しないでください**Auto_Fix**セキュリティに影響する場合。<br /><br /> 使用すると**Auto_Fix**を指定する必要があります*ユーザー*と*パスワード*ログインが存在しない場合は、それ以外の場合を指定してください*ユーザー*が*パスワード*は無視されます。 *ログイン*NULL にする必要があります。 *ユーザー*現在のデータベースで有効なユーザーである必要があります。 ログインにマップされている別のユーザーを含めることはできません。|  
|**Report**|現在のデータベース内で、どのログインにもリンクされていないユーザーと、対応するセキュリティ識別子 (SID) を一覧表示します。 *ユーザー*、*ログイン*、および*パスワード*NULL であるか、指定されていません。<br /><br /> レポート オプションのシステム テーブルを使用してクエリに置き換えると、エントリを比較**sys.server_prinicpals**内のエントリに**sys.database_principals**します。|  
|**Update_One**|指定したリンク*ユーザー*を既存の現在のデータベースで[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]*ログイン*します。 *ユーザー*と*ログイン*指定する必要があります。 *パスワード*NULL であるか、指定されていません。|  
  
 [ @UserNamePattern= ] '*user*'  
 現在のデータベース内のユーザーの名前です。 *ユーザー*は**sysname**、既定値は NULL です。  
  
 [ @LoginName= ] '*login*'  
 名前を指定する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインします。 *login* のデータ型は **sysname** で、既定値は NULL です。  
  
 [ @Password= ] '*password*'  
 新しいに割り当てられているパスワード[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を指定して作成したログイン**Auto_Fix**します。 一致するログインが既に存在する場合、ユーザーとログインがマップと*パスワード*は無視されます。 Sp_change_users_login を作成し、新しい一致するログインが存在しない場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインと割り当てます*パスワード*新しいログインのパスワードとして。 *パスワード*は**sysname**NULL にする必要がありません。  
  
> **重要!!** 常に使用して、[強力なパスワード。](../../relational-databases/security/strong-passwords.md)
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|UserName|**sysname**|データベース ユーザー名。|  
|UserSID|**varbinary(85)**|ユーザーのセキュリティ識別子です。|  
  
## <a name="remarks"></a>コメント  
 sp_change_users_login は、現在のデータベースのデータベース ユーザーを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインとリンクする場合に使用します。 ユーザーのログインが既に変更されている場合は、sp_change_users_login を使用してユーザーを新しいログインにリンクすれば、ユーザーの権限が失われることはありません。 新しい*ログイン*sa にすることはできません、*ユーザー*dbo、guest、または INFORMATION_SCHEMA ユーザーにすることはできません。  
  
 sp_change_users_login は、データベース ユーザーを Windows レベルのプリンシパル、証明書、または非対称キーにマップする場合は使用できません。  
  
 sp_change_users_login は、Windows プリンシパルから作成された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインや、CREATE USER WITHOUT LOGIN を使用して作成されたユーザーでは使用できません。  
  
 ユーザー定義のトランザクション内では、sp_change_users_login は実行できません。  
  
## <a name="permissions"></a>アクセス許可  
 db_owner 固定データベース ロールのメンバーシップが必要です。 Sysadmin 固定サーバー ロールのメンバーだけを指定できます、 **Auto_Fix**オプション。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-showing-a-report-of-the-current-user-to-login-mappings"></a>A. 現在のユーザーとログインの対応関係を示すレポートを表示する  
 次の例では、現在のデータベース内のユーザーと各ユーザーのセキュリティ識別子 (SID) を示すレポートを作成します。  
  
```  
EXEC sp_change_users_login 'Report';  
```  
  
### <a name="b-mapping-a-database-user-to-a-new-sql-server-login"></a>B. 新しい SQL Server ログインにデータベース ユーザーのマッピング  
 次の例では、データベース ユーザーは、新しい関連付け[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインします。 データベース ユーザー `MB-Sales`、再マップが別のログインに割り当て先となる最初のログインに`MaryB`します。  
  
```  
--Create the new login.  
CREATE LOGIN MaryB WITH PASSWORD = '982734snfdHHkjj3';  
GO  
--Map database user MB-Sales to login MaryB.  
USE AdventureWorks2012;  
GO  
EXEC sp_change_users_login 'Update_One', 'MB-Sales', 'MaryB';  
GO  
```  
  
### <a name="c-automatically-mapping-a-user-to-a-login-creating-a-new-login-if-it-is-required"></a>C. 新しいログインを作成する必要がある場合、ログインにユーザーを自動的にマッピング  
 次の例は、使用する方法を示します`Auto_Fix`、既存のユーザーを同じ名前のログインにマップするか、作成、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログイン`Mary`パスワードを持つ`B3r12-3x$098f6`場合、ログイン`Mary`存在しません。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_change_users_login 'Auto_Fix', 'Mary', NULL, 'B3r12-3x$098f6';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_helplogins &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  
