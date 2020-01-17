---
title: CREATE COLUMN MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SQL13.SWB.NEWCOLUMNMASTERKEYDEF.GENERAL.F1
- SQL13.SWB.COLUMNMASTERKEYDEF.GENERAL.F1
- CREATE COLUMN MASTER KEY
- COLUMN MASTER KEY
- CREATE_COLUMN_MASTER_KEY_TSQL
- COLUMN_MASTER_KEY_TSQL
- SQL13.SWB.NEWCOLUMNMASTERKEY.GENERAL.F1
- SQL13.SWB.COLUMNMASTERKEY.GENERAL.F1
dev_langs:
- TSQL
helpviewer_keywords:
- column master key definition
- column master key, create
- CREATE COLUMN MASTER KEY statement
- Always Encrypted, create column master key
ms.assetid: f8926b95-e146-4e3f-b56b-add0c0d0a30e
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: cd6148499c6e9d906d0077632001d3fe32ce9cc3
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593893"
---
# <a name="create-column-master-key-transact-sql"></a>CREATE COLUMN MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

データベースに列マスター キー メタデータ オブジェクトを作成します。 列マスター キー メタデータ エントリは、外部キー ストアに格納されたキーを表します。 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) または[セキュリティで保護されたエンクレーブが設定された Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md) を使用していると、そのキーによって列暗号化キーが保護 (暗号化) されます。 複数の列マスター キーを使用してキーのローテーションを定期的に行い、セキュリティを強化できます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のオブジェクト エクスプローラーまたは PowerShell を使用して、キー ストアに列マスター キーを作成し、データベースに関連するメタデータ オブジェクトを作成します。 詳しくは、「[Always Encrypted のキー管理の概要](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)」をご覧ください。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 

> [!IMPORTANT]
> (ENCLAVE_COMPUTATIONS を使用した) エンクレーブ対応のキーの作成には、[セキュリティで保護されたエンクレーブが設定された Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md) が必要です。

## <a name="syntax"></a>構文  

``` sql 
CREATE COLUMN MASTER KEY key_name   
    WITH (  
        KEY_STORE_PROVIDER_NAME = 'key_store_provider_name',  
        KEY_PATH = 'key_path'   
        [,ENCLAVE_COMPUTATIONS (SIGNATURE = signature)]
         )   
[;]  
```  
  
## <a name="arguments"></a>引数  
*key_name*  
データベース内の列マスター キーの名前。  
  
*key_store_provider_name*  
キー ストア プロバイダーの名前を指定します。 キー ストア プロバイダーは、列マスター キーが含まれるキー ストアを保持するクライアント側ソフトウェア コンポーネントです。 

Always Encrypted が有効なクライアント ドライバーでは次のことが行われます。

- キー ストア プロバイダー名が使用されます 
- キー ストア プロバイダーのドライバーのレジストリでキー ストア プロバイダーが検索されます 

その後、ドライバーでは、プロバイダーを使用して列暗号化キーの暗号化が解除されます。 列暗号化キーは、列マスター キーによって保護されています。 列マスター キーは、基になるキー ストアに格納されています。 その後、列暗号化キーのプレーンテキスト値を使用して、暗号化されたデータベースの列に対応するクエリ パラメーターが暗号化されます。 または、列暗号化キーで、暗号化された列からのクエリ結果の暗号化が解除されます。  
  
Always Encrypted が有効なクライアント ドライバー ライブラリには、一般的なキー ストア用のキー ストア プロバイダーが含まれます。   
  
使用可能なプロバイダーのセットは、クライアント ドライバーの種類とバージョンによって異なります。 特定のドライバーについては、Always Encrypted の次のドキュメントをご覧ください。[Always Encrypted を使用したアプリケーションの開発](../../relational-databases/security/encryption/always-encrypted-client-development.md)。


次の表では、システム プロバイダーの名前を示します。  
  
|キー ストア プロバイダーの名前|基になっているキー ストア|  
    |-----------------------------|--------------------------|
    |'MSSQL_CERTIFICATE_STORE'|Windows 証明書ストア| 
    |'MSSQL_CSP_PROVIDER'|Microsoft CryptoAPI をサポートするハードウェア セキュリティ モジュール (HSM) などのストア。|
    |'MSSQL_CNG_STORE'|ハードウェア セキュリティ モジュール (HSM) など、Cryptography API: Next Generation をサポートするストア。|  
    |'AZURE_KEY_VAULT'|「[Azure Key Vault の使用を開始する](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)」をご覧ください|  
    |'MSSQL_JAVA_KEYSTORE'| Java キー ストア。
  

Always Encrypted が有効なクライアント ドライバーでは、組み込みのキー ストア プロバイダーがない列マスター キーを格納するカスタム キー ストア プロバイダーを設定することができます。 カスタム キー ストア プロバイダーの名前を "MSSQL_" で始めることはできません。これは、[!INCLUDE[msCoName](../../includes/msconame-md.md)] キー ストア プロバイダー用に予約されているプレフィックスです。 

  
key_path  
列マスター キー ストア内のキーのパス。 キーのパスは、データを暗号化および暗号化を解除することが予想される各クライアント アプリケーションに対して有効である必要があります。 データは、参照されている列マスター キーによって (間接的に) 保護されている列に格納されます。 クライアント アプリケーションには、キーへのアクセス権が必要です。 キーのパスの形式は、キー ストア プロバイダーに固有です。 次の一覧では、特定の Microsoft システム キー ストア プロバイダーのキー パスの形式を説明します。  
  
-   **プロバイダー名:** MSSQL_CERTIFICATE_STORE  
  
    **キーのパスの形式:** *CertificateStoreName*/*CertificateStoreLocation*/*CertificateThumbprint*  
  
     各要素の説明は次のとおりです。  
  
    *CertificateStoreLocation*  
    証明書ストアの場所。現在のユーザーまたはローカル マシンにする必要があります。 詳しくは、「[Local Machine and Current User Certificate Stores](https://msdn.microsoft.com/library/windows/hardware/ff548653.aspx)」(ローカル マシンおよび現在のユーザーの証明書ストア) をご覧ください。  
  
    *CertificateStore*  
    証明書ストアの名前 (例: "My")。  
  
    *CertificateThumbprint*  
    証明書のサムプリント。  
  
    **使用例:**  
  
    ```  
    N'CurrentUser/My/BBF037EC4A133ADCA89FFAEC16CA5BFA8878FB94'  
  
    N'LocalMachine/My/CA5BFA8878FB94BBF037EC4A133ADCA89FFAEC16'  
    ```  
  
-   **プロバイダー名:** MSSQL_CSP_PROVIDER  
  
    **キーのパスの形式:** *ProviderName*/*KeyIdentifier*  
  
    各要素の説明は次のとおりです。  
  
    *ProviderName*  
    列マスター キー ストアの暗号サービス プロバイダー (CSP) の名前。CAPI が実装されています。 キー ストアとして HSM を使用する場合、プロバイダー名は HSM ベンダー提供の CSP の名前にする必要があります。 クライアント コンピューターにプロバイダーをインストールする必要があります。  
  
    *KeyIdentifier*  
    キー ストア内のキーの識別子。列マスター キーとして使用されます。  
  
    **使用例:**  
  
    ```  
    N'My HSM CSP Provider/AlwaysEncryptedKey1'  
    ```  
  
-   **プロバイダー名:** MSSQL_CNG_STORE  
  
    **キーのパスの形式:** *ProviderName*/*KeyIdentifier*  
  
    各要素の説明は次のとおりです。  
  
    *ProviderName*  
    列マスター キー ストアのキー ストレージ プロバイダー (KSP) の名前。Cryptography: Next Generation (CNG) API が実装されています。 キー ストアとして HSM を使用する場合、プロバイダー名は HSM ベンダー提供の KSP の名前にする必要があります。 クライアント コンピューターにプロバイダーをインストールする必要があります。  
  
    *KeyIdentifier*  
    キー ストア内のキーの識別子。列マスター キーとして使用されます。  
  
    **使用例:**  
  
    ```  
    N'My HSM CNG Provider/AlwaysEncryptedKey1'  
    ```  

-   **プロバイダー名:** AZURE_KEY_STORE  
  
    **キーのパスの形式:** *KeyUrl*  
  
    各要素の説明は次のとおりです。  
  
    *KeyUrl*  
    Azure Key Vault 内のキーの URL

ENCLAVE_COMPUTATIONS  
列マスター キーがエンクレーブ対応であることを指定します。 列マスター キーで暗号化されたすべての列暗号化キーを、サーバー側のセキュリティで保護されたエンクレーブと共有し、エンクレーブ内の計算に使用できます。 詳細については、「[セキュア エンクレーブを使用する Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)」を参照してください。

*signature*  
"*キーのパス*" のデジタル署名と列マスター キーでの ENCLAVE_COMPUTATIONS の設定の結果であるバイナリ リテラル。 署名には、ENCLAVE_COMPUTATIONS が指定されているかどうかが反映されます。 この署名は、承認されていないユーザーが符号付きの値を変更できないようにします。 Always Encrypted 対応のクライアント ドライバーでは、署名が検証されて、署名が無効な場合はアプリケーションにエラーが返されます。 署名は、クライアント側のツールを使用して生成されている必要があります。 詳細については、「[セキュア エンクレーブを使用する Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)」を参照してください。
  
  
## <a name="remarks"></a>Remarks  

データベースに列暗号化キー メタデータ エントリを作成する前、および Always Encrypted を使用してデータベース内の列を暗号化する前に、列マスター キー メタデータ エントリを作成します。 メタデータ内の列マスター キー エントリには、実際の列マスター キーは含まれません。 列マスター キーは、(SQL Server の外部にある) 外部列キー ストアに格納する必要があります。 メタデータ内のキー ストア プロバイダー名と列マスター キー パスは、クライアント アプリケーションに対して有効である必要があります。 クライアント アプリケーションでは、列マスター キーを使用して、列暗号化キーの暗号化を解除する必要があります。 列暗号化キーは、列マスター キーで暗号化されています。 また、クライアント アプリケーションでは、暗号化された列のクエリを実行する必要があります。

SQL Server Management Studio (SSMS) や PowerShell などのツールを使って、列マスター キーを管理することをお勧めします。 そのようなツールを使うと、署名を生成し (セキュリティで保護されたエンクレーブが設定された Always Encrypted を使っている場合)、`CREATE COLUMN MASTER KEY` ステートメントを自動的に発行して列暗号化キーのメタデータ オブジェクトを作成することができます。 「[SQL Server Management Studio を使用して Always Encrypted キーをプロビジョニングする](../../relational-databases/security/encryption/configure-always-encrypted-keys-using-ssms.md)」および「[PowerShell を使用した Always Encrypted キーのプロビジョニング](../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md)」を参照してください。 

  
## <a name="permissions"></a>アクセス許可  
**ALTER ANY COLUMN MASTER KEY** 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-column-master-key"></a>A. 列マスター キーを作成する  
次の例では、列マスター キーの列マスター キー メタデータ エントリを作成します。 列マスター キーは、MSSQL_CERTIFICATE_STORE プロバイダーを使用して列マスター キーにアクセスするクライアント アプリケーションの証明書ストアに格納されます。  
  
```sql  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
   );  
```  
  
列マスター キーの列マスター キー メタデータ エントリを作成します。 MSSQL_CNG_STORE プロバイダーを使用するクライアント アプリケーションが、列マスター キーにアクセスします。  
  
```sql  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CNG_STORE',    
    KEY_PATH = N'My HSM CNG Provider/AlwaysEncryptedKey'  
);  
```  
  
列マスター キーの列マスター キー メタデータ エントリを作成します。 列マスター キーは、AZURE_KEY_VAULT プロバイダーを使用して列マスター キーにアクセスするクライアント アプリケーション用に、Azure キー コンテナーに格納されます。  
  
```sql  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',  
    KEY_PATH = N'https://myvault.vault.azure.net:443/keys/  
        MyCMK/4c05f1a41b12488f9cba2ea964b6a700');  
```  
  
列マスター キーの列マスター キー メタデータ エントリを作成します。 列マスター キーは、カスタム列マスター キー ストアに格納されます。  
  
```sql  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = 'CUSTOM_KEY_STORE',    
    KEY_PATH = 'https://contoso.vault/sales_db_tce_key'  
);  
```  
### <a name="b-creating-an-enclave-enabled-column-master-key"></a>B. エンクレーブ対応の列マスター キーを作成します  
次の例では、エンクレーブ対応の列マスター キーに対する列マスター キー メタデータ エントリを作成します。 エンクレーブ対応の列マスター キーは、MSSQL_CERTIFICATE_STORE プロバイダーを使用して列マスター キーにアクセスするクライアント アプリケーションの証明書ストアに格納されます。  
  
```sql  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
     ENCLAVE_COMPUTATIONS (SIGNATURE = 0xA80F5B123F5E092FFBD6014FC2226D792746468C901D9404938E9F5A0972F38DADBC9FCBA94D9E740F3339754991B6CE26543DEB0D094D8A2FFE8B43F0C7061A1FFF65E30FDDF39A1B954F5BA206AAC3260B0657232020542419990261D878318CC38EF4E853970ED69A8D4A306693B8659AAC1C4E4109DE5EB148FD0E1FDBBC32F002C1D8199D313227AD689279D8DEEF91064DF122C19C3767C463723AB663A6F8412AE17E745922C0E3A257EAEF215532588ACCBD440A03C7BC100A38BD0609A119E1EF7C5C6F1B086C68AB8873DBC6487B270340E868F9203661AFF0492CEC436ABF7C4713CE64E38CF66C794B55636BFA55E5B6554AF570CF73F1BE1DBD)
  );  
```  
  
エンクレーブ対応の列マスター キーに対する列マスター キー メタデータ エントリを作成します。 エンクレーブ対応の列マスター キーは、AZURE_KEY_VAULT プロバイダーを使用して列マスター キーにアクセスするクライアント アプリケーション用に、Azure キー コンテナーに格納されます。  
  
```sql  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',  
    KEY_PATH = N'https://myvault.vault.azure.net:443/keys/MyCMK/4c05f1a41b12488f9cba2ea964b6a700');
    ENCLAVE_COMPUTATIONS (SIGNATURE = 0xA80F5B123F5E092FFBD6014FC2226D792746468C901D9404938E9F5A0972F38DADBC9FCBA94D9E740F3339754991B6CE26543DEB0D094D8A2FFE8B43F0C7061A1FFF65E30FDDF39A1B954F5BA206AAC3260B0657232020582413990261D878318CC38EF4E853970ED69A8D4A306693B8659AAC1C4E4109DE5EB148FD0E1FDBBC32F002C1D8199D313227AD689279D8DEEF91064DF122C19C3767C463723AB663A6F8412AE17E745922C0E3A257EAEF215532588ACCBD440A03C7BC100A38BD0609A119E1EF7C5C6F1B086C68AB8873DBC6487B270340E868F9203661AFF0492CEC436ABF7C4713CE64E38CF66C794B55636BFA55E5B6554AF570CF73F1BE1DBD)
  );
```  
  
## <a name="see-also"></a>参照
 
* [DROP COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-master-key-transact-sql.md)   
* [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)
* [sys.column_master_keys (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
* [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
* [セキュリティで保護されたエンクレーブが設定された Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
* [Always Encrypted のキー管理の概要](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
* [セキュリティで保護されたエンクレーブが設定された Always Encrypted のキーの管理](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)   
  
