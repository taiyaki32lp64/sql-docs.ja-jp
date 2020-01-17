---
title: CREATE SYMMETRIC KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE SYMMETRIC KEY
- SYMMETRIC KEP
- CREATE_SYMMETRIC_KEY_TSQL
- SYMMETRIC_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE SYMMETRIC KEY statement
- temporary symmetric keys [SQL Server]
- symmetric keys [SQL Server], creating
- symmetric keys [SQL Server]
ms.assetid: b5d23572-b79d-4cf1-9eef-d648fa3b1358
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 485ef972b86795a2127dba5fc3e86bdf98354c7c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68117066"
---
# <a name="create-symmetric-key-transact-sql"></a>CREATE SYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、対称キーを生成し、プロパティを指定します。  
  
 この機能は、データ層アプリケーション フレームワーク (DACFx) を使用してデータベースのエクスポートとの互換性はありません。 エクスポートする前に、すべての対称キーを削除する必要があります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
CREATE SYMMETRIC KEY key_name   
    [ AUTHORIZATION owner_name ]  
    [ FROM PROVIDER provider_name ]  
    WITH 
      [
          <key_options> [ , ... n ]  
        | ENCRYPTION BY <encrypting_mechanism> [ , ... n ] 
      ]
  
<key_options> ::=  
      KEY_SOURCE = 'pass_phrase'  
    | ALGORITHM = <algorithm>  
    | IDENTITY_VALUE = 'identity_phrase'  
    | PROVIDER_KEY_NAME = 'key_name_in_provider'   
    | CREATION_DISPOSITION = {CREATE_NEW | OPEN_EXISTING }  
  
<algorithm> ::=  
    DES | TRIPLE_DES | TRIPLE_DES_3KEY | RC2 | RC4 | RC4_128  
    | DESX | AES_128 | AES_192 | AES_256   
  
<encrypting_mechanism> ::=  
      CERTIFICATE certificate_name   
    | PASSWORD = 'password'   
    | SYMMETRIC KEY symmetric_key_name   
    | ASYMMETRIC KEY asym_key_name  
```  
  
## <a name="arguments"></a>引数  
 *Key_name*  
 対称キーをデータベースで認識するための、一意の名前を指定します。 _key_name_ が 1 つのシャープ記号 (#) で始まる場合、一時キーを指定します。 たとえば、 **#temporaryKey900007** のように指定します。 2 つ以上の # で始まる名前の対称キーは作成できません。 EKM プロバイダーを使用して一時対称キーを作成することはできません。  
  
 AUTHORIZATION *owner_name*  
 対称キーを所有するデータベース ユーザーまたはアプリケーション ロールの名前を指定します。  
  
 FROM PROVIDER *provider_name*  
 拡張キー管理 (EKM) プロバイダーと名前を指定します。 EKM デバイスからはキーがエクスポートされません。 最初に CREATE PROVIDER ステートメントを使用してプロバイダーを定義する必要があります。 外部キー プロバイダーの作成について詳しくは、「[拡張キー管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)」をご覧ください。  
  
> [!NOTE]  
>  このオプションは、包含データベースでは使用できません。  
  
 KEY_SOURCE **='** _pass\_phrase_ **'**  
 キーの派生元のパス フレーズを指定します。  
  
 IDENTITY_VALUE **='** _identity\_phrase_ **'**  
 一時キーで暗号化されるタグ付けデータの GUID の生成元となる ID 句を指定します。  
  
 PROVIDER_KEY_NAME **='** _key\_name\_in\_provider_ **'**  
 拡張キー管理プロバイダーで参照されている名前を指定します。  
  
> [!NOTE]  
>  このオプションは、包含データベースでは使用できません。  
  
 CREATION_DISPOSITION **=** CREATE_NEW  
 拡張キー管理デバイス上で新しいキーを作成します。  デバイスにキーが既に存在する場合は、ステートメントがエラーで失敗します。  
  
 CREATION_DISPOSITION **=** OPEN_EXISTING  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の対称キーを、既存の拡張キー管理キーにマップします。 CREATION_DISPOSITION = OPEN_EXISTING が指定されない場合、この既定値は CREATE_NEW です。  
  
 *certificate_name*  
 対称キーの暗号化に使用する証明書の名前を指定します。 証明書はデータベース内に存在する必要があります。  
  
 **'** *password* **'**  
 対称キーを保護する TRIPLE_DES キーの派生元パスワードを指定します。 *password* は、Windows のパスワード ポリシーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを実行するコンピューターに要求する条件を満足する必要があります。 強力なパスワードを常に使用してください。  
  
 *symmetric_key_name*  
 作成するキーの暗号化に使用する対称キーを指定します。 指定したキーはデータベース内に存在し、開かれている必要があります。  
  
 *asym_key_name*  
 作成するキーの暗号化に使用する非対称キーを指定します。 この非対称キーはデータベース内に存在する必要があります。  
  
 \<algorithm>  
暗号化アルゴリズムを指定します。   
> [!WARNING]  
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]以降、AES_128、AES_192、AES_256 以外のすべてのアルゴリズムが使用されなくなりました。 古いアルゴリズムを使用する場合は (推奨されません)、データベース互換性レベルを 120 以下に設定する必要があります。  
  
## <a name="remarks"></a>Remarks  
 対称キーを作成するときには、証明書、パスワード、対称キー、非対称キー、PROVIDER のうち少なくとも 1 つを使用して対称キーを暗号化する必要があります。 キーには種類ごとの暗号化を複数指定できます。 つまり、1 つの対称キーを、複数の証明書、パスワード、対称キー、および非対称キーを使用して同時に暗号化できます。  
  
> [!CAUTION]  
>  証明書ではなくパスワードを使用して対称キーを暗号化する場合は、パスワードの暗号化に TRIPLE DES 暗号化アルゴリズムが使用されます。 このため、AES など、強力な暗号化アルゴリズムで作成されたキーでも、キー自身はそれより弱いアルゴリズムで保護されます。  
  
 キーを複数のユーザーに配布する前に、追加パスワードを使用して対称キーを暗号化できます。  
  
 一時キーは、そのキーを作成したユーザーが所有します。 また一時キーは、現在のセッションでのみ有効です。  
  
 IDENTITY_VALUE では、新しい対称キーで暗号化されるデータをタグ付けするための GUID が生成されます。 このタグ付けは、キーと暗号化データの照合に使用できます。 特定の句で生成された GUID は常に同じになります。 句を使用して GUID を生成した後は、句を使用してアクティブになっているセッションが 1 つでもあると、同じ句を再度使用することはできません。 IDENTITY_VALUE は省略可能な句ですが、一時キーで暗号化したデータを保存する場合はこの句を使用することをお勧めします。  
  
 既定の暗号化アルゴリズムはありません。  
  
> [!IMPORTANT]  
>  重要なデータの保護には RC4 および RC4_128 ストリーム暗号を使用しないことをお勧めします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、こうしたキーで実行された暗号化をそれ以上エンコードしません。  
  
 対称キーに関する情報は、[sys.symmetric_keys](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md) カタログ ビューで確認できます。  
  
 暗号プロバイダーから作成された対称キーによって、対称キーを暗号化することはできません。  
  
 **DES アルゴリズムに関する説明:**  
  
-   DESX は不適切な名前でした。 ALGORITHM = DESX を使用して作成された対称キーでは、実際には 192 ビット キーを使用した TRIPLE DES 暗号が使用されます。 DESX アルゴリズムは提供されません。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
-   ALGORITHM = TRIPLE_DES_3KEY を使用して作成された対称キーでは、192 ビット キーを使用した TRIPLE DES が使用されます。  
-   ALGORITHM = TRIPLE_DES を使用して作成された対称キーでは、128 ビット キーを使用した TRIPLE DES が使用されます。  
  
 **非推奨の RC4 アルゴリズム:**  
  
 異なるデータ ブロックに対して同じ RC4 または RC4_128 KEY_GUID を繰り返し使用すると、同一の RC4 キーが生成されます。これは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が自動的に salt を提供しないためです。 同一の RC4 キーを繰り返し使用することは、暗号強度を著しく低下させる既知のエラーです。 そのため、RC4 キーワードおよび RC4_128 キーワードは非推奨とされます。 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
> [!WARNING]  
>  RC4 アルゴリズムは、旧バージョンとの互換性のためにのみサポートされています。 データベース互換性レベルが 90 または 100 の場合、新しい素材は RC4 または RC4_128 を使用してのみ暗号化できます (非推奨)。AES アルゴリズムのいずれかなど、新しいアルゴリズムを使用してください。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、どの互換性レベルでも、RC4 または RC4_128 を使用して暗号化された素材を暗号化解除できます。  
  
## <a name="permissions"></a>アクセス許可  
 データベースに対する ALTER ANY SYMMETRIC KEY 権限が必要です。 AUTHORIZATION を指定する場合は、データベース ユーザーに対する IMPERSONATE 権限、またはアプリケーション ロールに対する ALTER 権限が必要です。 証明書または非対称キーを使用して暗号化する場合は、証明書または非対称キーに対する VIEW DEFINITION 権限が必要です。 対称キーを所有できるのは、Windows ログイン、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン、およびアプリケーション ロールだけです。 グループとロールは対称キーを所有できません。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-symmetric-key"></a>A. 対称キーを作成する  
 次の例では、`AES 256` アルゴリズムを使用して対称キー `JanainaKey09` を作成し、新しいキーを証明書 `Shipping04` を使用して暗号化します。  
  
```  
CREATE SYMMETRIC KEY JanainaKey09   
WITH ALGORITHM = AES_256  
ENCRYPTION BY CERTIFICATE Shipping04;  
GO  
```  
  
### <a name="b-creating-a-temporary-symmetric-key"></a>B. 一時対称キーを作成する  
 次の例では、パス フレーズ `#MarketingXXV` から、一時対称キー `The square of the hypotenuse is equal to the sum of the squares of the sides` を作成します。 このキーには文字列 `Pythagoras` から生成された GUID が与えられ、証明書 `Marketing25` を使用して暗号化されます。  
  
```  
  
CREATE SYMMETRIC KEY #MarketingXXV   
WITH ALGORITHM = AES_128,  
KEY_SOURCE   
     = 'The square of the hypotenuse is equal to the sum of the squares of the sides',  
IDENTITY_VALUE = 'Pythagoras'  
ENCRYPTION BY CERTIFICATE Marketing25;  
GO  
```  
  
### <a name="c-creating-a-symmetric-key-using-an-extensible-key-management-ekm-device"></a>C. 拡張キー管理 (EKM) デバイスを使用して対称キーを作成する  
 次の例では、`MyEKMProvider` というプロバイダーとキー名 `KeyForSensitiveData` を使用して、`MySymKey` という対称キーを作成します。 `User1` に承認を割り当てています。また、システム管理者が `MyEKMProvider` というプロバイダーを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に既に登録していることを前提としています。  
  
```  
CREATE SYMMETRIC KEY MySymKey  
AUTHORIZATION User1  
FROM PROVIDER EKMProvider  
WITH  
PROVIDER_KEY_NAME='KeyForSensitiveData',  
CREATION_DISPOSITION=OPEN_EXISTING;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [暗号化アルゴリズムの選択](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [sys.symmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [拡張キー管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [Azure Key Vault を使用する拡張キー管理 &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  
