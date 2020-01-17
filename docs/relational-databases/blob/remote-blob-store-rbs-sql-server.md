---
title: リモート BLOB ストア (RBS) [SQL Server] | Microsoft Docs
ms.custom: ''
ms.date: 11/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- Remote Blob Store (RBS) [SQL Server]
- RBS (Remote Blob Store) [SQL Server]
ms.assetid: 31c947cf-53e9-4ff4-939b-4c1d034ea5b1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fc6bb3164b54f0799073e8b959f68b0dd625c47e
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258181"
---
# <a name="remote-blob-store-rbs-sql-server"></a>リモート BLOB ストア (RBS) [SQL Server]
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のリモート BLOB ストア (RBS) はオプションのアドオン コンポーネントです。これを使用すると、データベース管理者は、バイナリ ラージ オブジェクトを、主なデータベース サーバーに直接格納するのではなく、汎用的なストレージ ソリューションに格納できます。  
  
 RBS は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール メディアに含まれていますが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ プログラムではインストールされません。 インストール メディアで RBS.msi を検索し、セットアップ ファイルを見つけます。

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール メディアがない場合は、次のいずれかの場所で RBS をダウンロードできます。

| [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョン | RBS のダウンロード場所 |
|:---|:---|
| [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] | [[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 Feature Pack](https://www.microsoft.com/download/details.aspx?id=56833) |
| [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] | [[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Feature Pack](https://www.microsoft.com/download/details.aspx?id=55992) |
| [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] | [[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] RBS ダウンロード ページ](https://go.microsoft.com/fwlink/?linkid=2109005) |
| &nbsp; | &nbsp; |
  
 
  
## <a name="why-rbs"></a>RBS の利点  
  
### <a name="optimized-database-storage-and-performance"></a>最適化されたデータベース ストレージとパフォーマンス  
 BLOB をデータベースに格納する場合は、大量のファイル領域と高コストのサーバー リソースが消費されることがあります。 RBS は、BLOB を選択した専用ストレージ ソリューションに転送し、データベースにその BLOB への参照を格納します。 これにより、構造化データ用のサーバー ストレージが解放され、データベース操作用のサーバー リソースが解放されます。  
  
### <a name="efficient-blob-management"></a>BLOB の効率的な管理  
 複数の RBS 機能が、格納された BLOB の管理をサポートします。  
  
-   BLOB は、ACID (原子性、一貫性、分離性、持続性) を備えたトランザクションで管理します。  
  
-   BLOB は、いくつかのコレクションで構成されています。  
  
-   ガベージ コレクション、一貫性チェック、およびその他のメンテナンス機能が含まれています。  
  
### <a name="standardized-api"></a>標準化された API  
 RBS では、アプリケーションから BLOB ストアにアクセスして変更するための標準化されたプログラミング モデルを提供する一連の API が定義されています。 各 BLOB ストアでは、独自のプロバイダー ライブラリを指定できます。このライブラリは、RBS クライアント ライブラリに接続して、BLOB の格納方法やアクセス方法を指定します。  
  
 多数のサード パーティのストレージ ソリューション ベンダーが、これらの標準 API に準拠し、さまざまなストレージ プラットフォームで BLOB ストレージをサポートする RBS プロバイダーを開発しています。  
  
## <a name="rbs-requirements"></a>RBS 要件  
 - RBS では、BLOB メタデータが格納されている主なデータベース サーバー用の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise が必要です。  ただし、指定された FILESTREAM プロバイダーを使用する場合は、BLOB 自体を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard に格納できます。 RBS が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続するには、 [!INCLUDE[ssSQL14_md](../../includes/sssql14-md.md)] の場合は ODBC ドライバー バージョン 11 以上、 [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]の場合は ODBC ドライバー バージョン 13 以上が必要です。 ドライバーは、「 [Download ODBC Driver for SQL Server](https://msdn.microsoft.com/library/mt703139.aspx)」(SQL Server 用の ODBC ドライバーをダウンロードする) で入手できます。    
  
 RBS には、RBS を使用して BLOB を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスで格納できる FILESTREAM プロバイダーが含まれています。 RBS を使用して BLOB を別のストレージ ソリューションに格納する場合は、そのストレージ ソリューション用に開発されたサード パーティの RBS プロバイダーを使用するか、RBS API を使用してカスタム RBS プロバイダーを開発する必要があります。 [Codeplex](https://go.microsoft.com/fwlink/?LinkId=210190)には、NTFS ファイル システムに BLOB を格納するサンプル プロバイダーが学習用リソースとして用意されています。  
  
## <a name="rbs-security"></a>RBS セキュリティ  
 SQL リモート BLOB ストレージ チームのブログはこの機能に関する適切な情報源です。 「 [RBS Security Model (RBS セキュリティ モデル)](https://blogs.msdn.com/b/sqlrbs/archive/2010/08/05/rbs-security-model.aspx)」で、RBS セキュリティ モデルに関する投稿を参照してください。  
  
### <a name="custom-providers"></a>カスタム プロバイダー  
 カスタム プロバイダーを使用して BLOB を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の外部に格納する場合は、カスタム プロバイダーが使用するストレージ メディアに適した権限と暗号化オプションで格納された BLOB が保護されていることを確認してください。  
  
### <a name="credential-store-symmetric-key"></a>資格情報ストアの対称キー  
 プロバイダーが資格情報ストア内に格納されているシークレットをセットアップして使用する必要がある場合、RBS では対称キーを使用して、プロバイダーのシークレットを暗号化します。このシークレットは、クライアントがプロバイダーの BLOB ストアに対する許可を得るために使用する場合があります。  
  
-   RBS 2016 では **AES_128** 対称キーを使用します。 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] では、後方互換性を確保する場合を除き、新しい **TRIPLE_DES** キーを作成することはできません。 詳細については、「[CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)」を参照してください。  
  
-   RBS 2014 以前のバージョンでは、古い **TRIPLE_DES** 対称キー アルゴリズムを使用して暗号化されたシークレットを保持する資格情報ストアを使用します。 現在、**TRIPLE_DES** を使用している場合、[!INCLUDE[msCoName](../../includes/msconame-md.md)] では、より強力な暗号化方式を適用するためにこのトピックの手順に従ってキーをローテーションし、セキュリティを強化することをお勧めします。  
  
 RBS 資格情報ストアの対称キー プロパティは、RBS データベースで次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行して判別できます。   
`SELECT * FROM sys.symmetric_keys WHERE name = 'mssqlrbs_encryption_skey';` このステートメントからの出力で、 **TRIPLE_DES** がまだ使用されていることが分かった場合は、このキーのローテーションが必要です。  
  
### <a name="rotating-the-symmetric-key"></a>対称キーのローテーション  
 RBS を使用する場合、資格情報ストアの対称キーを定期的にローテーションする必要があります。 これは、組織のセキュリティ ポリシーを満たすための一般的なセキュリティに関するベスト プラクティスです。  RBS 資格情報ストアの対称キーをローテーションする 1 つの方法は、RBS データベースで [後述のスクリプト](#Key_rotation) を使用することです。  このスクリプトを使用して、アルゴリズムやキーの長さなど、より強力な暗号化強度プロパティに移行することもできます。 キー ローテーションを行う前に、データベースをバックアップしておいてください。  スクリプトの最後に、確認手順がいくつかあります。  
セキュリティ ポリシーで指定されたものとは異なるキー プロパティ (アルゴリズムやキーの長さなど) が求められている場合、スクリプトをテンプレートとして使用できます。 次の 2 つの場所でキー プロパティを変更します。1) 一時キーの作成 2) 永続キーの作成。  
  
##  <a name="rbsresources"></a> RBS リソース  
  
 **RBS サンプル**  
 [Codeplex](https://go.microsoft.com/fwlink/?LinkId=210190) で入手できる RBS サンプルでは、RBS アプリケーションの開発方法とカスタム RBS プロバイダーの開発およびインストール方法を示します。  
  
 **RBS ブログ**  
 [RBS ブログ](https://go.microsoft.com/fwlink/?LinkId=210315) には、RBS の理解、配置、および維持に役立つ追加情報が含まれています。  
  
##  <a name="Key_rotation"></a> キー ローテーションのスクリプト  
 この例では、 `sp_rotate_rbs_symmetric_credential_key` というストアド プロシージャを作成し、現在使用している RBS 資格情報ストアの対称キーを、  
任意の対称キーに置き換えます。  セキュリティ ポリシーで定期的なキー ローテーションが求められている場合、または特定のアルゴリズム要件がある場合は、   
この操作が必要になることがあります。  
 このストアド プロシージャでは、 **AES_256** を使用する対称キーで現在の対称キーが置き換えられます。  対称キーが置き換えられたら、  
シークレットを新しいキーで再暗号化する必要があります。  このストアド プロシージャでは   
シークレットの再暗号化も行います。  キー ローテーションの前にデータベースをバックアップする必要があります。  
  
```  
CREATE PROC sp_rotate_rbs_symmetric_credential_key  
AS  
BEGIN  
BEGIN TRANSACTION;  
BEGIN TRY  
CLOSE ALL SYMMETRIC KEYS;  
  
/* Prove that all secrets can be re-encrypted, by creating a   
temporary key (#mssqlrbs_encryption_skey) and create a   
temp table (#myTable) to hold the re-encrypted secrets.    
Check to see if all re-encryption worked before moving on.*/  
  
CREATE TABLE #myTable(sql_user_sid VARBINARY(85) NOT NULL,  
    blob_store_id SMALLINT NOT NULL,  
    credential_name NVARCHAR(256) COLLATE Latin1_General_BIN2 NOT NULL,  
    old_secret VARBINARY(MAX), -- holds secrets while existing symmetric key is deleted  
    credential_secret VARBINARY(MAX)); -- holds secrets with the new permanent symmetric key  
  
/* Create a new temporary symmetric key with which the credential store secrets   
can be re-encrypted. These will be used once the existing symmetric key is deleted.*/  
CREATE SYMMETRIC KEY #mssqlrbs_encryption_skey    
    WITH ALGORITHM = AES_256 ENCRYPTION BY   
    CERTIFICATE [cert_mssqlrbs_encryption];  
  
OPEN SYMMETRIC KEY #mssqlrbs_encryption_skey    
    DECRYPTION BY CERTIFICATE [cert_mssqlrbs_encryption];  
  
INSERT INTO #myTable   
    SELECT cred_store.sql_user_sid, cred_store.blob_store_id, cred_store.credential_name,   
    encryptbykey(  
        key_guid('#mssqlrbs_encryption_skey'),   
        decryptbykeyautocert(cert_id('cert_mssqlrbs_encryption'),   
            NULL, cred_store.credential_secret)  
        ),   
    NULL  
    FROM [mssqlrbs_resources].[rbs_internal_blob_store_credentials] AS cred_store;  
  
IF( EXISTS(SELECT * FROM #myTable WHERE old_secret IS NULL))  
BEGIN  
    PRINT 'Abort. Failed to read some values';  
    SELECT * FROM #myTable;  
    ROLLBACK;  
END;  
ELSE  
BEGIN  
/* Re-encryption worked, so go ahead and drop the existing RBS credential store   
 symmetric key and replace it with a new symmetric key.*/  
DROP SYMMETRIC KEY [mssqlrbs_encryption_skey];  
  
CREATE SYMMETRIC KEY [mssqlrbs_encryption_skey]   
WITH ALGORITHM = AES_256   
ENCRYPTION BY CERTIFICATE [cert_mssqlrbs_encryption];  
  
OPEN SYMMETRIC KEY [mssqlrbs_encryption_skey]   
DECRYPTION BY CERTIFICATE [cert_mssqlrbs_encryption];  
  
/*Re-encrypt using the new permanent symmetric key.    
Verify if encryption provided a result*/  
UPDATE #myTable   
SET [credential_secret] =   
    encryptbykey(key_guid('mssqlrbs_encryption_skey'), decryptbykey(old_secret))  
  
IF( EXISTS(SELECT * FROM #myTable WHERE credential_secret IS NULL))  
BEGIN  
    PRINT 'Aborted. Failed to re-encrypt some values'  
    SELECT * FROM #myTable  
    ROLLBACK  
END  
ELSE  
BEGIN  
  
/* Replace the actual RBS credential store secrets with the newly   
encrypted secrets stored in the temp table #myTable.*/                
SET NOCOUNT ON;  
DECLARE @sql_user_sid varbinary(85);  
DECLARE @blob_store_id smallint;  
DECLARE @credential_name varchar(256);  
DECLARE @credential_secret varbinary(256);  
DECLARE curSecretValue CURSOR   
    FOR SELECT sql_user_sid, blob_store_id, credential_name, credential_secret   
FROM #myTable ORDER BY sql_user_sid, blob_store_id, credential_name;  
  
OPEN curSecretValue;  
FETCH NEXT FROM curSecretValue   
    INTO @sql_user_sid, @blob_store_id, @credential_name, @credential_secret  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    UPDATE [mssqlrbs_resources].[rbs_internal_blob_store_credentials]   
        SET [credential_secret] = @credential_secret   
        FROM [mssqlrbs_resources].[rbs_internal_blob_store_credentials]   
        WHERE sql_user_sid = @sql_user_sid AND blob_store_id = @blob_store_id AND   
            credential_name = @credential_name  
FETCH NEXT FROM curSecretValue   
    INTO @sql_user_sid, @blob_store_id, @credential_name, @credential_secret  
END  
CLOSE curSecretValue  
DEALLOCATE curSecretValue  
  
DROP TABLE #myTable;  
CLOSE ALL SYMMETRIC KEYS;  
DROP SYMMETRIC KEY #mssqlrbs_encryption_skey;  
  
/* Verify that you can decrypt all encrypted credential store entries using the certificate.*/  
IF( EXISTS(SELECT * FROM [mssqlrbs_resources].[rbs_internal_blob_store_credentials]   
WHERE decryptbykeyautocert(cert_id('cert_mssqlrbs_encryption'),   
    NULL, credential_secret) IS NULL))  
BEGIN  
    print 'Aborted. Failed to verify key rotation'  
    ROLLBACK;  
END;  
ELSE  
    COMMIT;  
END;  
END;  
END TRY  
BEGIN CATCH  
     PRINT 'Exception caught: ' + cast(ERROR_NUMBER() as nvarchar) + ' ' + ERROR_MESSAGE();  
     ROLLBACK  
END CATCH  
END;  
GO  
```  
  
 これで、 `sp_rotate_rbs_symmetric_credential_key` ストアド プロシージャを使用して、RBS 資格情報ストアの対称キーをローテーションすることができます。キー ローテーション後もシークレットはそのままです。  
  
```  
SELECT *, decryptbykeyautocert(cert_id('cert_mssqlrbs_encryption'), NULL, credential_secret)   
FROM [mssqlrbs_resources].[rbs_internal_blob_store_credentials];  
  
EXEC sp_rotate_rbs_symmetric_credential_key;  
  
SELECT *, decryptbykeyautocert(cert_id('cert_mssqlrbs_encryption'), NULL, credential_secret)   
FROM [mssqlrbs_resources].[rbs_internal_blob_store_credentials];  
  
/* See that the RBS credential store symmetric key properties reflect the new changes*/  
SELECT * FROM sys.symmetric_keys WHERE name = 'mssqlrbs_encryption_skey';  
```  
  
## <a name="see-also"></a>参照  
[リモート BLOB ストアと AlwaysOn 可用性グループ (SQL Server)](../../database-engine/availability-groups/windows/remote-blob-store-rbs-and-always-on-availability-groups-sql-server.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
  
