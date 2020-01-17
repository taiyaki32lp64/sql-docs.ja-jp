---
title: ALTER COLUMN ENCRYPTION KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER COLUMN ENCRYPTION
- ALTER_COLUMN_ENCRYPTION_TSQL
- ALTER COLUMN ENCRYPTION KEY
- ALTER_COLUMN_ENCRYPTION_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column encryption key, alter
- ALTER COLUMN ENCRYPTION KEY statement
ms.assetid: c79a220d-e178-4091-a330-c924cc0f0ae0
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: c06fb5b28e1c3ec5bd50b8922bcdf1e5d1b27ff7
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594392"
---
# <a name="alter-column-encryption-key-transact-sql"></a>ALTER COLUMN ENCRYPTION KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  データベースで、暗号化された値を追加または削除する列暗号化キーを変更します。 列暗号化キーは、対応する列マスター キーのローテーションで最大 2 つの値を持つことができます。 列暗号化キーは、[Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) または[セキュリティで保護されたエンクレーブが設定された Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md) を使用して列を暗号化するときに使用されます。 列暗号化キーの値を追加する前に、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [CREATE MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) ステートメントを使用して、値の暗号化に使用された列マスター キーを定義する必要があります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
ALTER COLUMN ENCRYPTION KEY key_name   
    [ ADD | DROP ] VALUE   
    (  
        COLUMN_MASTER_KEY = column_master_key_name   
        [, ALGORITHM = 'algorithm_name' , ENCRYPTED_VALUE =  varbinary_literal ]   
    ) [;]  
```  
  
## <a name="arguments"></a>引数  
 *key_name*  
 変更する、列の暗号化キー。  
  
 *column_master_key_name*  
 列の暗号化キー (CEK) を暗号化するために使用される列マスター キー (CMK) の名前を指定します。  
  
 *algorithm_name*  
 値を暗号化するために使用する暗号化アルゴリズムの名前です。 システム プロバイダーのアルゴリズムは、**RSA_OAEP** である必要があります。 列の暗号化キーの値を削除するときに、この引数は有効ではありません。  
  
 *varbinary_literal*  
 指定されたマスター暗号化キーを使用して暗号化された CEK BLOB。 列の暗号化キーの値を削除するときに、この引数は有効ではありません。  
  
> [!WARNING]  
>  このステートメントでは、プレーンテキストの CEK 値を渡さないでください。 そうすれば、この機能の利点が得られます。  
  
## <a name="remarks"></a>Remarks  
通常、列暗号化キーは、暗号化された値を 1 つだけ使用して作成されます。 列マスター キーを回転する必要がある場合 (現在の列マスター キーを新しい列マスター キーと置き換える必要がある場合)、新しい列マスター キーで暗号化された新しい値の列暗号化キーを追加できます。 このワークフローにより、クライアント アプリケーションが新しい列マスター キーを使用できるようになるまでの間、クライアント アプリケーションが列暗号化キーを使用して暗号化されたデータにアクセスできるようになります。 新しいマスター キーにアクセスできないクライアント アプリケーションでも、Always Encrypted が有効にされたドライバーは、古い列マスター キーで暗号化された列暗号化キー値を使用して機密データにアクセスできます。 Always Encrypted でサポートされる暗号化アルゴリズムでは、プレーンテキスト値が 256 ビットである必要があります。 
 
SQL Server Management Studio (SSMS) や PowerShell などのツールを使って、列マスター キーをローテーションすることをお勧めします。 「[SQL Server Management Studio を使用した Always Encrypted キーの交換](../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-ssms.md)」および「[PowerShell を使用して Always Encrypted キーをローテーションする](../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)」をご覧ください。

暗号化された値は、列のマスター キーを保持するキー ストアをカプセル化するキー ストア プロバイダーを使用して生成する必要があります。  

 列マスター キーは、次の理由でローテーションされます。
- 法令に遵守するためにキーを定期的にローテーションする必要があります。
- 列マスター キーのセキュリティが侵害されたためにローテーションする必要があります。
- サーバー側のセキュリティで保護されたエンクレーブと列の暗号化キーの共有を有効または無効にします。 たとえば、現在使用中の列マスター キーがエンクレーブ計算をサポートしていない場合 (ENCLAVE_COMPUTATIONS プロパティで定義されていない場合)、お使いの列マスター キーで暗号化されている列暗号化キーを使用して保護されている列でエンクレーブ計算を有効にしたい場合、ENCLAVE_COMPUTATIONS プロパティで列マスター キーを新しいキーと置き換える必要があります。 「[Always Encrypted のキー管理の概要](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)」および「[セキュリティで保護されたエンクレーブが設定された Always Encrypted のキーを管理する](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)」。

列暗号化キーについての情報を表示するには、[sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)、[sys.column_encryption_keys  &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)、[sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md) を使います。  
  
## <a name="permissions"></a>アクセス許可  
 データベースに対する **ALTER ANY COLUMN ENCRYPTION KEY** 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-adding-a-column-encryption-key-value"></a>A. 列の暗号化キーの値を追加する  
 次の例と呼ばれる列の暗号化キーを変更する `MyCEK`です。  
  
```sql  
ALTER COLUMN ENCRYPTION KEY MyCEK  
ADD VALUE  
(  
    COLUMN_MASTER_KEY = MyCMK2,   
    ALGORITHM = 'RSA_OAEP',   
    ENCRYPTED_VALUE = 0x016E000001630075007200720065006E00740075007300650072002F006D0079002F0064006500650063006200660034006100340031003000380034006200350033003200360066003200630062006200350030003600380065003900620061003000320030003600610037003800310066001DDA6134C3B73A90D349C8905782DD819B428162CF5B051639BA46EC69A7C8C8F81591A92C395711493B25DCBCCC57836E5B9F17A0713E840721D098F3F8E023ABCDFE2F6D8CC4339FC8F88630ED9EBADA5CA8EEAFA84164C1095B12AE161EABC1DF778C07F07D413AF1ED900F578FC00894BEE705EAC60F4A5090BBE09885D2EFE1C915F7B4C581D9CE3FDAB78ACF4829F85752E9FC985DEB8773889EE4A1945BD554724803A6F5DC0A2CD5EFE001ABED8D61E8449E4FAA9E4DD392DA8D292ECC6EB149E843E395CDE0F98D04940A28C4B05F747149B34A0BAEC04FFF3E304C84AF1FF81225E615B5F94E334378A0A888EF88F4E79F66CB377E3C21964AACB5049C08435FE84EEEF39D20A665C17E04898914A85B3DE23D56575EBC682D154F4F15C37723E04974DB370180A9A579BC84F6BC9B5E7C223E5CBEE721E57EE07EFDCC0A3257BBEBF9ADFFB00DBF7EF682EC1C4C47451438F90B4CF8DA709940F72CFDC91C6EB4E37B4ED7E2385B1FF71B28A1D2669FBEB18EA89F9D391D2FDDEA0ED362E6A591AC64EF4AE31CA8766C259ECB77D01A7F5C36B8418F91C1BEADDD4491C80F0016B66421B4B788C55127135DA2FA625FB7FD195FB40D90A6C67328602ECAF3EC4F5894BFD84A99EB4753BE0D22E0D4DE6A0ADFEDC80EB1B556749B4A8AD00E73B329C95827AB91C0256347E85E3C5FD6726D0E1FE82C925D3DF4A9  
);  
GO  
  
```  
  
### <a name="b-dropping-a-column-encryption-key-value"></a>B. 列の暗号化キーの値を削除する  
 次の例と呼ばれる列の暗号化キーを変更する `MyCEK` 値を削除することによりします。  
  
```sql  
ALTER COLUMN ENCRYPTION KEY MyCEK  
DROP VALUE  
(  
    COLUMN_MASTER_KEY = MyCMK  
);  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [DROP COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Always Encrypted &#40;データベース エンジン&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_encryption_keys (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [sys.column_encryption_key_values (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Always Encrypted のキー管理の概要](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
 [セキュリティで保護されたエンクレーブが設定された Always Encrypted のキーを管理する](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)   
  
  
