---
title: SQL Server Management Studio で Always Encrypted を使用した列のクエリを実行する | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c97d3ae0dd6b334e129134ba391124d8de3e8260
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595797"
---
# <a name="query-columns-using-always-encrypted-with-sql-server-management-studio"></a>SQL Server Management Studio で Always Encrypted を使用した列のクエリを実行する
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

この記事では、[SQL Server Management Studio (SSMS)](../../../ssms/download-sql-server-management-studio-ssms.md) を使用して [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) によって暗号化された列にクエリを実行する方法について説明します。 SSMS を使って、次のことができます。
- 暗号化された列に格納された暗号化テキスト値を取得する。 
- 暗号化された列に格納されたプレーンテキスト値を取得する。   
- 暗号化された列をターゲットとするプレーンテキスト値を送信する (たとえば、`INSERT` または `UPDATE` ステートメントや、`WHERE` ステートメントの `SELECT` 句のルックアップ パラメーターとして)。

## <a name="retrieving-ciphertext-values-stored-in-encrypted-columns"></a>暗号化された列に格納された暗号化テキスト値の取得    
暗号化された列に格納されているデータの暗号化テキストを取得する SELECT クエリの実行では (データの暗号化の解除なし)、データを保護する列マスター キーへのアクセス権は必要ありません。 SSMS で暗号化テキストとして暗号化された列から値を取得するには、次のようにします。

1. クエリの実行対象の列を保護するキーに関するメタデータにアクセスできることを確認します。 実際の列マスター キーにアクセスできる必要はありませんが、データベースレベルの権限では、データベース内の列マスター キーと列暗号化キーのメタデータ オブジェクトを表示できる必要があります。 詳しくは、以下の「[暗号化された列にクエリを実行するためのアクセス許可](#permissions-for-querying-encrypted-columns)」を参照してください。
1. 暗号化テキスト値を取得する `SELECT` クエリの実行元のクエリ エディター ウィンドウのデータベース接続に対して Always Encrypted を無効にしていることを確認します。 以下の「[データベース接続での Always Encrypted の有効化と無効化](#en-dis)」を参照してください。     
1. `SELECT` クエリを実行します。 暗号化された列から取得されたデータは、バイナリ (暗号化された) 値として返されます。   

### <a name="example"></a>例
`SSN` が `Patients` テーブルの暗号化された列であると仮定して、以下に示されているクエリでバイナリ暗号化テキスト値を取得します (Always Encrypted がデータベース接続で無効になっている場合)。   

![always-encrypted-ciphertext](../../../relational-databases/security/encryption/media/always-encrypted-ciphertext.png)
 
## <a name="retrieving-plaintext-values-stored-in-encrypted-columns"></a>暗号化された列に格納されたプレーンテキスト値の取得    
(値の暗号化を解除するために) プレーンテキストとして暗号化された列から値を取得する場合は、次のようにします。   
1. 列マスター キーと、クエリの実行対象の列を保護するキーに関するメタデータにアクセスできることを確認します。 詳しくは、以下の「[暗号化された列にクエリを実行するためのアクセス許可](#permissions-for-querying-encrypted-columns)」を参照してください。
1.  データを取得および暗号化解除する `SELECT` クエリの実行元のクエリ エディター ウィンドウのデータベース接続に対して Always Encrypted を有効にしていることを確認します。 これにより、.NET Framework Data Provider for SQL Server (SSMS で使用) は、クエリの結果セット内の暗号化された列の暗号化を解除するよう指示されます。 以下の「[データベース接続での Always Encrypted の有効化と無効化](#en-dis)」を参照してください。
1.  `SELECT` クエリを実行します。 暗号化された列から取得されたデータは、元のデータ型のプレーンテキスト値として返されます。
 
### <a name="example"></a>例
SSN が `char(11)` テーブルで暗号化された `Patients` 列であると仮定して、以下に示されているクエリでプレーンテキスト値を返します (Always Encrypted がデータベース接続で有効になっている場合、および `SSN` 列に構成された列マスター キーにアクセスできる場合)。   

![always-encrypted-plaintext](../../../relational-databases/security/encryption/media/always-encrypted-plaintext.png)
 
## <a name="sending-plaintext-values-targeting-encrypted-columns"></a>暗号化された列をターゲットとするプレーンテキスト値の送信       
暗号化された列をターゲットとする値を送信するクエリ (暗号化された列に格納されている値を使用して挿入、更新またはフィルタリングするクエリなど) を実行する場合は、次のようにします。

1. 列マスター キーと、クエリの実行対象の列を保護するキーに関するメタデータにアクセスできることを確認します。 詳しくは、以下の「[暗号化された列にクエリを実行するためのアクセス許可](#permissions-for-querying-encrypted-columns)」を参照してください。
1.  データを取得および暗号化解除する `SELECT` クエリの実行元のクエリ エディター ウィンドウのデータベース接続に対して Always Encrypted を有効にしていることを確認します。 これにより、.NET Framework Data Provider for SQL Server (SSMS で使用) は、クエリの結果セット内の暗号化された列の暗号化を解除するよう指示されます。 以下の「[データベース接続での Always Encrypted の有効化と無効化](#en-dis)」を参照してください。
1. クエリ エディター ウィンドウで Always Encrypted のパラメーター化が有効になっていることを確認してください。 (SSMS バージョン 17.0 以降が必要です)。Transact-SQL 変数を宣言し、データベースに送信 (挿入、更新またはフィルタリング) する値で初期化します。 詳細については、以下の「 [Always Encrypted のパラメーター化](#param) 」を参照してください。

1. データベースに Transact-SQL 変数の値を送信するクエリを実行します。 SSMS は変数をクエリ パラメーターに変換し、その値を暗号化してからデータベースに送信します。   

### <a name="example"></a>例
`SSN` が `char(11)` テーブルの暗号化された `Patients` 列であると仮定して、以下のスクリプトで SSN 列の `'795-73-9838'` を含む行の検索を試み、 `LastName` 列の値を返します (Always Encrypted がデータベース接続で有効で、Always Encrypted のパラメーター化がクエリ エディター ウィンドウで有効で、 `SSN` 列に構成された列マスター キーにアクセスできる場合)。   

![always-encrypted-patients](../../../relational-databases/security/encryption/media/always-encrypted-patients.png)

## <a name="permissions-for-querying-encrypted-columns"></a>暗号化された列にクエリを実行するためのアクセス許可

暗号化テキストのデータを取得するクエリを含め、暗号化された列でクエリを実行するには、データベースでの `VIEW ANY COLUMN MASTER KEY DEFINITION` と `VIEW ANY COLUMN ENCRYPTION KEY DEFINITION` の権限が必要です。

これらの権限に加え、クエリ結果を暗号化解除する場合や、(Transact-SQL 変数をパラメーター化することで生成される) クエリ パラメーターを暗号化する場合には、ターゲット列を保護する列マスター キーにアクセスする必要もあります。

- **証明書ストア - ローカル コンピューター** 列マスター キーとして使用される証明書への `Read` アクセス権を持っているか、コンピューターの管理者である必要があります。   
- **Azure Key Vault** 列マスター キーが格納されている資格情報コンテナーに対する `get`、 `unwrapKey`、および `verify` の権限が必要です。
- **キー ストア プロバイダー (KSP)** キー ストアまたはキーを使用するときに入力を求められる可能性がある必要な権限と資格情報は、ストアと KSP の構成によって異なります。   
- **暗号化サービス プロバイダー (CSP)** キー ストアまたはキーを使用するときに入力を求められる可能性がある必要な権限と資格情報は、ストアと CSP の構成によって異なります。

詳細については、 [列マスター キーの作成と格納 (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md) を参照してください。

## <a name="en-dis"></a> データベース接続での Always Encrypted の有効化と無効化   
SSMS でデータベースに接続する場合は、データベース接続について Always Encrypted を有効または無効にすることができます。 既定では、Always Encrypted は無効になっています。 

データベース接続で Always Encrypted を有効にすると、以下の操作を透過的に試行するように、SQL Server Management Studio で使用される NET Framework Data Provider for SQL Server に指示されます。   
-   暗号化された列から取得され、クエリ結果に返される値の暗号化を解除する。   
-   暗号化されたデータベース列をターゲットとするパラメーター化された Transact-SQL 変数の値を暗号化する。   

接続に対して Always Encrypted を有効にしなかった場合、SSMS で使用される SQL Server の .NET Framework Data Provider は、クエリ パラメーターの暗号化や結果の暗号化解除を試行しません。

新しい接続を作成するときや **[サーバーに接続]** ダイアログを使用して既存の接続を変更するときに、Always Encrypted を有効または無効にすることができます。 

Always Encrypted を有効 (無効) にするには、次のようにします。
1. **[サーバーに接続]** ダイアログを開きます (詳細については、「[SQL Server インスタンスに接続する](../../../ssms/tutorials/connect-query-sql-server.md#connect-to-a-sql-server-instance)」を参照してください)。
1. **[オプション >>]** をクリックします。
1. SSMS 18 以降を使用している場合:
    1. **[Always Encrypted]** タブを選択します。
    1. Always Encrypted を有効にするには、 **[Always Encrypted を有効にする (列の暗号化)]** を選択します。 Always Encrypted を無効にするには、 **[Always Encrypted を有効にする (列の暗号化)]** が選択されていないことを確認します。
    1. [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] を使用し、SQL Server インスタンスがセキュア エンクレーブで構成されている場合は、エンクレーブ構成証明の url を指定できます。 SQL Server インスタンスでセキュア エンクレーブを使用しない場合は、 **[エンクレーブ構成証明 URL]** テキストボックスを空白のままにしてください。 詳細については、「[セキュア エンクレーブを使用する Always Encrypted](always-encrypted-enclaves.md)」を参照してください。
1. SSMS 17 以前を使用している場合:
    1. **[追加のプロパティ]** タブを選択します。
    1. Always Encrypted を有効にするには、「`Column Encryption Setting = Enabled`」と入力します。 Always Encrypted を無効にするには、`Column Encryption Setting = Disabled` を指定するか、 **[追加のプロパティ]** タブから **[列暗号化設定]** の設定を削除します (既定値は **[無効]** )。   
 1. **[接続]** をクリックします。

> [!TIP]
> 既存のクエリ エディター ウィンドウで Always Encrypted の有効化と無効化を切り替えるには、次のようにします。   
> 1.    クエリ エディター ウィンドウの任意の場所をクリックします。
> 2.    **[接続]**  >  **[接続の変更...]** を選択します。これにより、クエリ エディター ウィンドウの現在の接続の **[サーバーに接続]** ダイアログが開きます。 
> 2.    上記の手順に従って Always Encrypted を有効または無効にし、 **[接続]** をクリックします。  
   
## <a name="param"></a>Always Encrypted のパラメーター化   
 
Always Encrypted のパラメーター化は、Transact-SQL 変数をクエリ パラメーター ([SqlParameter クラス](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)のインスタンス) に自動的に変換する、SQL Server Management Studio の機能です (SSMS バージョン 17.0 以降が必要です)。これにより、基になる .NET Framework Data Provider for SQL Server は暗号化された列をターゲットとするデータを検出し、データベースに送信する前にそのデータを暗号化できます。 
  
パラメーター化しないと、.NET Framework Data Provider は、クエリ エディターで作成される各ステートメントを非パラメーター化クエリとして渡します。 クエリに、暗号化された列をターゲットとする Transact-SQL 変数またはリテラルが含まれている場合、.NET Framework Data Provider for SQL Server では、データベースにクエリを送信する前に、データを検出して暗号化することはできません。 その結果、(プレーンテキストのリテラル Transact-SQL 変数と暗号化された列の間で) 型が一致しないため、クエリは失敗します。 たとえば、 `SSN` 列が暗号化されていると仮定して、パラメーター化せずに以下のクエリを正常に実行することはできません。   

```sql
DECLARE @SSN NCHAR(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN
```

### <a name="enabling-and-disabling-parameterization-for-always-encrypted"></a>Always Encrypted のパラメーター化の有効化/無効化

既定では、Always Encrypted のパラメーター化は無効になっています。

現在のクエリ エディター ウィンドウで Always Encrypted のパラメーター化を有効化/無効化するには、次のようにします。

1. メイン メニューから **[クエリ]** を選択します。
2. **[クエリ オプション...]** を選択します。
3. **[実行]**  >  **[詳細]** の順に移動します。
4. **[Always Encrypted のパラメーター化を有効にする]** を選択または選択解除します。
5. **[OK]** をクリックします。

今後のクエリ エディター ウィンドウで Always Encrypted のパラメーター化を有効化/無効化する場合は、次のようにします。

1. メイン メニューから **[ツール]** を選択します。
2. **[オプション...]** を選択します。
3. **[クエリ実行]**  >  **[SQL Server]**  >  **[詳細]** の順に移動します。
4. **[Always Encrypted のパラメーター化を有効にする]** を選択または選択解除します。
5. **[OK]** をクリックします。

Always Encrypted が有効な状態のデータベース接続を使用するクエリ エディター ウィンドウでクエリを実行する場合に、パラメーター化がクエリ エディター ウィンドウで有効になっていないと、有効にするよう求められます。

> [!NOTE]
> Always Encrypted のパラメーター化が機能するのは、Always Encrypted が有効な状態のデータベース接続を使用するクエリ エディター ウィンドウのみです (「[Always Encrypted のパラメーター化の有効化/無効化](#enabling-and-disabling-parameterization-for-always-encrypted)」を参照)。 クエリ エディター ウィンドウで Always Encrypted が有効な状態ではないデータベース接続を使用すると、Transact-SQL 変数がパラメーター化されません。

### <a name="how-parameterization-for-always-encrypted-works"></a>Always Encrypted のパラメーター化のしくみ

クエリ エディター ウィンドウでデータベース接続の Always Encrypted のパラメーター化と Always Encrypted の動作の両方が有効になっている場合、SQL Server Management Studio は、次の前提条件を満たす Transact-SQL 変数のパラメーター化を試みます。

- 同じステートメントで宣言され、初期化 (インライン初期化) されている。 別個の `SET` ステートメントを使用して宣言された変数はパラメーター化されません。
- 単一のリテラルを使用して初期化されている。 演算子または関数を含む式を使用して初期化された変数はパラメーター化されません。

SQL Server Management Studio がパラメーター化する、変数の例を以下に示します。

```sql
DECLARE @SSN char(11) = '795-73-9838';
   
DECLARE @BirthDate date = '19990104';
DECLARE @Salary money = $30000;
```

SQL Server Management Studio がパラメーター化を試みない変数の例を以下に示します。

```sql
DECLARE @Name nvarchar(50); --Initialization seperate from declaration
SET @Name = 'Abel';

DECLARE @StartDate date = GETDATE(); -- a function used instead of a literal

DECLARE @NewSalary money = @Salary * 1.1; -- an expression used instead of a literal
```
 
試行されたパラメーター化が正常に行われるようにするには   
- パラメーター化する変数の初期化で使用されるリテラルの型は、変数宣言の型と一致する必要があります。   
- 変数の宣言された型が date 型または time 型である場合、以下の ISO 8601 に準拠した形式のいずれかを使用する文字列で変数を初期化する必要があります。   

パラメーター化エラーの原因となる Transact-SQL 変数宣言の例を以下に示します。   
```sql
DECLARE @BirthDate date = '01/04/1999' -- unsupported date format   
   
DECLARE @Number int = 1.1 -- the type of the literal does not match the type of the variable   
```
SQL Server Management Studio では Intellisense を使用して、正常にパラメーター化できた変数と失敗したパラメーター化の試行 (およびその理由) を通知します。   

クエリ エディターでは、正常にパラメーター化できた変数の宣言に警告の下線が付けられます。 警告の下線が付いた宣言ステートメントにカーソルを置くと、パラメーター化プロセスの結果が表示されます。これには、結果の [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) オブジェクト (変数に対応する) の次の主要なプロパティの値が含まれます:[SqlDbType](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqldbtype.aspx)、[Size](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.size.aspx)、[Precision](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.precision.aspx)、[Scale](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.scale.aspx)、[SqlValue](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqlvalue.aspx)。 また、 **[エラー一覧]** ビューの **[警告]** タブには、正常にパラメーター化されたすべての変数の完全な一覧も表示されます。 **[エラー一覧]** ビューを開くには、メイン メニューから **[ビュー]** を選択し、 **[エラー一覧]** を選択します。    

SQL Server Management Studio が変数のパラメーター化を試みたときに、パラメーター化が失敗した場合には、変数の宣言にエラーの下線が付けられます。 エラーの下線が付けられた宣言ステートメントにカーソルを置くと、エラーに関する結果が表示されます。 また、 **[エラー一覧]** ビューの **[エラー]** タブで、すべての変数のパラメーター化エラーの完全な一覧を表示することもできます。 **[エラー一覧]** ビューを開くには、メイン メニューから **[ビュー]** を選択し、 **[エラー一覧]** を選択します。   

下のスクリーン ショットは、6 つの変数宣言の例を示しています。 SQL Server Management Studio は、最初の 3 つの変数を正常にパラメーター化しています。 最後の 3 つの変数ではパラメーター化の前提条件が満たされなかったため、SQL Server Management Studio ではそれらのパラメーター化は試行されていません (宣言にはまったくマークが付けられていません)。

![always-encrypted-parameter-warnings](../../../relational-databases/security/encryption/media/always-encrypted-parameter-warnings.png)
 
次の別の例では、2 つの変数はパラメーター化の前提条件を満たしていますが、変数が正しく初期化されていないため、パラメーター化の試行は失敗しています。    
 
![always-encrypted-error](../../../relational-databases/security/encryption/media/always-encrypted-error.png)
 
> [!NOTE]
> Always Encrypted でサポートされる型変換のサブセットは限られているため、多くの場合、Transact-SQL 変数のデータ型が、ターゲットとなるターゲット データベース列の型と同じである必要があります。 たとえば、 `SSN` テーブル内の `Patients` 列の型が `char(11)`であると仮定して、 `@SSN` である、 `nchar(11)`変数の型が列の型と一致しないため、以下のクエリは失敗します。   

```sql
DECLARE @SSN nchar(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN;
```

    Msg 402, Level 16, State 2, Line 5   
    The data types char(11) encrypted with (encryption_type = 'DETERMINISTIC', 
    encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
    column_encryption_key_database_name = 'Clinic') collation_name = 'Latin1_General_BIN2' 
    and nchar(11) encrypted with (encryption_type = 'DETERMINISTIC', 
    encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
    column_encryption_key_database_name = 'Clinic') are incompatible in the equal to operator. 

> [!NOTE]
> パラメーター化しないと、型変換を含め、クエリ全体が SQL Server/Azure SQL Database 内で処理されます。 パラメーター化が有効になっている場合は、SQL Server Management Studio 内の .NET Framework でいくつかの型変換が実行されます。 .NET Framework 型システムと SQL Server 型システムには違いがある (float など、いくつかの型の精度が異なる) ため、パラメーター化を有効にして実行されたクエリでは、パラメーター化を有効にせずに実行されたクエリとは異なる結果が生成される場合があります。 

## <a name="next-steps"></a>Next Steps
- [Always Encrypted を使用したアプリケーションの開発](always-encrypted-client-development.md)


## <a name="see-also"></a>参照
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
