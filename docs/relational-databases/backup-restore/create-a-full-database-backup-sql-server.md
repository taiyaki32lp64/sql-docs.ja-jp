---
title: データベースの完全バックアップを作成する | Microsoft Docs
ms.custom: sqlfreshmay19
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: carlrab
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [SQL Server], full backups
- backing up databases [SQL Server], SQL Server Management Studio
- backups [SQL Server], creating
- database backups [SQL Server], SQL Server Management Studio
ms.assetid: 586561fc-dfbb-4842-84f8-204a9100a534
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fe0c9a950221317cb4a9088bae7629fc0c894165
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710320"
---
# <a name="create-a-full-database-backup"></a>データベースの完全バックアップの作成

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、または PowerShell を使用して、データベースの完全バックアップを作成する方法について説明します。

Azure Blob Storage サービスへの SQL Server のバックアップについては、「[Windows Azure BLOB ストレージ サービスを使用した SQL Server のバックアップと復元](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)」および「[SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)」を参照してください。

## <a name="Restrictions"></a> 制限事項と制約事項

- `BACKUP` ステートメントは、明示的または暗黙的なトランザクションでは使用できません。
- 新しいバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって作成されたバックアップは、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では復元できません。

バックアップの概念とタスクに関する概要および詳細については、先へ進む前に「[Backup Overview &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)」を参照してください。

## <a name="Recommendations"></a> 推奨事項

- データベース サイズが大きくなると、データベースの完全バックアップにかかる時間は長くなり、必要な記憶領域も増加します。 大規模なデータベースでは、一連の[データベースの差分バックアップ](../../relational-databases/backup-restore/differential-backups-sql-server.md)を使用してデータベースの完全バックアップを補完することを検討してください。
- データベースの完全バックアップのサイズは、 [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) システム ストアド プロシージャを使用して推計します。
- 既定では、バックアップ操作が成功するたびに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログおよびシステム イベント ログにエントリが 1 つ追加されます。 頻繁にバックアップすると、これらの成功メッセージがすぐに蓄積され、エラー ログが大きくなります。 そのために、他のメッセージを探すのが困難になることがあります。 そのような場合、これらのエントリに依存するスクリプトがなければ、トレース フラグ 3226 を使用することによってこれらのバックアップ ログ エントリを除外できます。 詳細については、「[トレース フラグ &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)」を参照してください。

## <a name="Security"></a> セキュリティ

データベースのバックアップでは、**TRUSTWORTHY** は OFF に設定されます。 **TRUSTWORTHY** を ON に設定する方法については、「[ALTER DATABASE の SET オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)」を参照してください。

[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降では、バックアップの作成での **PASSWORD** および **MEDIAPASSWORD** オプションが廃止されました。 パスワード付きで作成されたバックアップを復元することは、引き続き可能です。

## <a name="Permissions"></a> Permissions

`BACKUP DATABASE` および `BACKUP LOG` アクセス許可は、既定では、**sysadmin** 固定サーバー ロール、**db_owner** 固定データベース ロール、および **db_backupoperator** 固定データベース ロールのメンバーに与えられます。

 バックアップ デバイスの物理ファイルに対する所有と許可の問題によって、バックアップ操作が妨げられることがあります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスでは、デバイスに対して読み書きを実行できる必要があります。つまり、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスが実行されているアカウントには、バックアップ デバイスに対する書き込み権限が必要です。 ただし、システム テーブルにバックアップ デバイスのエントリを追加する [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)では、ファイル アクセスの権限は確認されません。 結果として、バックアップ デバイスの物理ファイルに関する問題は、バックアップや復元が試行され、物理リソースがアクセスされるまで、表面化しない可能性があります。

## <a name="SSMSProcedure"></a> SQL Server Management Studio の使用

> [!NOTE]
> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してバックアップ タスクを指定する場合、 **[スクリプト]** ボタンをクリックしてスクリプトの保存先を選択することにより、対応する [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md) スクリプトを生成できます。

1. **オブジェクト エクスプローラー**で適切な [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続した後、サーバー ツリーを展開します。

1. **[データベース]** を展開し、ユーザー データベースを選択するか、または **[システム データベース]** を展開してシステム データベースを選択します。

1. バックアップするデータベースを右クリックし、 **[タスク]** をポイントして、 **[バックアップ]** をクリックします。

1. **[データベースのバックアップ]** ダイアログボックスで、選択したデータベースがドロップダウン リストに表示されます (これは、サーバー上の他の任意のデータベースに変更できます)。

1. **[バックアップの種類]** ドロップダウン リストで、目的のバックアップの種類 (既定値は **[完全]** ) を選択します。

   > [!IMPORTANT]
   > 差分バックアップまたはトランザクション ログ バックアップを実行するには、事前にデータベースの完全バックアップを少なくとも 1 回実行する必要があります。
   
1. **[バックアップ コンポーネント]** で **[データベース]** を選択します。

1. **[バックアップ先]** セクションで、バックアップ ファイルの既定の場所を確認します (../mssql/data フォルダー内)。

   別のデバイスにバックアップするには、 **[バックアップ先]** ドロップダウン リストを使用して、選択内容を変更します。 バックアップの速度を向上させるためにバックアップ セットを複数のファイルにストライプするには、 **[追加]** をクリックしてバックアップ オブジェクトやバックアップ先を追加します。
 
   バックアップ先を削除するには、バックアップ先を選択して **[削除]** をクリックします。 既存のバックアップ先の内容を表示するには、バックアップ先を選択して **[内容]** をクリックします。

1. (省略可能) **[メディア オプション]** と **[バックアップ オプション]** のページで、その他の使用可能な設定を確認します。

   さまざまなバックアップ オプションの詳細については、[[全般] ページ](back-up-database-general-page.md)、[[メディア オプション] ページ](back-up-database-media-options-page.md)、[[バックアップ オプション] ページ](back-up-database-backup-options-page.md)を参照してください。

1. **[OK]** をクリックしてバックアップを開始します。

1. バックアップが正常に完了したら、 **[OK]** をクリックして SQL Server Management Studio のダイアログ ボックスを閉じます。

### <a name="additional-information"></a>関連情報

- データベースの完全バックアップを作成したら、[データベースの差分バックアップ](create-a-differential-database-backup-sql-server.md)または[トランザクション ログ バックアップ](back-up-a-transaction-log-sql-server.md)を作成できます。

- (省略可能) **[コピーのみのバックアップ]** チェック ボックスをオンにして、コピーのみのバックアップを作成することもできます。 *コピーのみのバックアップ*は、従来の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップのシーケンスから独立した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップです。 詳細については、「[コピーのみのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)」を参照してください。 コピーのみのバックアップは、 **[差分]** バックアップの種類には使用できません。

- URL にバックアップする場合は、 **[メディア オプション]** ページで、 **[メディアに上書きします]** が無効にされます。

### <a name="examples"></a>使用例

次の例では、次の Transact-SQL コードを使用してテスト データベースを作成します。

```sql
USE [master]
GO

CREATE DATABASE [SQLTestDB]
GO

USE [SQLTestDB]
GO
CREATE TABLE SQLTest
   (
      ID INT NOT NULL PRIMARY KEY,
      c1 VARCHAR(100) NOT NULL,
      dt1 DATETIME NOT NULL DEFAULT getdate()
   );
GO

USE [SQLTestDB]
GO

INSERT INTO SQLTest (ID, c1) VALUES (1, 'test1')
INSERT INTO SQLTest (ID, c1) VALUES (2, 'test2')
INSERT INTO SQLTest (ID, c1) VALUES (3, 'test3')
INSERT INTO SQLTest (ID, c1) VALUES (4, 'test4')
INSERT INTO SQLTest (ID, c1) VALUES (5, 'test5')
GO

SELECT * FROM SQLTest
GO
```

#### <a name="a-full-back-up-to-disk-to-default-location"></a>A. 既定の場所のディスクへの完全バックアップ

この例では、`SQLTestDB` データベースを既定のバックアップ場所にあるディスクにバックアップします。

1. **オブジェクト エクスプローラー**で適切な [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続した後、サーバー ツリーを展開します。

1. **[データベース]** を展開して `SQLTestDB`を右クリックし、 **[タスク]** をポイントしてから **[バックアップ]** をクリックします。

1. **[OK]** をクリックします。

1. バックアップが正常に完了したら、 **[OK]** をクリックして SQL Server Management Studio のダイアログ ボックスを閉じます。

![SQL のバックアップを取得する](media/quickstart-backup-restore-database/backup-db-ssms.png)

#### <a name="b-full-back-up-to-disk-to-non-default-location"></a>B. 既定以外の場所のディスクへの完全バックアップ

この例では、ご自分で選択した場所にあるディスクに `SQLTestDB` データベースがバックアップされます。

1. **オブジェクト エクスプローラー**で適切な [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続した後、サーバー ツリーを展開します。

1. **[データベース]** を展開して `SQLTestDB`を右クリックし、 **[タスク]** をポイントしてから **[バックアップ]** をクリックします。

1. **[全般]** ページの **[バックアップ先]** セクションで、 **[バックアップ先]** ドロップダウン リストから **[ディスク]** を選択します。

1. 既存のバックアップ ファイルがすべて削除されるまで、 **[削除]** を選択します。

1. **[追加]** を選択すると、 **[バックアップ先の選択]** ダイアログ ボックスが開きます。

1. **[ファイル名]** テキスト ボックスに有効なパスとファイル名を入力し、拡張子として **.bak** を使用することで、このファイルの分類を簡略化します。

1. **[OK]** をクリックしてから、もう一度 **[OK]** をクリックしてバックアップを開始します。

1. バックアップが正常に完了したら、 **[OK]** をクリックして SQL Server Management Studio のダイアログ ボックスを閉じます。

![DB の場所を変更する](media/create-a-full-database-backup-sql-server/change-db-location.png)

#### <a name="c-create-an-encrypted-backup"></a>C. 暗号化されたバックアップの作成

この例では、`SQLTestDB` データベースを暗号化して既定のバックアップ場所にバックアップします。

1. **オブジェクト エクスプローラー**で適切な [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続した後、サーバー ツリーを展開します。

1. **[データベース]** 、 **[システム データベース]** の順に展開し、`master` を右クリックして **[新しいクエリ]** をクリックします。これにより、ご利用の `SQLTestDB` データベースに接続した状態でクエリ ウィンドウが開きます。

1. 次のコマンドを実行して、`master` データベース内に[**データベース マスター キー**](../../relational-databases/security/encryption/create-a-database-master-key.md)と[**証明書**](../../t-sql/statements/create-certificate-transact-sql.md)を作成します。  

   ```sql
   -- Create the master key
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  

   -- If the master key already exists, open it in the same session that you create the certificate (see next step)
   OPEN MASTER KEY DECRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe'

   -- Create the certificate encrypted by the master key
   CREATE CERTIFICATE MyCertificate
   WITH SUBJECT = 'Backup Cert', EXPIRY_DATE = '20201031';  
   ```

1. **オブジェクト エクスプローラー**の **[データベース]** ノードで、`SQLTestDB` を右クリックし、 **[タスク]** をポイントしてから **[バックアップ]** をクリックします。

1. **[メディア オプション]** ページの **[メディアを上書きする]** セクションで、 **[新しいメディア セットにバックアップし、すべての既存のバックアップ セットを消去する]** をオンにします。

1. **[バックアップ オプション]** ページの **[暗号化]** セクションで、 **[バックアップを暗号化する]** チェック ボックスをオンにします。

1. [アルゴリズム] ボックスの一覧から、 **[AES 256]** を選択します。

1. **[証明書または非対称キー]** ボックスの一覧で、 `MyCertificate`を選択します。

1. **[OK]** を選択します。

![暗号化されたバックアップ](media/create-a-full-database-backup-sql-server/encrypted-backup.png)

#### <a name="d-back-up-to-the-azure-blob-storage-service"></a>D. Azure BLOB ストレージ サービスへのバックアップ

以下の例では、Azure Blob Storage サービスへの `SQLTestDB` のデータベースの完全バックアップを実行します。 この例では、BLOB コンテナーを含むストレージ アカウントを既に用意していることを前提としています。 この例では、共有アクセス署名が自動的に作成されます。この例では、既存の共有アクセス署名のあるコンテナーがないからです。

ストレージ アカウントに Azure BLOB コンテナーがない場合は、続行する前に作成してください。 詳細については、「[汎用ストレージアカウントの作成](https://docs.microsoft.com/azure/storage/common/storage-quickstart-create-account?tabs=azure-portal)」と「[コンテナーを作成する](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal#create-a-container)」を参照してください。

1. **オブジェクト エクスプローラー**で適切な [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続した後、サーバー ツリーを展開します。

1. **[データベース]** を展開して `SQLTestDB`を右クリックし、 **[タスク]** をポイントしてから **[バックアップ]** をクリックします。

1. **[全般]** ページの **[宛先]** セクションで、 **[バックアップ先]** ドロップダウン リストから **[URL]** を選択します。

1. **[追加]** をクリックすると、 **[バックアップ先の選択]** ダイアログ ボックスが開きます。

1. SQL Server Management Studio で使用する Azure ストレージ コンテナーを以前に登録したことがある場合は、それを選択します。 それ以外の場合は、 **[新しいコンテナー]** をクリックして新しいコンテナーを登録します。

1. **[Microsoft サブスクリプションへの接続]** ダイアログ ボックスで、ご利用のアカウントにサインインします。

1. **[ストレージ アカウントの選択]** ドロップダウン テキスト ボックスで、ご利用のストレージ アカウントを選択します。

1. **[BLOB コンテナーの選択]** ドロップダウン テキスト ボックスで、ご利用の BLOB コンテナーを選択します。

1. **[Shared Access Policy の有効期限]** ドロップダウン カレンダー ボックスで、この例で作成した共有アクセスポリシーの有効期限を選択します。

1. SQL Server Management Studio で **[資格情報の作成]** をクリックして、共有アクセス署名と資格情報を生成します。

1. **[OK]** をクリックして、 **[Microsoft サブスクリプションへの接続]** ダイアログ ボックスを閉じます。

1. **[バックアップ ファイル]** テキスト ボックスで、バックアップ ファイルの名前を変更します (省略可能)。

1. **[OK]** をクリックして **[バックアップ先の選択]** ダイアログ ボックスを閉じます。

1. **[OK]** をクリックしてバックアップを開始します。

1. バックアップが正常に完了したら、 **[OK]** をクリックして SQL Server Management Studio のダイアログ ボックスを閉じます。

## <a name="TsqlProcedure"></a> Transact-SQL の使用

次の項目を指定して `BACKUP DATABASE` ステートメントを実行し、データベースの完全バックアップを作成します。

- バックアップするデータベースの名前。
- データベースの完全バックアップを書き込むバックアップ デバイス。

データベースの完全バックアップのための [!INCLUDE[tsql](../../includes/tsql-md.md)] の基本構文を次に示します。

 BACKUP DATABASE *database* TO *backup_device* [ **,** ...*n* ] [ WITH *with_options* [ **,** ...*o* ] ] ;

|オプション|[説明]|
|------------|-----------------|
|*database*|バックアップするデータベースです。|
|*backup_device* [ **,** ...*n* ]|バックアップ操作に使用する 1 ～ 64 個のバックアップ デバイスの一覧を指定します。 物理バックアップ デバイスを指定したり、対応する論理バックアップ デバイス (既に定義されている場合) を指定したりできます。 物理バックアップ デバイスを指定するには、DISK オプションまたは TAPE オプションを使用します。<br /><br /> { DISK &#124; TAPE } **=** _physical\_backup\_device\_name_<br /><br /> 詳細については、「 [バックアップ デバイス &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)」を参照してください。|
|WITH *with_options* [ **,** ...*o* ]|必要に応じて、1 つ以上の追加オプション ( *o*) を指定します。 基本的な with オプションについては、手順 2. を参照してください。|
|||

必要に応じて、1 つ以上の **WITH** オプションを指定します。 ここでは、一部の基本的な **WITH** オプションについて説明します。 すべての **WITH** オプションについては、「[BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)」を参照してください。

基本的なバックアップ セットの **WITH** オプション:

- **{ COMPRESSION | NO_COMPRESSION }** :[!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 以降でのみ、このバックアップで [バックアップの圧縮](../../relational-databases/backup-restore/backup-compression-sql-server.md) を実行するかどうかを指定し、サーバー レベルの既定値をオーバーライドできます。
- **ENCRYPTION (ALGORITHM, SERVER CERTIFICATE | ASYMMETRIC KEY)** : SQL Server 2014 以降でのみ、使用する暗号化アルゴリズムと暗号化の保護に使用する証明書または非対称キーを指定します。
- **DESCRIPTION** **=** { **'** _text_ **'**  |  **@** _text\_variable_ }:バックアップ セットを記述したテキストを自由な形式で指定します。 文字列の長さは最大 255 文字です。
- **NAME = { *backup_set_name* |  **@** _backup\_set\_name\_var_ }** :バックアップ セットの名前を指定します。 名前の長さは最大 128 文字です。 NAME を指定しないと、名前は空白になります。

既定では、`BACKUP` ではバックアップが既存のメディア セットに追加されて、既存のバックアップ セットが保持されます。 これを明示的に指定するには、`NOINIT` オプションを使用します。 既存のバックアップ セットへの追加については、「 [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)」を参照してください。

また、**FORMAT** オプションを使用して、バックアップ メディアをフォーマットすることもできます。

 FORMAT [ **,** MEDIANAME **=** { *media_name* |  **@** _media\_name\_variable_ } ] [ **,** MEDIADESCRIPTION **=** { *text* |  **@** _text\_variable_ } ]

 **FORMAT** 句は、バックアップ メディアを初めて使用する場合や既存のデータをすべて上書きする場合に使用します。 必要に応じて、新しいメディアにメディア名と説明を割り当てます。

 > [!IMPORTANT]
 > `BACKUP` ステートメントで **FORMAT** 句を使用すると、バックアップ メディアに格納されているバックアップが破棄されるので、十分注意して使用してください。

### <a name="TsqlExample"></a> 使用例

次の例では、次の Transact-SQL コードを使用してテスト データベースを作成します。

```sql
USE [master]
GO

CREATE DATABASE [SQLTestDB]
GO

USE [SQLTestDB]
GO
CREATE TABLE SQLTest (
   ID INT NOT NULL PRIMARY KEY,
   c1 VARCHAR(100) NOT NULL,
   dt1 DATETIME NOT NULL DEFAULT GETDATE()
)
GO

USE [SQLTestDB]
GO

INSERT INTO SQLTest (ID, c1) VALUES (1, 'test1')
INSERT INTO SQLTest (ID, c1) VALUES (2, 'test2')
INSERT INTO SQLTest (ID, c1) VALUES (3, 'test3')
INSERT INTO SQLTest (ID, c1) VALUES (4, 'test4')
INSERT INTO SQLTest (ID, c1) VALUES (5, 'test5')
GO

SELECT * FROM SQLTest
GO
```

#### <a name="a-back-up-to-a-disk-device"></a>A. ディスク デバイスへのバックアップ

次の例では、新しいメディア セットを作成する `SQLTestDB` を使用して、 `FORMAT` データベース全体をディスクにバックアップします。

```sql
USE SQLTestDB;
GO
BACKUP DATABASE SQLTestDB
TO DISK = 'c:\tmp\SQLTestDB.bak'
   WITH FORMAT,
      MEDIANAME = 'SQLServerBackups',
      NAME = 'Full Backup of SQLTestDB';
GO
```

#### <a name="b-back-up-to-a-tape-device"></a>B. テープ デバイスへのバックアップ

 次の例では、 `SQLTestDB` データベース全体をテープにバックアップし、以前のバックアップに追加します。

```sql
USE SQLTestDB;
GO
BACKUP DATABASE SQLTestDB
   TO TAPE = '\\.\Tape0'
   WITH NOINIT,
      NAME = 'Full Backup of SQLTestDB';
GO
```

#### <a name="c-back-up-to-a-logical-tape-device"></a>C. 論理テープ デバイスへのバックアップ

次の例では、テープ ドライブ用の論理バックアップ デバイスを作成した後、 そのデバイスに SQLTestDB データベース全体をバックアップします。

```sql
-- Create a logical backup device,
-- SQLTestDB_Bak_Tape, for tape device \\.\tape0.
USE master;
GO
EXEC sp_addumpdevice 'tape', 'SQLTestDB_Bak_Tape', '\\.\tape0'; USE SQLTestDB;
GO
BACKUP DATABASE SQLTestDB
   TO SQLTestDB_Bak_Tape
   WITH FORMAT,
      MEDIANAME = 'SQLTestDB_Bak_Tape',
      MEDIADESCRIPTION = '\\.\tape0',
      NAME = 'Full Backup of SQLTestDB';
GO
```

## <a name="PowerShellProcedure"></a> PowerShell の使用

**Backup-SqlDatabase** コマンドレットを使用します。 データベースの完全バックアップであることを明示するには、 **-BackupAction** パラメーターにその既定値 **Database** を指定します。 このパラメーターは、データベースの完全バックアップでは省略可能です。

> [!NOTE]
> これらの例では、SqlServer モジュールが必要です。 それがインストールされているかどうかを判断するには、`Get-Module -Name SqlServer` を実行します。 このモジュールをインストールするには、PowerShell の管理者セッションで `Install-Module -Name SqlServer` を実行します。
>
> 詳細については、「 [SQL Server PowerShell プロバイダー](https://docs.microsoft.com/sql/powershell/sql-server-powershell-provider)」を参照してください。

> [!IMPORTANT]
> SQL Server Management Studio 内から PowerShell ウィンドウを開いて SQL Server のインストールに接続する場合、PowerShell とご利用の SQL Server インスタンスとの接続の確立には SSMS 内のご利用の資格情報が自動的に使用されるので、この例の資格情報の部分は省略できます。

### <a name="examples"></a>使用例

#### <a name="a-full-backup-local"></a>A. 完全バックアップ (ローカル)

次の例では、 `<myDatabase>` データベースの完全なバックアップを、サーバー インスタンス `Computer\Instance`の既定のバックアップ場所に作成します。 オプションで、この例では **-BackupAction Database**を指定します。

完全な構文とその他の例については、「[Backup-SqlDatabase](https://docs.microsoft.com/powershell/module/sqlserver/backup-sqldatabase)」を参照してください。

```powershell
$credential = Get-Credential

Backup-SqlDatabase -ServerInstance Computer[\Instance] -Database <myDatabase> -BackupAction Database -Credential $credential
```

#### <a name="b-full-backup-to-azure"></a>B. Azure への完全バックアップ

次の例では、Azure Blob Storage サービスに `<myDatabase>` インスタンスのデータベース `<myServer>` の完全バックアップを作成します。 保存されたアクセス ポリシーは読み取り、書き込み、および一覧表示権で作成されています。 SQL Server 資格情報 `https://<myStorageAccount>.blob.core.windows.net/<myContainer>`は、保存されたアクセス ポリシーに関連付けられている Shared Access Signature を使用して作成されています。 PowerShell コマンドでは **BackupFile** パラメーターを使用して、場所 (URL) とバックアップ ファイル名を指定します。

```powershell
$credential = Get-Credential
$container = 'https://<myStorageAccount>blob.core.windows.net/<myContainer>'
$fileName = '<myDatabase>.bak'
$server = '<myServer>'
$database = '<myDatabase>
$backupFile = $container + '/' + $fileName

Backup-SqlDatabase -ServerInstance $server -Database $database -BackupFile $backupFile -Credential $credential
```

## <a name="RelatedTasks"></a> 関連タスク

- [データベースのバックアップ (SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)
- [データベースの差分バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)
- [SSMS を使用したデータベース バックアップの復元](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)
- [単純復旧モデルでのデータベース バックアップの復元 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)
- [完全復旧モデルで障害発生時点までデータベースを復元する方法 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)
- [データベースを新しい場所に復元する &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)
- [メンテナンス プラン ウィザードの使用](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)

## <a name="see-also"></a>参照

- [SQL Server のバックアップと復元操作のトラブルシューティング](https://support.microsoft.com/kb/224071)
- [バックアップの概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)
- [トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)
- [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)
- [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)
- [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)
- [データベースのバックアップ &#40;全般ページ&#41;](../../relational-databases/backup-restore/back-up-database-general-page.md)
- [データベースのバックアップ &#40;バックアップ オプション ページ&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)
- [差分バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)
- [データベースの完全バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)
