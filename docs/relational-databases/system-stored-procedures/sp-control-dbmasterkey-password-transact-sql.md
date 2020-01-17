---
title: sp_control_dbmasterkey_password (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 02/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_control_dbmasterkey_password
- sp_control_dbmasterkey_password_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_control_dbmasterkey_password
ms.assetid: 63979a87-42a2-446e-8e43-30481faaf3ca
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0af97dacdf5927428042d8e67593a0c6ee78542d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108774"
---
# <a name="spcontroldbmasterkeypassword-transact-sql"></a>sp_control_dbmasterkey_password (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  追加するか、データベース マスター_キーを開くために必要なパスワードを格納している資格情報を削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_control_dbmasterkey_password @db_name = 'database_name,  
     @password = 'master_key_password' , @action = { 'add' | 'drop' }  
```  
  
## <a name="arguments"></a>引数  
 @db_name=N'*database_name*'  
 この資格情報に関連付けられているデータベースの名前を指定します。 システム データベースにすることはできません。 *database_name*は**nvarchar**します。  
  
 @password= N'*パスワード*'  
 マスター キーのパスワードを指定します。 *パスワード*は**nvarchar**します。  
  
 @action= N'add'  
 指定したデータベースの資格情報を、資格情報ストアに追加します。 資格情報には、データベースのマスター キーのパスワードが格納されます。 渡される値@actionは **nvarchar** します。  
  
 @action=N'drop'  
 指定したデータベースの資格情報を、資格情報ストアから削除します。 渡される値@actionは **nvarchar** します。  
  
## <a name="remarks"></a>コメント  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、キーの暗号化解除や暗号化にデータベースのマスター キーが必要となる場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではインスタンスのサービス マスター キーを使用して、データベースのマスター キーの暗号化解除が試行されます。 復号化に失敗した場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のマスター _ キー資格情報をマスター _ キーを必要なデータベースと同じファミリ GUID を持つ資格情報ストアを検索します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、次に、一致した資格情報を順に使用してデータベースのマスター キーの暗号化解除が試行されます。これは暗号化解除が成功するか、資格情報がなくなった時点で終了します。  
  
> [!CAUTION]  
>  Sa およびその他の高い権限を持つサーバー プリンシパルにアクセス可能にする必要があるデータベースのマスター_キー資格情報を作成できません。 データベースのキー階層をサービス マスター キーで暗号化解除できないようにデータベースを構成できます。 このオプションは、- 防御は sa またはその他の高い特権を持つサーバー プリンシパルにアクセスできない暗号化された情報を含むのデータベースとしてサポートされます。 そのようなデータベースのマスター_キー資格情報を作成するには、この防御、データベースの暗号化を解除するには、sa およびその他の高い特権を持つサーバー プリンシパルの有効化が削除されます。  
  
 Sp_control_dbmasterkey_password を使用して作成される資格情報は、 [sys.master_key_passwords](../../relational-databases/system-catalog-views/sys-master-key-passwords-transact-sql.md)カタログ ビューです。 データベース マスター _ キー、次の形式を指定することで作成された資格情報の名前:`##DBMKEY_<database_family_guid>_<random_password_guid>##`します。 パスワードは、資格情報シークレットとして格納されます。 sys.credentials には、資格情報ストアに追加されたパスワードごとに 1 行のデータが格納されます。  
  
 sp_control_dbmasterkey_password を使用して、システム データベース master、model、msdb、または tempdb の資格情報を作成することはできません。  
  
 sp_control_dbmasterkey_password では、指定したデータベースのマスター キーをパスワードで開くことができるかどうかは検証されません。  
  
 指定したデータベースの資格情報に既に格納されているパスワードを指定した場合、sp_control_dbmasterkey_password は失敗します。  
  
> [!NOTE]  
>  異なるサーバー インスタンスの 2 つのデータベースで、同じファミリ GUID を共有することができます。 この場合、両方のデータベースの資格情報ストア内で同じマスター キー レコードが共有されます。  
  
 sp_control_dbmasterkey_password に渡されるパラメーターは、トレースには表示されません。  
  
> [!NOTE]  
>  sp_control_dbmasterkey_password を使用して追加された資格情報を使ってデータベース マスター キーを開く場合、そのデータベース マスター キーはサービス マスター キーによって再暗号化されます。 データベースが読み取り専用モードの場合は、再暗号化操作は失敗し、データベース マスター _ キーは暗号化されません。 後続のアクセスをデータベース マスター _ キーでは、OPEN MASTER KEY ステートメントとパスワードを使用する必要があります。 パスワードの使用を避けるには、データベースを読み取り専用モードに移行する前に、資格情報を作成するようにしてください。  
  
 **潜在的な下位互換性の問題点:** 現時点では、ストアド プロシージャでは、マスター _ キーが存在するかどうかは調べません。 これは下位互換性を確保するために許容されていますが、警告が表示されます。 ただし、この動作は非推奨とされます。 マスター _ キーが存在する必要があります、将来のリリースと、ストアド プロシージャで使用されるパスワード**sp_control_dbmasterkey_password**データベース マスター _ キーの暗号化に使用されるパスワードの 1 つとして同じパスワードをする必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 データベースに対する CONTROL 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-credential-for-the-adventureworks2012-master-key"></a>A. AdventureWorks2012 マスター_キーの資格情報の作成  
 次の例では、`AdventureWorks2012` データベースのマスター キーの資格情報を作成し、マスター キーのパスワードをシークレットとして資格情報に保存します。 ため、すべてのパラメーターに渡される`sp_control_dbmasterkey_password`データ型でなければなりません**nvarchar**、テキスト文字列はキャスト演算子により変換されます`N`します。  
  
```  
EXEC sp_control_dbmasterkey_password @db_name = N'AdventureWorks2012',   
    @password = N'sdfjlkj#mM00sdfdsf98093258jJlfdk4', @action = N'add';  
GO  
```  
  
### <a name="b-dropping-a-credential-for-a-database-master-key"></a>B. データベースのマスター キーの資格情報を削除する  
 次の例では、A. は、すべてのパラメーターが必要ですが、パスワードを含むことに注意してください。 例で作成した資格情報を削除します。  
  
```  
EXEC sp_control_dbmasterkey_password @db_name = N'AdventureWorks2012',   
    @password = N'sdfjlkj#mM00sdfdsf98093258jJlfdk4', @action = N'drop';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [暗号化されたミラー データベースの設定](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)   
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [資格情報 &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)  
  
  
