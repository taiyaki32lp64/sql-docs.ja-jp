---
title: Transact-SQL を使用してインプレースでの列の暗号化を構成する | Microsoft Docs
ms.custom: ''
ms.date: 10/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: b7e8118dc6404bf0f23422e030737403857367d8
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595567"
---
# <a name="configure-column-encryption-in-place-with-transact-sql"></a>Transact-SQL を使用してインプレースでの列の暗号化を構成する
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

この記事では、セキュリティで保護されたエンクレーブが設定された Always Encrypted と [ALTER TABLE](../../../odbc/microsoft/alter-table-statement.md)/`ALTER COLUMN` ステートメントを使用して、列に対する暗号化操作をインプレースで実行する方法について説明します。 インプレース暗号化および一般的な前提条件に関する基本的な情報については、「[セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列の暗号化をインプレースで構成する](always-encrypted-enclaves-configure-encryption.md)」をご覧ください。

`ALTER TABLE` または `ALTER COLUMN` ステートメントを使うと、列のターゲット暗号化構成を設定できます。 ステートメントを実行すると、ステートメントの列定義で指定されている現在およびターゲットの暗号化構成に応じて、サーバー側のセキュリティで保護されたエンクレーブにより、列に格納されているデータの暗号化、再暗号化、暗号化解除が行われます。 
- 列が現在暗号化されていない場合は、列の定義で `ENCRYPTED WITH` 句を指定すると、暗号化が行われます。
- 列が現在暗号化されている場合は、列の定義で `ENCRYPTED WITH` 句を指定しないと、暗号化解除 (プレーンテキスト列への変換) が行われます。
- 列が現在暗号化されている場合、`ENCRYPTED WITH` 句を指定し、指定した列の暗号化の種類または列の暗号化キーが、現在使用されている暗号化の種類または列の暗号化キーと異なる場合は、再暗号化が行われます。 

> [!NOTE]
> 列を `NULL` または `NOT NULL` に変更したり、照合順序を変更したりする場合を除き、暗号化操作と他の変更を 1 つの `ALTER TABLE`/`ALTER COLUMN` ステートメントで組み合わせることはできません。 たとえば、1 つの `ALTER TABLE`/`ALTER COLUMN` Transact-SQL ステートメントで、列の暗号化と、列のデータ型の変更を、同時に行うことはできません。 2 つの異なるステートメントを使用します。

サーバー側のセキュリティで保護されたエンクレーブを使用する他のクエリと同様、インプレース暗号化をトリガーする `ALTER TABLE`/`ALTER COLUMN` ステートメントは、Always Encrypted とエンクレーブ計算が有効になっている接続を通して送信する必要があります。 

この記事の残りの部分では、SQL Server Management Studio から `ALTER TABLE`/`ALTER COLUMN` ステートメントを使用して、インプレース暗号化をトリガーする方法について説明します。 または、アプリケーションから `ALTER TABLE`/`ALTER COLUMN` を発行することもできます。 

> [!NOTE]
> 現時点では、SqlServer PowerShell モジュールの [Invoke-Sqlcmd](https://docs.microsoft.com/powershell/module/sqlserver/invoke-sqlcmd) コマンドレットや [sqlcmd](../../../tools/sqlcmd-utility.md) などの SSMS 以外のツールでは、インプレース暗号化操作に対する `ALTER TABLE`/`ALTER COLUMN` の使用はサポートされていません。

## <a name="perform-in-place-encryption-with-transact-sql-in-ssms"></a>SSMS で Transact-SQL を使用してインプレース暗号化を実行する
### <a name="pre-requisites"></a>前提条件
- 「[セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列の暗号化をインプレースで構成する](always-encrypted-enclaves-configure-encryption.md)」で説明されている前提条件。
- SQL Server Management Studio 18.3 以降。

### <a name="steps"></a>手順
1. データベース接続で Always Encrypted とエンクレーブ計算を有効にしてクエリ ウィンドウを開きます。 詳しくは、「[ データベース接続での Always Encrypted の有効化と無効化](always-encrypted-query-columns-ssms.md#en-dis)」をご覧ください。
2. クエリ ウィンドウで、`ENCRYPTED WITH` 句でエンクレーブ対応の列暗号化キーを指定して、`ALTER TABLE`/`ALTER COLUMN` ステートメントを実行します。 列が文字列型の列 (`char`、`varchar`、`nchar`、`nvarchar` など) の場合は、照合順序を BIN2 の照合順序に変更する必要があります。 
    
    > [!NOTE]
    > 列マスター キーが Azure Key Vault に格納されている場合は、Azure にサインインするように求められることがあります。

3. テーブルにアクセスするすべてのバッチおよびストアド プロシージャのプラン キャッシュをクリアして、パラメーター暗号化情報を更新します。 
 
    ```sql
    ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
    ```
    > [!NOTE]
    > 影響を受けたクエリのプランをキャッシュから削除しないと、暗号化後のクエリの最初の実行が失敗する可能性があります。

    > [!NOTE]
    > `ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE` または `DBCC FREEPROCCACHE` を使用してプランのキャッシュをクリアするときは、クエリのパフォーマンスが一時的に低下する可能性があるため、慎重に行ってください。 キャッシュのクリアによる悪影響を最小限に抑えるため、影響を受けるクエリのプランのみを選択して削除することができます。

4.  [sp_refresh_parameter_encryption](../../system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) を呼び出し、[sys.parameters](../..//system-catalog-views/sys-parameters-transact-sql.md) に保存されていて、列の暗号化によって無効にされた可能性のある各モジュール (ストアド プロシージャ、関数、ビュー、トリガー) のパラメーターのメタデータを更新します。

### <a name="examples"></a>使用例
#### <a name="encrypting-a-column-in-place"></a>インプレースでの列の暗号化
以下の例の前提:
- `CEK1` は、エンクレーブ対応の列暗号化キーです。
- `SSN` 列はプレーンテキストであり、現在は既定のデータベース照合順序 (Latin1 で BIN2 以外の照合順序など) を使用しています (例: `Latin1_General_CI_AI_KS_WS`)。

このステートメントを使うと、ランダム化された暗号化とエンクレーブ対応の列暗号化キーを使用して、`SSN` 列が暗号化されます。 また、既定のデータベースの照合順序は、(同じコード ページ内の) 対応する BIN2 の照合順序で上書きされます。

その操作はオンラインで実行されます (`ONLINE = ON`)。 また、クエリのプランを再作成する `ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE` の呼び出しは、テーブル スキーマの変更によって影響を受けることに注意してください。

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char] COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
WITH
(ONLINE = ON);
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

#### <a name="re-encrypt-a-column-in-place-to-change-encryption-type"></a>インプレースで列を再暗号化して暗号化の種類を変更する
以下の例の前提:
- `SSN` 列は、決定論的暗号化と、エンクレーブ対応の列暗号化キー `CEK1` を使用して暗号化されています。
- 列レベルで設定されている現在の照合順序は `Latin1_General_BIN2` です。

次のステートメントでは、ランダム化された暗号化と同じキー (`CEK1`) を使用して、列が再暗号化されます

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1]
, ENCRYPTION_TYPE = Randomized
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

#### <a name="re-encrypt-a-column-in-place-to-rotate-a-column-encryption-key"></a>インプレースで列を再暗号化して列暗号化キーをローテーションする
以下の例の前提:
- `SSN` 列は、ランダム化された暗号化と、エンクレーブ対応の列暗号化キー `CEK1` を使用して暗号化されています。
- `CEK2` は、エンクレーブ対応の (`CEK1` とは異なる) 列暗号化キーです。
- 列レベルで設定されている現在の照合順序は `Latin1_General_BIN2` です。

次のステートメントでは、`CEK2` を使用して列が再暗号化されます。

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK2]
, ENCRYPTION_TYPE = Randomized
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```
#### <a name="decrypt-a-column-in-place"></a>列をインプレースで復号化する
以下の例の前提:
- `SSN` 列は、エンクレーブ対応の列暗号化キーを使用して暗号化されています。
- 列レベルで設定されている現在の照合順序は `Latin1_General_BIN2` です。

次のステートメントでは、列が暗号化解除されます (照合順序は変更されません。代わりに、同じステートメントで BIN2 以外の照合順序などに照合順序を変更することもできます)。

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
WITH (ONLINE = ON);
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

## <a name="next-steps"></a>Next Steps
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する列のクエリを実行する](always-encrypted-enclaves-query-columns.md)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用する列でインデックスを作成して使用する](always-encrypted-enclaves-create-use-indexes.md)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するアプリケーションを開発する](always-encrypted-enclaves-client-development.md)

## <a name="see-also"></a>参照  
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して列の暗号化をインプレースで構成する](always-encrypted-enclaves-configure-encryption.md)
- [既存の暗号化された列に対してセキュリティで保護されたエンクレーブが設定された Always Encrypted を有効にする](always-encrypted-enclaves-enable-for-encrypted-columns.md)
- [チュートリアル: SSMS を使用したセキュリティで保護されたエンクレーブを持つ Always Encrypted の概要](../tutorial-getting-started-with-always-encrypted-enclaves.md)