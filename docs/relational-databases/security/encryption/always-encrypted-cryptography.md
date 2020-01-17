---
title: Always Encrypted による暗号 | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, cryptography system
ms.assetid: ae8226ff-0853-4716-be7b-673ce77dd370
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b0fe0e861e8139416250ffc2677230dbc2aeab6d
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594402"
---
# <a name="always-encrypted-cryptography"></a>Always Encrypted による暗号
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  このドキュメントでは、 [および](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) において、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Always Encrypted [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)]機能で使用される暗号化マテリアルを派生させる暗号化アルゴリズムとメカニズムについて説明します。  
  
## <a name="keys-key-stores-and-key-encryption-algorithms"></a>キー、キー ストア、およびキー暗号化アルゴリズム
 Always Encrypted では 2 種類のキーを使用します。列マスター キーと列暗号化キーです。  
  
 列マスター キー (CMK) は、常にクライアントによって制御され、外部キー ストアに格納されているキー暗号化キー (たとえば、他のキーの暗号化に使用されるキー) です。 Always Encrypted が有効なクライアント ドライバーは CMK ストア プロバイダーを介してキー ストアと対話します。このプロバイダーはドライバー ライブラリの一部 ( [!INCLUDE[msCoName](../../../includes/msconame-md.md)]/system プロバイダー) またはクライアント アプリケーションの一部 (カスタム プロバイダー) である場合があります。 現在、クライアント ドライバー ライブラリには、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 証明書ストア [およびハードウェア セキュリティ モジュール (HSM) の](/windows/desktop/SecCrypto/using-certificate-stores) キー ストア プロバイダーが含まれています。 現在のプロバイダーの一覧については、「[CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-column-master-key-transact-sql.md)」を参照してください。 アプリケーション開発者は、任意のストアのカスタム プロバイダーを提供できます。  
  
 列暗号化キー (CEK) は、CMK によって保護されているコンテンツ暗号化キー (たとえば、データを保護するために使用されるキー) です。  
  
 すべての [!INCLUDE[msCoName](../../../includes/msconame-md.md)] CMK ストア プロバイダーでは、RSA-OAEP (RSA with Optimal Asymmetric Encryption Padding) を使用して CEK が暗号化されます。 Microsoft Cryptography API がサポートされているキー ストア プロバイダー:.NET Framework の Next Generation (CNG) ([SqlColumnEncryptionCngProvider クラス](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcolumnencryptioncngprovider.aspx)) では、RFC 8017 のセクション A.2.1 で指定されている既定のパラメーターが使用されます。 これらの既定のパラメーターでは、SHA-1 のハッシュ関数と、SHA-1 を指定した MGF1 のマスク生成関数を使用します。 他のすべてのキー ストア プロバイダーでは、SHA-256 が使用されます。 
  
## <a name="data-encryption-algorithm"></a>データ暗号化のアルゴリズム  
 Always Encrypted では **AEAD_AES_256_CBC_HMAC_SHA_256** アルゴリズムを使用して、データベース内のデータを暗号化します。  
  
 **AEAD_AES_256_CBC_HMAC_SHA_256** は、[https://tools.ietf.org/html/draft-mcgrew-aead-aes-cbc-hmac-sha2-05](https://tools.ietf.org/html/draft-mcgrew-aead-aes-cbc-hmac-sha2-05) の仕様ドラフトから派生しました。 このアルゴリズムでは、Encrypt-then-MAC 手法に従って、関連データで認証済み暗号化スキームを使用します。 つまり、プレーンテキストが最初に暗号化され、その結果として生成される暗号化テキストに基づいて MAC が生成されます。  
  
 パターンを非表示にするために、 **AEAD_AES_256_CBC_HMAC_SHA_256** では暗号化ブロック チェーン (CBC) という操作モードを使用します。この場合、初期値は初期化ベクター (IV) という名前のシステムに渡されます。 CBC モードの詳細な説明は、[https://csrc.nist.gov/publications/nistpubs/800-38a/sp800-38a.pdf](https://csrc.nist.gov/publications/nistpubs/800-38a/sp800-38a.pdf) にあります。  
  
 **AEAD_AES_256_CBC_HMAC_SHA_256** は、以下の手順を使用して指定されたプレーンテキストの暗号化テキストの値を計算します。  
  
### <a name="step-1-generating-the-initialization-vector-iv"></a>手順 1:初期化ベクター (IV) の生成  
 Always Encrypted では、以下の 2 種類の **AEAD_AES_256_CBC_HMAC_SHA_256**がサポートされています。  
  
-   ランダム化  
  
-   決定的  
  
 ランダムな暗号化の場合、IV はランダムに生成されます。 その結果、同じプレーンテキストが暗号化されるたびに、別の暗号化テキストが生成され、情報の漏えいを防ぐことができます。  
  
```  
When using randomized encryption: IV = Generate cryptographicaly random 128bits  
```  
  
 決定論的暗号化がある場合、IV はランダムに生成されず、代わりに、以下のアルゴリズムを使用してプレーンテキスト値から派生されます。  
  
```  
When using deterministic encryption: IV = HMAC-SHA-256( iv_key, cell_data ) truncated to 128 bits.  
```  
  
 iv_key は以下の方法で CEK から派生します。  
  
```  
iv_key = HMAC-SHA-256(CEK, "Microsoft SQL Server cell IV key" + algorithm + CEK_length)  
```  
  
 IV で必要な場合、1 つのデータ ブロックに収まるように HMAC 値の切り捨てが行われます。
その結果、決定的な暗号化では常に指定されたプレーンテキスト値に対して同じ暗号化テキストが生成されます。これにより、2 つのプレーンテキスト値のそれぞれ対応する暗号化テキスト値を比較して、プレーンテキスト値が同じであるかどうかを推定できます。 この制限された情報の公開により、データベース システムは暗号化された列値の等価比較をサポートできます。  
  
 決定的な暗号化は、定義済みの IV 値を使用するなどして、パターンを非表示にする場合や代替との比較を行う場合により効果的です。  
  
### <a name="step-2-computing-aes_256_cbc-ciphertext"></a>手順 2:AES_256_CBC 暗号化テキストの計算  
 IV を計算した後、 **AES_256_CBC** 暗号化テキストが次のように生成されます。  
  
```  
aes_256_cbc_ciphertext = AES-CBC-256(enc_key, IV, cell_data) with PKCS7 padding.  
```  
  
 この暗号化キー (enc_key) は次のように CEK から派生します。  
  
```  
enc_key = HMAC-SHA-256(CEK, "Microsoft SQL Server cell encryption key" + algorithm + CEK_length )  
```  
  
### <a name="step-3-computing-mac"></a>手順 3:MAC の計算  
 その後、MAC は以下のアルゴリズムを使用して計算されます。  
  
```  
MAC = HMAC-SHA-256(mac_key, versionbyte + IV + Ciphertext + versionbyte_length)  
```  
  
 各要素の説明は次のとおりです。  
  
```  
versionbyte = 0x01 and versionbyte_length = 1
mac_key = HMAC-SHA-256(CEK, "Microsoft SQL Server cell MAC key" + algorithm + CEK_length)  
```  
  
### <a name="step-4-concatenation"></a>手順 4:Concatenation  
 最後に、暗号化された値は、アルゴリズム バージョン バイト、MAC、IV および AES_256_CBC 暗号化テキストを連結して生成されます。  
  
```  
aead_aes_256_cbc_hmac_sha_256 = versionbyte + MAC + IV + aes_256_cbc_ciphertext  
```  
  
## <a name="ciphertext-length"></a>暗号化テキストの長さ  
 **AEAD_AES_256_CBC_HMAC_SHA_256** 暗号化テキストの各コンポーネントの長さ (バイト単位) は次のとおりです。  
  
-   versionbyte: 1  
  
-   MAC: 32  
  
-   IV: 16  
  
-   aes_256_cbc_ciphertext: `(FLOOR (DATALENGTH(cell_data)/ block_size) + 1)* block_size`。  
  
    -   block_size は 16 バイトです。  
  
    -   cell_data はプレーンテキスト値です。  
  
     したがって、aes_256_cbc_ciphertext の最小サイズは 1 ブロックは (16 バイト) になります。  
  
 指定されたプレーンテキスト値を暗号化した場合の暗号化テキストの長さは、以下の式を使用して計算できます。  
  
```  
1 + 32 + 16 + (FLOOR(DATALENGTH(cell_data)/16) + 1) * 16  
```  
  
 例:  
  
-   4 バイト長の **int** プレーンテキスト値は、暗号化後に 65 バイト長のバイナリ値になります。  
  
-   2,000 バイト長の **nchar(1000)** プレーンテキスト値は、暗号化後に 2,065 バイト長のバイナリ値になります。  
  
 次の表には、データ型と各型の暗号化テキストの長さの完全な一覧が含まれています。  
  
|データ型|暗号化テキストの長さ (バイト)|  
|---------------|---------------------------------|  
|**bigint**|65|  
|**[バイナリ]**|多様。 上の式を使用します。|  
|**bit**|65|  
|**char**|多様。 上の式を使用します。|  
|**date**|65|  
|**datetime**|65|  
|**datetime2**|65|  
|**datetimeoffset**|65|  
|**decimal**|81|  
|**float**|65|  
|**geography**|該当なし (サポートされていません)|  
|**geometry**|該当なし (サポートされていません)|  
|**hierarchyid**|該当なし (サポートされていません)|  
|**image**|該当なし (サポートされていません)|  
|**int**|65|  
|**money**|65|  
|**nchar**|多様。 上の式を使用します。|  
|**ntext**|該当なし (サポートされていません)|  
|**numeric**|81|  
|**nvarchar**|多様。 上の式を使用します。|  
|**real**|65|  
|**smalldatetime**|65|  
|**smallint**|65|  
|**smallmoney**|65|  
|**sql_variant**|該当なし (サポートされていません)|  
|**sysname**|該当なし (サポートされていません)|  
|**text**|該当なし (サポートされていません)|  
|**time**|65|  
|**timestamp**<br /><br /> (**rowversion**)|該当なし (サポートされていません)|  
|**tinyint**|65|  
|**uniqueidentifier**|81|  
|**varbinary**|多様。 上の式を使用します。|  
|**varchar**|多様。 上の式を使用します。|  
|**xml**|該当なし (サポートされていません)|  
  
## <a name="net-reference"></a>.NET リファレンス  
 このドキュメントに記載されているアルゴリズムの詳細については、[.NET リファレンス](https://referencesource.microsoft.com/)の **SqlAeadAes256CbcHmac256Algorithm.cs**、**SqlColumnEncryptionCertificateStoreProvider.cs**、**SqlColumnEncryptionCertificateStoreProvider.cs** ファイルを参照してください。  
  
## <a name="see-also"></a>参照  
 - [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 - [Always Encrypted を使用したアプリケーションの開発](../../../relational-databases/security/encryption/always-encrypted-client-development.md)  
  
  
