---
title: CREATE ASYMMETRIC KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ASYMMETRIC_KEY_TSQL
- CREATE ASYMMETRIC KEY
- CREATE_ASYMMETRIC_KEY_TSQL
- ASYMMETRIC KEY
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], creating
- encryption [SQL Server], asymmetric keys
- CREATE ASYMMETRIC KEY statement
- asymmetric keys [SQL Server]
- cryptography [SQL Server], asymmetric keys
ms.assetid: 141bc976-7631-49f6-82bd-a235028645b1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 009029f16d85fa82867f37e075066701dacfc375
ms.sourcegitcommit: e9c1527281f2f3c7c68981a1be94fe587ae49ee9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2019
ms.locfileid: "73064689"
---
# <a name="create-asymmetric-key-transact-sql"></a>CREATE ASYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  データベースに非対称キーを作成します。  
  
 この機能は、データ層アプリケーション フレームワーク (DACFx) を使用してデータベースのエクスポートとの互換性はありません。 エクスポートする前にすべての非対称キーを削除する必要があります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
CREATE ASYMMETRIC KEY asym_key_name   
   [ AUTHORIZATION database_principal_name ]  
   [ FROM <asym_key_source> ]  
   [ WITH <key_option> ] 
   [ ENCRYPTION BY <encrypting_mechanism> ] 
   [ ; ]
  
<asym_key_source>::=  
     FILE = 'path_to_strong-name_file'  
   | EXECUTABLE FILE = 'path_to_executable_file'  
   | ASSEMBLY assembly_name  
   | PROVIDER provider_name  
  
<key_option> ::=  
   ALGORITHM = <algorithm>  
      |  
   PROVIDER_KEY_NAME = 'key_name_in_provider'  
      |  
      CREATION_DISPOSITION = { CREATE_NEW | OPEN_EXISTING }  
  
<algorithm> ::=  
      { RSA_4096 | RSA_3072 | RSA_2048 | RSA_1024 | RSA_512 }   
  
<encrypting_mechanism> ::=  
    PASSWORD = 'password'   
```  
  
## <a name="arguments"></a>引数  
 *asym_key_name*  
 データベース内の非対称キーの名前です。 非対称キー名は、[識別子](../../relational-databases/databases/database-identifiers.md)のルールに従うと共に、データベース内で一意である必要があります。  

 AUTHORIZATION *database_principal_name*  
 非対称キーの所有者を指定します。 所有者がロールまたはグループになることはできません。 このオプションを省略した場合、所有者は現在のユーザーになります。  
  
 FROM *asym_key_source*  
 非対称キー ペアの読み込み元を指定します。  
  
 FILE = '*path_to_strong-name_file*'  
 キー ペアの読み込み元となる、厳密な名前のファイルのパスを指定します。 Windows API の MAX_PATH による 260 文字までの制限があります。  
  
> [!NOTE]  
>  このオプションは、包含データベースでは使用できません。  
  
 EXECUTABLE FILE = '*path_to_executable_file*'  
 公開キーの読み込み元となる、アセンブリ ファイルのパスを指定します。 Windows API の MAX_PATH による 260 文字までの制限があります。  
  
> [!NOTE]  
>  このオプションは、包含データベースでは使用できません。  
  
 ASSEMBLY *assembly_name*  
 公開キーの読み込み元となるデータベースに既に読み込まれている署名付きアセンブリの名前を指定します。  
  
 PROVIDER *provider_name*  
 拡張キー管理 (EKM) プロバイダーの名前を指定します。 最初に CREATE PROVIDER ステートメントを使用してプロバイダーを定義する必要があります。 外部キーの管理について詳しくは、「[拡張キー管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)」をご覧ください。  
  
 ALGORITHM = \<algorithm>  
 指定できるアルゴリズムは、RSA_4096、RSA_3072、RSA_2048、RSA_1024、RSA_512 の 5 つです。  
  
 RSA_1024 と RSA_512 は非推奨とされました。 RSA_1024 または RSA_512 を使う場合は (推奨されません)、データベース互換性レベルを 120 以下に設定する必要があります。  
  
 PROVIDER_KEY_NAME = '*key_name_in_provider*'  
 外部プロバイダーからキー名を指定します。  
  
 CREATION_DISPOSITION = CREATE_NEW  
 拡張キー管理デバイス上で新しいキーを作成します。 デバイス上のキー名を指定するには、PROVIDER_KEY_NAME を使用する必要があります。 デバイスにキーが既に存在する場合は、ステートメントがエラーで失敗します。  
  
 CREATION_DISPOSITION = OPEN_EXISTING  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の非対称キーを、既存の拡張キー管理キーにマップします。 デバイス上のキー名を指定するには、PROVIDER_KEY_NAME を使用する必要があります。 CREATION_DISPOSITION = OPEN_EXISTING が指定されない場合、既定値は CREATE_NEW です。  
  
 ENCRYPTION BY PASSWORD = '*password*'  
 秘密キーを暗号化するパスワードを指定します。 この句が存在しない場合、秘密キーはデータベースのマスター キーで暗号化されます。 *password* は最大 128 文字です。 *password* は、Windows のパスワード ポリシーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを実行するコンピューターに要求する条件を満足する必要があります。  
  
## <a name="remarks"></a>Remarks  
 "*非対称キー*" は、データベース レベルのセキュリティ保護可能なエンティティです。 既定の形式では、このエンティティには公開キーと秘密キーの両方が含まれます。 FROM 句を使用せずに CREATE ASYMMETRIC KEY を実行した場合は、新しいキー ペアが作成されます。 FROM 句を使用して CREATE ASYMMETRIC KEY を実行した場合は、ファイルからキー ペアがインポートされるか、アセンブリまたは DLL ファイルから公開キーがインポートされます。  
  
 既定では、秘密キーはデータベースのマスター キーによって保護されます。 データベースのマスター キーが作成されていない場合、秘密キーを保護するにはパスワードが必要です。  
  
 秘密キーは、512、1,024、または 2,048 ビットの長さで指定できます。  
  
## <a name="permissions"></a>アクセス許可  
 データベースに対する CREATE ASYMMETRIC KEY 権限が必要です。 AUTHORIZATION 句を指定する場合は、データベース プリンシパルに対する IMPERSONATE 権限、またはアプリケーション ロールに対する ALTER 権限が必要です。 非対称キーを所有できるのは、Windows ログイン、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン、およびアプリケーション ロールだけです。 グループとロールによる非対称キーの所有はできません。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-an-asymmetric-key"></a>A. 非対称キーを作成する  
 次の例では、`RSA_2048` アルゴリズムを使って `PacificSales09` という非対称キーを作成し、パスワードで秘密キーを保護します。  
  
```sql  
CREATE ASYMMETRIC KEY PacificSales09   
    WITH ALGORITHM = RSA_2048   
    ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>';   
GO  
```  
  
### <a name="b-creating-an-asymmetric-key-from-a-file-giving-authorization-to-a-user"></a>B. 非対称キーをファイルから作成し、ユーザーを認証する  
 次の例では、ファイルに格納されたキー ペアから非対称キー `PacificSales19` を作成し、その非対称キーの所有権をユーザー `Christina` に割り当てます。 秘密キーは、データベース マスター キーによって保護され、非対称キーを作成する前に作成される必要があります。  
  
```sql  
CREATE ASYMMETRIC KEY PacificSales19  
    AUTHORIZATION Christina  
    FROM FILE = 'c:\PacSales\Managers\ChristinaCerts.tmp';  
GO  
```  
  
### <a name="c-creating-an-asymmetric-key-from-an-ekm-provider"></a>C. EKM プロバイダーから非対称キーを作成する  
 次の例では、`EKM_Provider1` という拡張キー管理プロバイダーに格納されているキー ペアから非対称キー `EKM_askey1` を作成し、そのプロバイダー上の `key10_user1` というキーを作成します。  
  
```sql  
CREATE ASYMMETRIC KEY EKM_askey1   
    FROM PROVIDER EKM_Provider1  
    WITH   
        ALGORITHM = RSA_2048,   
        CREATION_DISPOSITION = CREATE_NEW  
        , PROVIDER_KEY_NAME  = 'key10_user1' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)  
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)  
 [ASYMKEYPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/asymkeyproperty-transact-sql.md)  
 [ASYMKEY_ID &#40;Transact-SQL&#41;](../../t-sql/functions/asymkey-id-transact-sql.md)  
 [暗号化アルゴリズムの選択](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
 [Azure Key Vault を使用する拡張キー管理 &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  
