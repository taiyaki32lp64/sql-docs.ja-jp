---
title: sp_refresh_parameter_encryption (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_refresh_parameter_encryption
- sp_refresh_parameter_encryption_TSQL
- sys.sp_refresh_parameter_encryption
- sys.sp_refresh_parameter_encryption_TSQL
helpviewer_keywords:
- sp_refresh_parameter_encryption
- Always Encrypted, sp_refresh_parameter_encryption
ms.assetid: 00b44baf-fcf0-4095-aabe-49fa87e77316
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a5f699f21b1f28537da2e2f0033fe6b17908186a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002464"
---
# <a name="sprefreshparameterencryption-transact-sql"></a>sp_refresh_parameter_encryption (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

指定された非スキーマ バインド ストアド プロシージャ、ユーザー定義関数、ビュー、DML トリガー、データベース レベルの DDL トリガー、または現在のデータベース内のサーバー レベル DDL トリガーのパラメーターを常に暗号化メタデータを更新します。 

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sys.sp_refresh_parameter_encryption [ @name = ] 'module_name' 
    [ , [ @namespace = ] '<class>' ]
[ ; ]

<class> ::=
{ DATABASE_DDL_TRIGGER | SERVER_DDL_TRIGGER }
```

## <a name="arguments"></a>引数

`[ @name = ] 'module_name'` ストアド プロシージャ、ユーザー定義関数、ビュー、DML トリガー、データベース レベルの DDL トリガー、またはサーバー レベル DDL トリガーの名前です。 *モジュール名*共通言語ランタイム (CLR) ストアド プロシージャまたは CLR 関数にすることはできません。 *モジュール名*スキーマ バインドをすることはできません。 *モジュール名*は`nvarchar`、既定値はありません。 *モジュール名*、マルチパート識別子を指定できますが、現在のデータベース内のオブジェクトに参照できるのみです。

`[ @namespace = ] ' < class > '` 指定したモジュールのクラスです。 ときに*module_name* 、DDL トリガーは、`<class>`が必要です。 `<class>` は `nvarchar(20)` です。 有効な入力は`DATABASE_DDL_TRIGGER`と`SERVER_DDL_TRIGGER`します。    

## <a name="return-code-values"></a>リターン コードの値  

0 (成功) または 0 以外の値の数 (失敗)


## <a name="remarks"></a>コメント

モジュールのパラメーターの暗号化メタデータはことができる場合、期限切れになります。   
* 暗号化プロパティ テーブルの列のモジュールの参照が更新されています。 たとえば、列が削除されましたし、同じ名前が、異なる暗号化の種類や暗号化キー、暗号化アルゴリズムを持つ新しい列が追加されました。  
* モジュールは、古いパラメーター暗号化メタデータを持つ別のモジュールを参照します。  

テーブルの暗号化プロパティが変更されると、`sp_refresh_parameter_encryption`テーブルを直接または間接的に参照するすべてのモジュールを実行する必要があります。 呼び出し元に移動する前にユーザーが内部のモジュールの最初の更新を必要とせず、任意の順序でこれらのモジュールでこのストアド プロシージャを呼び出すことができます。

`sp_refresh_parameter_encryption` 拡張プロパティをアクセス許可には影響しませんまたは`SET`オブジェクトに関連付けられているオプション。 

サーバー レベルの DDL トリガーを更新するには、任意のデータベースのコンテキストからこのストアド プロシージャを実行します。

> [!NOTE]
>  実行すると、オブジェクトに関連付けられている署名は削除`sp_refresh_parameter_encryption`します。

## <a name="permissions"></a>アクセス許可

必要があります`ALTER`モジュールに対する権限と`REFERENCES`任意の CLR ユーザー定義型と、オブジェクトによって参照されている XML スキーマ コレクションに対する権限。   

指定されたモジュールは、データベース レベルの DDL トリガーが、必要があります`ALTER ANY DATABASE DDL TRIGGER`現在のデータベースでのアクセスを許可します。    

指定されたモジュールは、サーバー レベルの DDL トリガーが、必要があります`CONTROL SERVER`権限。

モジュールで定義されている、`EXECUTE AS`句、`IMPERSONATE`指定したプリンシパルに権限が必要です。 一般に、オブジェクトの更新は変わりませんその`EXECUTE AS`モジュールが定義していない限り、プリンシパル`EXECUTE AS USER`とモジュールが、時に、別のユーザーに解決が作成されたので、プリンシパルのユーザー名。
 
## <a name="examples"></a>使用例

次の例では、テーブルとテーブルを参照するプロシージャを作成、Always Encrypted を構成および後、テーブルを変更および実行を示しています、`sp_refresh_parameter_encryption`プロシージャ。  

まず、最初のテーブルとテーブルを参照するストアド プロシージャを作成します。
```sql
CREATE TABLE [Patients]([PatientID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11), 
    [FirstName] [nvarchar](50) NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [MiddleName] [nvarchar](50) NULL,
    [StreetAddress] [nvarchar](50) NOT NULL,
    [City] [nvarchar](50) NOT NULL,
    [ZipCode] [char](5) NOT NULL,
    [State] [char](2) NOT NULL,
    [BirthDate] [date] NOT NULL,
 CONSTRAINT [PK_Patients] PRIMARY KEY CLUSTERED 
(
    [PatientID] ASC
) WITH 
    (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, 
     IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, 
     ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY];
GO

CREATE PROCEDURE [find_patient] @SSN [char](11)
AS
BEGIN
    SELECT * FROM [Patients] WHERE SSN=@SSN
END;
GO
```

Always Encrypted キーを設定します。
```sql
CREATE COLUMN MASTER KEY [CMK1]
WITH
(
       KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',
    KEY_PATH = N'CurrentUser/my/A66BB0F6DD70BDFF02B62D0F87E340288E6F9305'
);
GO

CREATE COLUMN ENCRYPTION KEY [CEK1]
WITH VALUES
(
       COLUMN_MASTER_KEY = [CMK1],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 
       0x016E000001630075007200720065006E00740075007300650072002F006D0079002F006100360036006200620030006600360064006400370030006200640066006600300032006200360032006400300066003800370065003300340030003200380038006500360066003900330030003500CA0D0CEC74ECADD1804CF99137B4BD06BBAB15D7EA74E0C249A779C7768A5B659E0125D24FF827F5EA8CA517A8E197ECA1353BA814C2B0B2E6C8AB36E3AE6A1E972D69C3C573A963ADAB6686CF5D24F95FE43140C4F9AF48FBA7DF2D053F3B4A1F5693A1F905440F8015BDB43AF8A04BE4E045B89876A0097E5FBC4E6A3B9C3C0D278C540E46C53938B8C957B689C4DC095821C465C73117CBA95B758232F9E5B2FCC7950B8CA00AFE374DE42847E3FBC2FDD277035A2DEF529F4B735C20D980073B4965B4542A34723276A1646998FC6E1C40A3FDB6ABCA98EE2B447F114D2AC7FF8C7D51657550EC5C2BABFFE8429B851272086DCED94332CF18FA854C1D545A28B1EF4BE64F8E035175C1650F6FC5C4702ACF99850A4542B3747EAEC0CC726E091B36CE24392D801ECAA684DE344FECE05812D12CD72254A014D42D0EABDA41C89FC4F545E88B4B8781E5FAF40D7199D4842D2BFE904D209728ED4F527CBC169E2904F6E711FF81A8F4C25382A2E778DD2A58552ED031AFFDA9D9D891D98AD82155F93C58202FC24A77F415D4F8EF22419D62E188AC609330CCBD97CEE1AEF8A18B01958833604707FDF03B2B386487CC679D7E352D0B69F9FB002E51BCD814D077E82A09C14E9892C1F8E0C559CFD5FA841CEF647DAB03C8191DC46B772E94D579D8C80FE93C3827C9F0AE04D5325BC73111E07EEEDBE67F1E2A73580085
);
GO
```


最後に置換する SSN 列実行と、暗号化された列、 `sp_refresh_parameter_encryption` Always Encrypted のコンポーネントを更新するプロシージャ。
```sql
ALTER TABLE [Patients] DROP COLUMN [SSN];
GO

ALTER TABLE [Patients] 
    ADD [SSN] [char](11) COLLATE Latin1_General_BIN2 
    ENCRYPTED WITH 
        (COLUMN_ENCRYPTION_KEY = [CEK1], 
        ENCRYPTION_TYPE = Deterministic, 
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') 
    NOT NULL;
GO

EXEC sp_refresh_parameter_encryption [find_patient];
GO
```

## <a name="see-also"></a>関連項目 

[Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
[Always Encrypted ウィザード](../../relational-databases/security/encryption/always-encrypted-wizard.md)   

