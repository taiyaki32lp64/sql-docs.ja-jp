---
title: 透過的なデータ暗号化
description: Parallel data Warehouse (PDW) 用の Transparent data encryption (TDE) は、データファイルとトランザクションログファイルおよび特別な PDW ログファイルのリアルタイム i/o 暗号化と暗号化解除を実行します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: e75230ed175c6fbf1b0a2492265bbe12067060ca
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399934"
---
# <a name="transparent-data-encryption"></a>Transparent Data Encryption
セキュリティで保護されたシステムの設計、機密資産の暗号化、データベース サーバーに対するファイアウォールの構築などの、データベースを保護するいくつかの対策を講じることができます。 ただし、物理メディア (ドライブやバックアップテープなど) が盗まれた場合は、悪意のある人物がデータベースを復元またはアタッチしてデータを参照するだけで済みます。 ソリューションの 1 つとして、データベース内の機密データを暗号化し、証明書を使用してデータを暗号化するために使用するキーを保護することが挙げられます。 これにより、キーを持たない人物によるデータの使用を防止できますが、このような保護は事前に計画する必要があります。  
  
*Transparent data encryption* (tde) では、データファイルとトランザクションログファイル、および特別な PDW ログファイルの i/o 暗号化と暗号化解除がリアルタイムで実行されます。 暗号化は、復旧中に、可用性のためのデータベース ブート レコードに格納されるデータベース暗号化キー (DEK) を使用します。 DEK は、SQL Server PDW の master データベースに格納されている証明書を使用してセキュリティで保護された対称キーです。 TDE は、"保存" データ、つまりデータとログ ファイルを保護します。 多数の法律、規制、さまざまな業界で制定されたガイドラインに準拠する機能を提供します。 この機能により、ソフトウェア開発者は、既存のアプリケーションを変更することなく、AES および3DES 暗号化アルゴリズムを使用してデータを暗号化できます。  
  
> [!IMPORTANT]  
> TDE では、クライアントと PDW の間で移動するデータの暗号化は提供されません。 クライアントと SQL Server PDW の間でデータを暗号化する方法の詳細については、「[証明書のプロビジョニング](provision-certificate.md)」を参照してください。  
>   
> TDE では、移動中または使用中のデータは暗号化されません。 SQL Server PDW 内の PDW コンポーネント間の内部トラフィックは暗号化されません。 メモリバッファーに一時的に格納されるデータは暗号化されません。 このリスクを軽減するには、SQL Server PDW への物理的なアクセスと接続を制御します。  
  
セキュリティで保護されたデータベースは、正しい証明書を使用することで復元できます。  
  
> [!NOTE]  
> TDE 用の証明書を作成する場合は、関連付けられている秘密キーと共に、直ちにバックアップする必要があります。 証明書が使用できなくなった場合、またはデータベースを別のサーバーに復元またはアタッチする必要がある場合に、証明書と秘密キーの両方のバックアップが必要です。これらのバックアップがない場合は、データベースを開けません。 暗号化証明書は、データベースで TDE を無効にした場合でも保持する必要があります。 データベースが暗号化されていない場合でも、トランザクション ログの一部はまだ保護されたままである場合があるため、データベースの完全バックアップが実行されるまでは、一部の操作では証明書が必要な場合があります。 有効期限の日付を過ぎた証明書であっても、TDE によりデータを暗号化および暗号化解除できる場合があります。  
  
データベース ファイルの暗号化は、ページ レベルで実行されます。 暗号化されたデータベースのページは、ディスクに書き込まれる前に暗号化され、メモリに読み込まれるときに暗号化解除されます。 TDE では、暗号化されたデータベースのサイズが増えることはありません。  
  
次の図は、TDE 暗号化のキーの階層を示しています。  
  
![階層を表示します。](media/tde-architecture.png "TDE_Architecture")  
  
## <a name="using-tde"></a>Transparent Data Encryption の使用  
TDE を使用するには、次の手順を実行します。 最初の3つの手順は、TDE をサポートする SQL Server PDW を準備するときに1回だけ実行されます。  
  
1.  マスターキーを master データベースに作成します。  
  
2.  **Sp_pdw_database_encryption**を使用して、SQL Server PDW で tde を有効にします。 この操作では、一時データベースを変更して、将来の一時データを確実に保護します。一時テーブルを持つアクティブなセッションがある場合は、この操作を実行しようとすると失敗します。 **sp_pdw_database_encryption**は、pdw システムログでユーザーデータのマスキングを有効にします。 (PDW システムログでのユーザーデータのマスキングの詳細については、「 [sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)」を参照してください)。  
  
3.  [Sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)を使用して、証明書のバックアップが格納される共有への認証と書き込みが可能な資格情報を作成します。 目的のストレージサーバーの資格情報が既に存在する場合は、既存の資格情報を使用できます。  
  
4.  Master データベースで、マスターキーによって保護されている証明書を作成します。  
  
5.  証明書をストレージ共有にバックアップします。  
  
6.  ユーザーデータベースで、データベース暗号化キーを作成し、master データベースに格納されている証明書で保護します。  
  
7.  `ALTER DATABASE`ステートメントを使用して、tde を使用してデータベースを暗号化します。  
  
次の例は、SQL Server PDW `AdventureWorksPDW2012`で作成された`MyServerCert`という名前の証明書を使用してデータベースを暗号化する方法を示しています。  
  
**最初: SQL Server PDW で TDE を有効にします。** この操作は、1回だけ実行する必要があります。  
  
```sql  
USE master;  
GO  
  
-- Create a database master key in the master database  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';  
GO  
  
-- Enable encryption for PDW  
EXEC sp_pdw_database_encryption 1;  
GO  
  
-- Add a credential that can write to the share  
-- A credential created for a backup can be used if you wish  
EXEC sp_pdw_add_network_credentials 'SECURE_SERVER', '<domain>\<Windows_user>', '<password>';  
```  
  
**2番目: master データベースに証明書を作成してバックアップします。** この操作は1回だけ実行する必要があります。 データベースごとに個別の証明書を使用できます (推奨)。または、1つの証明書を使用して複数のデータベースを保護することができます。  
  
```sql  
-- Create certificate in master  
CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My DEK Certificate';  
GO  
  
-- Back up the certificate with private key  
BACKUP CERTIFICATE MyServerCert   
    TO FILE = '\\SECURE_SERVER\cert\MyServerCert.cer'  
    WITH PRIVATE KEY   
    (   
        FILE = '\\SECURE_SERVER\cert\MyServerCert.key',  
        ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>'   
    )   
GO  
```  
  
**最後: DEK を作成し、ALTER DATABASE を使用してユーザーデータベースを暗号化します。** この操作は、TDE によって保護されているデータベースごとに繰り返されます。  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_128  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO  
  
ALTER DATABASE AdventureWorksPDW2012 SET ENCRYPTION ON;  
GO  
```  
  
暗号化および暗号化解除の操作は、SQL Server によってバックグラウンドスレッドでスケジュールされます。 これらの操作の状態を表示するには、この記事の後半に記載されている一覧のカタログビューと動的管理ビューを使用します。  
  
> [!CAUTION]  
> TDE が有効になっているデータベースのバックアップ ファイルも、データベース暗号化キーを使用して暗号化されます。 このため、このバックアップを復元するときには、データベース暗号化キーを保護している証明書が必要です。 つまり、データの損失を防ぐには、データベースをバックアップするだけでなく、サーバー証明書のバックアップも確実に保守する必要があります。 証明書が使用できなくなると、データの損失が発生します。  
  
## <a name="commands-and-functions"></a>コマンドと関数  
TDE の証明書を次に示すステートメントで処理できるようにするには、この証明書をデータベース マスター キーで暗号化する必要があります。  
  
次の表に、TDE のコマンドと関数の説明とリンクを示します。  
  
|コマンドまたは関数|目的|  
|-----------------------|-----------|  
|[データベース暗号化キーの作成](../t-sql/statements/create-database-encryption-key-transact-sql.md)|データベースの暗号化に使用されるキーを作成します。|  
|[データベース暗号化キーの変更](../t-sql/statements/alter-database-encryption-key-transact-sql.md)|データベースの暗号化に使用されるキーを変更します。|  
|[データベース暗号化キーの削除](../t-sql/statements/drop-database-encryption-key-transact-sql.md)|データベースの暗号化に使用されたキーを削除します。|  
|[データベースの変更](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)|TDE を有効にするために使用される **ALTER DATABASE** オプションについて説明します。|  
  
## <a name="catalog-views-and-dynamic-management-views"></a>カタログ ビューと動的管理ビュー  
次の表に、TDE のカタログ ビューと動的管理ビューを示します。  
  
|カタログ ビューまたは動的管理ビュー|目的|  
|-------------------------------------------|-----------|  
|[システムデータベース](../relational-databases/system-catalog-views/sys-databases-transact-sql.md)|データベース情報を表示するカタログ ビュー|  
|[sys. 証明書](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)|データベース内の証明書を表示するカタログ ビュー|  
|[dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)|各ノード、データベースで使用される暗号化キー、およびデータベースの暗号化の状態に関する情報を提供する動的管理ビュー。|  
  
## <a name="permissions"></a>アクセス許可  
TDE の各機能とコマンドには、上の表で説明されているように、個別の権限要件があります。  
  
TDE に関連するメタデータを表示`CONTROL SERVER`するには、アクセス許可が必要です。  
  
## <a name="considerations"></a>考慮事項  
データベース暗号化操作の再暗号化スキャンが実行されている間は、データベースに対するメンテナンス操作が無効になります。  
  
データベースの暗号化の状態を確認するには、 **dm_pdw_nodes_database_encryption_keys**動的管理ビューを使用します。 詳細については、この記事の前の方の「*カタログビューと動的管理ビュー* 」を参照してください。  
  
### <a name="restrictions"></a>制限  
`CREATE DATABASE ENCRYPTION KEY`、 `ALTER DATABASE ENCRYPTION KEY`、 `DROP DATABASE ENCRYPTION KEY`、または`ALTER DATABASE...SET ENCRYPTION`ステートメントでは、次の操作は許可されません。  
  
-   データベースの削除。  
  
-   `ALTER DATABASE`コマンドを使用します。  
  
-   データベースバックアップを開始しています。  
  
-   データベースの復元を開始しています。  
  
次の操作または条件により`CREATE DATABASE ENCRYPTION KEY`、 `ALTER DATABASE ENCRYPTION KEY`、 `DROP DATABASE ENCRYPTION KEY`、、 `ALTER DATABASE...SET ENCRYPTION`またはステートメントが禁止されます。  
  
-   `ALTER DATABASE`コマンドを実行しています。  
  
-   データ バックアップが実行されている。  
  
データベース ファイルを作成する際には、TDE が有効になっているとファイルの瞬時初期化を使用できません。  
  
### <a name="areas-not-protected-by-tde"></a>TDE によって保護されていない領域  
TDE では、外部テーブルは保護されません。  
  
TDE では、診断セッションは保護されません。 診断セッションを使用している間は、機微なパラメーターを使用してクエリを実行しないように注意する必要があります。 機密情報を公開する診断セッションは、不要になったらすぐに削除する必要があります。  
  
TDE によって保護されたデータは SQL Server PDW メモリに配置されると、暗号化が解除されます。 アプライアンスで特定の問題が発生すると、メモリダンプが作成されます。 ダンプファイルは、問題の発生時にメモリの内容を表し、暗号化されていない形式で機微なデータを含むことができます。 メモリダンプの内容は、他のユーザーと共有する前に確認する必要があります。  
  
Master データベースは TDE によって保護されていません。 Master データベースにはユーザーデータは含まれませんが、ログイン名などの情報が含まれています。  
  
### <a name="transparent-data-encryption-and-transaction-logs"></a>Transparent Data Encryption とトランザクション ログ  
データベースで TDE の使用を有効にすると、仮想トランザクションログの残りの部分が解放され、次の仮想トランザクションログが強制的に適用されます。 これにより、データベースが暗号化対象として設定された後にトランザクション ログにクリア テキストが残らないことが保証されます。 次の例のように、 `encryption_state` `sys.dm_pdw_nodes_database_encryption_keys`ビューの列を表示することで、各 PDW ノードのログファイルの暗号化の状態を確認できます。  
  
```sql  
WITH dek_encryption_state AS   
(  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id, encryption_state  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
        INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
           ON dek.database_id = node_db_map.database_id AND dek.pdw_node_id = node_db_map.pdw_node_id  
        LEFT JOIN sys.pdw_database_mappings AS db_map  
            ON node_db_map .physical_name = db_map.physical_name  
        INNER JOIN sys.dm_pdw_nodes AS nodes  
            ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
)  
SELECT TOP 1 encryption_state  
       FROM dek_encryption_state  
       WHERE dek_encryption_state.database_id = DB_ID('AdventureWorksPDW2012 ')  
       ORDER BY (CASE encryption_state WHEN 3 THEN -1 ELSE encryption_state END) DESC;  
```  
  
データベース暗号化キーを変更する前にトランザクション ログに書き込まれたデータは、以前のデータベース暗号化キーで暗号化されます。  
  
### <a name="pdw-activity-logs"></a>PDW アクティビティログ  
SQL Server PDW は、トラブルシューティングを目的とした一連のログを保持します。 (これは、トランザクションログ、SQL Server エラーログ、または Windows イベントログではないことに注意してください)。これらの PDW アクティビティログには、完全なステートメントをクリアテキストで含めることができ、その一部にはユーザーデータを含めることができます。 一般的な例として、 **INSERT**ステートメントと**UPDATE**ステートメントがあります。 **Sp_pdw_log_user_data_masking**を使用すると、ユーザーデータのマスキングを明示的に有効または無効にすることができます。 SQL Server PDW の暗号化を有効にすると、PDW アクティビティログ内のユーザーデータのマスクが自動的にオンになり、保護されます。 **sp_pdw_log_user_data_masking**は、tde を使用しない場合にステートメントをマスクするためにも使用できますが、Microsoft サポートチームが問題を分析する能力を大幅に削減するため、この方法はお勧めしません。  
  
### <a name="transparent-data-encryption-and-the-tempdb-system-database"></a>Transparent Data Encryption と tempdb システム データベース  
[Sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)を使用して暗号化が有効になっている場合、tempdb システムデータベースは暗号化されます。 これは、すべてのデータベースで TDE を使用する前に必要です。 これにより、SQL Server PDW の同じインスタンスで暗号化されていないデータベースのパフォーマンスが低下する可能性があります。  
  
## <a name="key-management"></a>キー管理  
データベース暗号化キー (DEK) は、master データベースに格納されている証明書によって保護されます。 これらの証明書は、master データベースのデータベースマスターキー (DMK) によって保護されます。 TDE に使用するには、DMK をサービスマスターキー (SMK) によって保護する必要があります。  
  
システムは、ユーザーの介入を必要とせずに (パスワードの入力など)、キーにアクセスできます。 証明書が使用できない場合は、適切な証明書が使用可能になるまで DEK の暗号化を解除できないことを示すエラーが出力されます。  
  
あるアプライアンスから別のアプライアンスにデータベースを移動する場合、その ' DEK ' を保護するために使用される証明書は、移行先サーバーで最初に復元する必要があります。 その後、データベースを通常どおり復元できます。 詳細については、標準の SQL Server のドキュメントを参照してください。 [TDE で保護されたデータベースを別の SQL Server に移動](https://technet.microsoft.com/library/ff773063.aspx)します。  
  
DEKs の暗号化に使用される証明書は、それらを使用するデータベースバックアップが存在する限り保持する必要があります。 証明書のバックアップには証明書の秘密キーが含まれている必要があります。秘密キーがないと、データベースの復元に証明書を使用できないためです。 これらの証明書の秘密キーのバックアップは別のファイルに保存され、証明書の復元用に指定する必要があるパスワードによって保護されます。  
  
## <a name="restoring-the-master-database"></a>Master データベースの復元  
Master データベースは、ディザスターリカバリーの一環として、 **Dwconfig**を使用して復元できます。  
  
-   制御ノードが変更されていない場合、つまり、master データベースのバックアップが作成されたのとは異なるアプライアンスに master データベースが復元された場合、DMK とすべての証明書は追加の操作なしで読み取り可能になります。  
  
-   Master データベースが別のアプライアンスに復元された場合、または master データベースのバックアップ後に制御ノードが変更された場合は、DMK を再生成するために追加の手順が必要になります。  
  
    1.  DMK を開きます。  
  
        ```sql  
        OPEN MASTER KEY DECRYPTION BY PASSWORD = '<password>';  
        ```  
  
    2.  SMK で暗号化を追加します。  
  
        ```sql  
        ALTER MASTER KEY   
            ADD ENCRYPTION BY SERVICE MASTER KEY;  
        ```  
  
    3.  アプライアンスを再起動します。  
  
## <a name="upgrade-and-replacing-virtual-machines"></a>Virtual Machines のアップグレードと置換  
アップグレードまたは置換 VM が実行されたアプライアンスに DMK が存在する場合、DMK password をパラメーターとして指定する必要があります。  
  
アップグレードアクションの例。 を`**********` DMK パスワードに置き換えます。  
  
`setup.exe /Action=ProvisionUpgrade ... DMKPassword='**********'`  
  
バーチャルマシンを置き換えるアクションの例。  
  
`setup.exe /Action=ReplaceVM ... DMKPassword='**********'`  
  
アップグレード時に、ユーザーデータベースが暗号化されていて、DMK パスワードが指定されていない場合、アップグレード操作は失敗します。 置換中に、DMK が存在するときに正しいパスワードが指定されていない場合、操作は DMK の回復手順をスキップします。 他のすべての手順は、[VM の置換] アクションの最後に完了します。ただし、追加の手順が必要であることを示すために、操作は最後に失敗を報告します。 セットアップログ ( **\ProgramData\Microsoft\Microsoft SQL Server Parallel Data Warehouse\100\Logs\Setup\\<タイムスタンプ> のセットアップ**) で、最後の近くに次の警告が表示されます。  
  
`*** WARNING \*\*\* DMK is detected in master database, but could not be recovered automatically! The DMK password was either not provided or is incorrect!`
  
次のステートメントを PDW で手動で実行し、DMK を回復するためにアプライアンスを再起動します。  
  
```sql
OPEN MASTER KEY DECRYPTION BY PASSWORD = '<DMK password>';  
ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY;  
```
  
「 **Master データベースの復元**」の手順に従って、データベースを回復してから、アプライアンスを再起動します。  
  
DMK が以前に存在していても、アクション後に復旧されなかった場合、データベースに対してクエリを実行すると、次のエラーメッセージが表示されます。  
  
```sql
Msg 110806;  
A distributed query failed: Database '<db_name>' cannot be opened due to inaccessible files or insufficient memory or disk space. See the SQL Server errorlog for details.
```  
  
## <a name="performance-impact"></a>パフォーマンスへの影響  
TDE のパフォーマンスへの影響は、使用しているデータの種類、データの格納方法、および SQL Server PDW におけるワークロードアクティビティの種類によって異なります。 TDE によって保護されている場合、データの読み取りと復号化の i/o、またはデータの暗号化と書き込みを行う i/o は CPU 集中型のアクティビティであり、他の CPU 集中型のアクティビティが同時に発生すると、より多くの影響を受けます。 TDE が暗号化`tempdb`するため、tde は暗号化されていないデータベースのパフォーマンスに影響を与える可能性があります。 パフォーマンスを正確に把握するには、データとクエリアクティビティを使用してシステム全体をテストする必要があります。  
  
## <a name="related-content"></a>関連コンテンツ  
次のリンクには、SQL Server が暗号化を管理する方法に関する一般的な情報が記載されています。 これらの記事は、SQL Server の暗号化について理解するのに役立ちますが、これらの記事には、SQL Server PDW に固有の情報は含まれておらず、SQL Server PDW には存在しない機能について説明しています。  
  
-   [SQL Server 暗号化](../relational-databases/security/encryption/sql-server-encryption.md)  
  
-   [暗号化階層](../relational-databases/security/encryption/encryption-hierarchy.md)  
  
-   [SQL Server とデータベースの暗号化キー](../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  

  
## <a name="see-also"></a>参照  
[データベースの変更](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)  
[マスターキーの作成](../t-sql/statements/create-master-key-transact-sql.md)  
[データベース暗号化キーの作成](../t-sql/statements/create-database-encryption-key-transact-sql.md)  
[バックアップ証明書](../t-sql/statements/backup-certificate-transact-sql.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[sp_pdw_database_encryption_regenerate_system_keys](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
[sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
[sys. 証明書](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)  
[dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)  
  
