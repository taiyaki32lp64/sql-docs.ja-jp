---
title: CERTENCODED (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CERTENCODED
- CERTENCODED_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CERTENCODED
ms.assetid: 677a0719-7b9a-4f0b-bc61-41634563f924
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e81c4101d03fd6f8426b1a15a29b206a0c2be7a5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040103"
---
# <a name="certencoded-transact-sql"></a>CERTENCODED (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

この関数は、証明書の公開部分をバイナリ形式で返します。 この関数は、引数として証明書の ID を受け取り、エンコードされた証明書を返します。 証明書を作成するには、バイナリの結果を **CREATE CERTIFICATE …WITH BINARY** に渡します。
  
## <a name="syntax"></a>構文  
  
```sql
CERTENCODED ( cert_id )  
```  
  
## <a name="arguments"></a>引数  
*cert_id*  
証明書の **certificate_id**。 Sys.certificates; でこの値を見つけます。[CERT_ID &#40;Transact-SQL&#41; ](../../t-sql/functions/cert-id-transact-sql.md) 関数もこの値を返すことができます。 *cert_id* は **int** データ型です。
  
## <a name="return-types"></a>戻り値の型
**varbinary**
  
## <a name="remarks"></a>Remarks  
**CERTENCODED** と **CERTPRIVATEKEY** を一緒に使用すると、バイナリの形式で証明書の異なる部分を返します。
  
## <a name="permissions"></a>アクセス許可  
**CERTENCODED** はパブリックに使用できます。
  
## <a name="examples"></a>使用例  
  
### <a name="simple-example"></a>簡単な例  
この例では、`Shipping04` という名前の証明書を作成した後、その証明書のバイナリ エンコードを **CERTENCODED** 関数を使用して返します。 この例では、証明書の有効期限を 2040 年 10 月 31 日に設定します。
  
```sql
CREATE DATABASE TEST1;
GO
USE TEST1
CREATE CERTIFICATE Shipping04
ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'
WITH SUBJECT = 'Sammamish Shipping Records',
EXPIRY_DATE = '20401031';
GO
SELECT CERTENCODED(CERT_ID('Shipping04'));
  
```  
  
### <a name="b-copying-a-certificate-to-another-database"></a>B. 別のデータベースへの証明書のコピー  
次のより複雑な例では、2 つのデータベース (`SOURCE_DB` と `TARGET_DB`) を作成します。 その後で、`SOURCE_DB` 内に証明書を作成し、証明書を `TARGET_DB` にコピーします。 最後に、`SOURCE_DB` で暗号化されたデータを証明書のコピーを使用して `TARGET_DB` で暗号化解除できることを示します。
  
この例の環境を作成するために、`SOURCE_DB` と `TARGET_DB` のデータベース、およびそれぞれのデータベース内のマスター キーを作成します。 その後、`SOURCE_DB` に証明書を作成します。
  
```sql
USE master;  
GO  
CREATE DATABASE SOURCE_DB;  
GO  
USE SOURCE_DB;  
GO  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0URCE_DB KEY Pa$$W0rd';  
GO  
CREATE DATABASE TARGET_DB;  
GO  
USE TARGET_DB  
GO  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'Pa$$W0rd in TARGET_DB';  
GO  
  
-- Create a certificate in SOURCE_DB  
USE SOURCE_DB;  
GO  
CREATE CERTIFICATE SOURCE_CERT WITH SUBJECT = 'SOURCE_CERTIFICATE';  
GO  
```  
  
次に、証明書のバイナリ記述を抽出します。
  
```sql
DECLARE @CERTENC VARBINARY(MAX);  
DECLARE @CERTPVK VARBINARY(MAX);  
SELECT @CERTENC = CERTENCODED(CERT_ID('SOURCE_CERT'));  
SELECT @CERTPVK = CERTPRIVATEKEY(CERT_ID('SOURCE_CERT'),  
       'CertEncryptionPa$$word');  
SELECT @CERTENC AS BinaryCertificate;  
SELECT @CERTPVK AS EncryptedBinaryCertificate;  
GO  
```  
  
その後で、`TARGET_DB` データベースに証明書の複製を作成します。 この作業のために次のコードを変更して、前の手順で返される 2 つのバイナリ値 (@CERTENC と @CERTPVK ) を挿入します。 これらの値を引用符で囲まないでください。
  
```sql
-- Create the duplicate certificate in the TARGET_DB database  
USE TARGET_DB  
GO  
CREATE CERTIFICATE TARGET_CERT  
FROM BINARY = <insert the binary value of the @CERTENC variable>  
WITH PRIVATE KEY (  
BINARY = <insert the binary value of the @CERTPVK variable>  
, DECRYPTION BY PASSWORD = 'CertEncryptionPa$$word');  
-- Compare the certificates in the two databases  
-- The two certificates should be the same   
-- except for name and (possibly) the certificate_id  
SELECT * FROM SOURCE_DB.sys.certificates  
UNION  
SELECT * FROM TARGET_DB.sys.certificates;  
```  
  
単一のバッチとして実行されるこのコードでは、`TARGET_DB` が、`SOURCE_DB` で暗号化されたデータを暗号化解除できることを示します。
  
```sql
USE SOURCE_DB;  
  
DECLARE @CLEARTEXT nvarchar(100);  
DECLARE @CIPHERTEXT varbinary(8000);  
DECLARE @UNCIPHEREDTEXT_Source nvarchar(100);  
SET @CLEARTEXT = N'Hello World';  
SET @CIPHERTEXT = ENCRYPTBYCERT(CERT_ID('SOURCE_CERT'), @CLEARTEXT);  
SET @UNCIPHEREDTEXT_Source =   
    DECRYPTBYCERT(CERT_ID('SOURCE_CERT'), @CIPHERTEXT)  
-- Encryption and decryption result in SOURCE_DB  
SELECT @CLEARTEXT AS SourceClearText, @CIPHERTEXT AS SourceCipherText,   
       @UNCIPHEREDTEXT_Source AS SourceDecryptedText;  
  
-- SWITCH DATABASE  
USE TARGET_DB;  
  
DECLARE @UNCIPHEREDTEXT_Target nvarchar(100);  
SET @UNCIPHEREDTEXT_Target = DECRYPTBYCERT(CERT_ID('TARGET_CERT'), @CIPHERTEXT);  
-- Encryption and decryption result in TARGET_DB  
SELECT @CLEARTEXT AS ClearTextInTarget, @CIPHERTEXT AS CipherTextInTarget, @UNCIPHEREDTEXT_Target AS DecriptedTextInTarget;   
GO  
```  
  
## <a name="see-also"></a>参照
[セキュリティ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
[sys.certificates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)
  
  
