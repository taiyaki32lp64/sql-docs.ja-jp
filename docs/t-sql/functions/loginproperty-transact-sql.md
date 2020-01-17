---
title: LOGINPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BadPasswordCount_TSQL
- BadPasswordTime_TSQL
- IsLockedIsMustChange
- PasswordLastSetTime
- LOGINPROPERTY_TSQL
- LockoutTime
- BadPasswordCount
- PasswordHash
- HistoryLengthIsExpired
- LockoutTime_TSQL
- PasswordHash_TSQL
- HistoryLengthIsExpired_TSQL
- PasswordLastSetTime_TSQL
- BadPasswordTime
- IsLockedIsMustChange_TSQL
- LOGINPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- default database
- LOGINPROPERTY function
ms.assetid: b34df777-79b0-49a5-88db-b99998479a5d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 7fb31db6e9b438fbab74a8b23462d8c7dc897d46
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68059763"
---
# <a name="loginproperty-transact-sql"></a>LOGINPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ログインのポリシー設定に関する情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
LOGINPROPERTY ( 'login_name' , 'property_name' )  
```  
  
## <a name="arguments"></a>引数  
 *login_name*  
 ログイン プロパティの状態が返される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの名前です。  
  
 *propertyname*  
 ログインに返されるプロパティ情報を含む式を指定します。 *propertyname* 値は次のいずれかを指定することができます。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|**BadPasswordCount**|正しくないパスワードで連続してログインが試行された回数を返します。|  
|**BadPasswordTime**|正しくないパスワードで最後にログインが試行された時刻を返します。|  
|**DaysUntilExpiration**|パスワードの有効期限が切れるまでの日数を返します。|  
|**DefaultDatabase**|データベースが指定されていない場合に、メタデータまたは **master** に格納されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの既定のデータベースを返します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外でプロビジョニングされているユーザーの場合は NULL を返します (Windows 認証ユーザーなど)。|  
|**DefaultLanguage**|メタデータに格納されているログインの既定の言語を返します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外でプロビジョニングされているユーザーの場合は NULL を返します (Windows 認証ユーザーなど)。|  
|**HistoryLength**|パスワード ポリシーの適用メカニズムを使用して、追跡されたログインのパスワードの数を返します。 パスワード ポリシーが適用されていない場合は 0 です。 パスワード ポリシーの適用は 1 から再開されます。|  
|**IsExpired**|ログインの期限が切れているかどうかを示します。|  
|**IsLocked**|ログインがロックされているかどうかを示します。|  
|**IsMustChange**|次回の接続時にログイン パスワードを変更する必要があるかどうかを示します。|  
|**LockoutTime**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインが、ログイン試行に許容される失敗の回数を超えたためロックアウトされた日付を返します。|  
|**PasswordHash**|パスワードのハッシュを返します。|  
|**PasswordLastSetTime**|現在のパスワードが設定された日付を返します。|  
|**PasswordHashAlgorithm**|パスワードのハッシュに使用されるアルゴリズムを返します。|  
  
## <a name="returns"></a>戻り値  
 データ型は、要求する値によって異なります。  
  
 **IsLocked**、**IsExpired**、**IsMustChange** は **int** 型です。  
  
-   ログインが指定した状態の場合は 1 です。  
  
-   ログインが指定した状態でない場合は 0 です。  
  
 **BadPasswordCount** および **HistoryLength** は **int** 型です。  
  
 **BadPasswordTime**、**LockoutTime**、**PasswordLastSetTime** は **datetime** 型です。  
  
 **PasswordHash** は **varbinary** 型です。  
  
 ログインが有効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインでない場合は NULL です。  
  
 **DaysUntilExpiration** は **int** 型です。  
  
-   ログインの有効期限が切れているか、照会した当日に有効期限が切れる場合は 0 です。  
  
-   Windows のローカル セキュリティ ポリシーでパスワードを無期限にしている場合は -1 です。  
  
-   ログインに対して CHECK_POLICY または CHECK_EXPIRATION が OFF であるか、オペレーティング システムがパスワード ポリシーをサポートしていない場合は NULL です。  
  
 **PasswordHashAlgorithm** は int 型です。  
  
-   SQL7.0 ハッシュの場合は 0  
  
-   SHA-1 ハッシュの場合は 1  
  
-   SHA-2 ハッシュの場合は 2  
  
-   ログインが有効な SQL Server ログインでない場合は NULL  
  
## <a name="remarks"></a>Remarks  
 この組み込み関数では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインのパスワード ポリシー設定に関する情報が返されます。 プロパティの名前の大文字と小文字は区別されません。したがって、**BadPasswordCount** と **badpasswordcount** は同じ意味です。 **PasswordHash、PasswordHashAlgorithm**、および **PasswordLastSetTime** プロパティの値は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のサポート対象の全構成で使用できますが、その他のプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] で実行され、CHECK_POLICY と CHECK_EXPIRATION の両方が有効な場合にのみ使用できます。 詳細については、「 [Password Policy](../../relational-databases/security/password-policy.md)」をご参照ください。  
  
## <a name="permissions"></a>アクセス許可  
 ログインに対する VIEW 権限が必要です。 パスワードのハッシュを要求する場合、CONTROL SERVER 権限も必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-checking-whether-a-login-must-change-its-password"></a>A. ログインがパスワードを変更する必要があるかどうかを確認する  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン `John3` が、次回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続するときにパスワードを変更する必要があるかどうかを確認します。  
  
```  
SELECT LOGINPROPERTY('John3', 'IsMustChange');  
GO  
```  
  
### <a name="b-checking-whether-a-login-is-locked-out"></a>B. ログインがロックアウトされているかどうかを確認する  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン `John3` がロックされているかどうかを確認します。  
  
```  
SELECT LOGINPROPERTY('John3', 'IsLocked');  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
  
