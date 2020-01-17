---
title: 透過的なデータ暗号化 (TDE) | Microsoft Docs
ms.custom: ''
ms.date: 05/09/2019
ms.prod: sql
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Transparent Data Encryption
- database encryption key, about
- TDE
- database encryption key
- TDE, about
- Transparent Data Encryption, about
- encryption [SQL Server], transparent data encryption
ms.assetid: c75d0d4b-4008-4e71-9a9d-cee2a566bd3b
author: jaszymas
ms.author: jaszymas
ms.reviewer: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 498fe2391cd3e8109aed3f6e1e02436234ffe6f7
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957327"
---
# <a name="transparent-data-encryption-tde"></a>Transparent Data Encryption (TDE)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  *透過的なデータ暗号化* (TDE) では、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)]、 [!INCLUDE[ssSDWfull](../../../includes/sssdwfull-md.md)] のデータ ファイルを暗号化します。これは、静止したデータの暗号化として知られています。 セキュリティで保護されたシステムの設計、機密資産の暗号化、データベース サーバーに対するファイアウォールの構築などの、データベースを保護するいくつかの対策を講じることができます。 ただし、物理メディア (ドライブやバックアップ テープなど) が盗まれるシナリオでは、悪意のある第三者がデータベースを復元するかアタッチするだけでデータを閲覧することができます。 解決策の 1 つは、データベース内の機密データを暗号化し、データの暗号化に使用されるキーを証明書で保護することです。 これにより、キーを持たない人物によるデータの使用を防止できますが、このような保護は事前に計画する必要があります。  
  
 TDE は、データとログ ファイルの I/O 暗号化と複合化をリアルタイムで実行します。 暗号化は、復旧中に、可用性のためのデータベース ブート レコードに格納されるデータベース暗号化キー (DEK) を使用します。 DEK は、サーバーの master データベースに保存されている証明書を使用して保護される対称キーか、EKM モジュールによって保護される非対称キーです。 TDE では、"静止した" データ、つまりデータとログ ファイルが保護されます。 この暗号化は、法律、規制、およびさまざまな業界で確立されているガイドラインの多くに準拠できるようになっています。 これによりソフトウェア開発者は、既存のアプリケーションを変更することなく、AES および 3DES 暗号化アルゴリズムを使用してデータを暗号化できます。  
  
> [!IMPORTANT]
>  TDE では、通信チャネル全体を暗号化することはできません。 通信チャネル全体でデータを暗号化する方法の詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
> 
>  **関連項目:**  
> 
>  -   [Azure SQL Database での Transparent Data Encryption](../../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md)  
> -   [SQL Data Warehouse での Transparent Data Encryption (TDE) の概要](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-encryption-tde-tsql/)  
> -   [別の SQL Server への TDE で保護されたデータベースの移動](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md)  
> -   [EKM の使用による TDE の有効化](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)   
> -   [SQL 暗号化機能への SQL Server コネクタの使用](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)
> - [よく寄せられる質問での TDE についての SQL Server セキュリティ ブログ](https://blogs.msdn.microsoft.com/sqlsecurity/2016/10/05/feature-spotlight-transparent-data-encryption-tde/)
 
  
## <a name="about-tde"></a>TDE について  
 データベース ファイルの暗号化は、ページ レベルで実行されます。 暗号化されたデータベースのページは、ディスクに書き込まれる前に暗号化され、メモリに読み込まれるときに暗号化解除されます。 TDE では、暗号化されたデータベースのサイズが増えることはありません。  
  
 **[!INCLUDE[ssSDS](../../../includes/sssds-md.md)] に該当する情報**  
  
 TDE を [!INCLUDE[sqldbesa](../../../includes/sqldbesa-md.md)] V12 と一緒に使用すると、マスター データベースに格納されるサーバー レベルの証明書が [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] によって自動的に作成されます。 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] で TDE データベースを移動する目的では、移動操作の際、データベースの暗号化を解除する必要がありません。 TDE と [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] の活用方法については、「[Azure SQL Database の Transparent Data Encryption](../../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md)」を参照してください。  
  
 **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に該当する情報**  
  
 セキュリティで保護されたデータベースは、正しい証明書を使用することで復元できます。 証明書の詳細については、「 [SQL Server Certificates and Asymmetric Keys](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)」をご覧ください。  
  
 TDE を有効にしたら、証明書とそれに関連付けられた秘密キーを直ちにバックアップする必要があります。 証明書が使用できなくなった場合、またはデータベースを別のサーバーに復元またはアタッチする必要がある場合に、証明書と秘密キーの両方のバックアップが必要です。これらのバックアップがない場合は、データベースを開けません。 暗号化証明書は、データベースで TDE を無効にした場合でも保持する必要があります。 データベースが暗号化されていない場合でも、トランザクション ログの一部はまだ保護されたままである場合があるため、データベースの完全バックアップが実行されるまでは、一部の操作では証明書が必要な場合があります。 有効期限の日付を過ぎた証明書であっても、TDE によりデータを暗号化および暗号化解除できる場合があります。  
  
 **暗号化階層**  
  
 TDE 暗号化のアーキテクチャを次の図に示します。 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]で TDE を使用する場合に、ユーザーによって構成可能なのは、データベース レベルの項目 (データベース暗号化キーと ALTER DATABASE の部分) のみです。  
  
 ![トピックで説明された階層を表示します。](../../../relational-databases/security/encryption/media/tde-architecture.png "トピックで説明された階層を表示します。")  
  
## <a name="using-transparent-data-encryption"></a>Transparent Data Encryption の使用  
 TDE を使用するには、次の手順を実行します。  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
-   マスター キーを作成します。  
  
-   マスター キーで保護された証明書を作成または取得します。  
  
-   データベース暗号化キーを作成し、証明書で保護します。  
  
-   暗号化を使用するようにデータベースを設定します。  
  
 次の例では、 `AdventureWorks2012` という名前のサーバーにインストールされた証明書を使用して、 `MyServerCert`データベースを暗号化および暗号化解除しています。  
  
```sql  
USE master;  
GO  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';  
go  
CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My DEK Certificate';  
go  
USE AdventureWorks2012;  
GO  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_128  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO  
ALTER DATABASE AdventureWorks2012  
SET ENCRYPTION ON;  
GO  
```  
  
 暗号化および暗号化解除の操作は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]によってバックグラウンド スレッドでスケジュールされます。 これらの操作の状態は、この後の一覧に示すカタログ ビューおよび動的管理ビューを使用して確認できます。  
  
> [!CAUTION]  
>  TDE が有効になっているデータベースのバックアップ ファイルも、データベース暗号化キーを使用して暗号化されます。 このため、このバックアップを復元するときには、データベース暗号化キーを保護している証明書が必要です。 つまり、データの損失を防ぐには、データベースをバックアップするだけでなく、サーバー証明書のバックアップも確実に保守する必要があります。 証明書が使用できなくなると、データの損失が発生します。 詳細については、「 [SQL Server Certificates and Asymmetric Keys](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)」をご覧ください。  
  
## <a name="commands-and-functions"></a>コマンドと関数  
 TDE の証明書を次に示すステートメントで処理できるようにするには、この証明書をデータベース マスター キーで暗号化する必要があります。 それらがパスワードだけで暗号化されている場合は、ステートメントで暗号化機能として受け付けられません。  
  
> [!IMPORTANT]  
>  TDE で使用された証明書をパスワードで保護するように変更すると、再起動後にデータベースにアクセスできなくなります。  
  
 次の表に、TDE のコマンドと関数の説明とリンクを示します。  
  
|コマンドまたは関数|目的|  
|-------------------------|-------------|  
|[CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-encryption-key-transact-sql.md)|データベースの暗号化に使用されるキーを作成します。|  
|[ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-encryption-key-transact-sql.md)|データベースの暗号化に使用されるキーを変更します。|  
|[DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-database-encryption-key-transact-sql.md)|データベースの暗号化に使用されたキーを削除します。|  
|[ALTER DATABASE SET のオプション &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql-set-options.md)|TDE を有効にするために使用される **ALTER DATABASE** オプションについて説明します。|  
  
## <a name="catalog-views-and-dynamic-management-views"></a>カタログ ビューと動的管理ビュー  
 次の表に、TDE のカタログ ビューと動的管理ビューを示します。  
  
|カタログ ビューまたは動的管理ビュー|目的|  
|---------------------------------------------|-------------|  
|[sys.databases &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)|データベース情報を表示するカタログ ビュー|  
|[sys.certificates &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)|データベース内の証明書を表示するカタログ ビュー|  
|[sys.dm_database_encryption_keys &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md)|データベースで使用されている暗号化キー、およびデータベースの暗号化の状態に関する情報を表示する動的管理ビュー|  
  
## <a name="permissions"></a>アクセス許可  
 TDE の各機能とコマンドには、上の表で説明されているように、個別の権限要件があります。  
  
 TDE に関係するメタデータを表示するには、証明書に対する VIEW DEFINITION 権限が必要です。  
  
## <a name="considerations"></a>考慮事項  
 データベース暗号化操作の再暗号化スキャンが実行されている間は、データベースに対するメンテナンス操作が無効になります。 メンテナンス操作を実行するには、データベースに対してシングル ユーザー モード設定を使用します。 詳細については、「 [データベースをシングル ユーザー モードに設定する](../../../relational-databases/databases/set-a-database-to-single-user-mode.md)」を参照してください。  
  
 データベースの暗号化の状態を確認するには、sys.dm_database_encryption_keys 動的管理ビューを使用します。 詳細については、このトピックの「カタログ ビューと動的管理ビュー」を参照してください。  
  
 TDE では、データベース内のすべてのファイルとファイル グループが暗号化されます。 データベースに READ ONLY とマークされているファイル グループがあると、データベースの暗号化操作は失敗します。  
  
 データベースがデータベース ミラーリングまたはログ配布で使用されている場合は、両方のデータベースが暗号化されます。 トランザクション ログは、2 つのデータベースの間で送信されるときに暗号化されます。  
  
> [!IMPORTANT]  
>  データベースを暗号化の対象として設定すると、フルテキスト インデックスが暗号化されるようになります。 SQL Server 2008 よりも前に作成されたフルテキスト インデックスは、SQL Server 2008 以上へのアップグレード中にデータベースにインポートされて TDE で暗号化されるようになります。  

> [!TIP]  
> データベースの TDE ステータスの変更を監視するには、SQL Server Audit または SQL Database Auditing を使用します。 SQL Server では、TDE は、[SQL Server Audit Action Groups and Actions](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md) (SQL Server Audit のアクション グループとアクション) で説明されている監査アクション グループ DATABASE_CHANGE_GROUP の下で追跡されます。
  
### <a name="restrictions"></a>制限  
 最初のデータベース暗号化、キー変更、またはデータベースの暗号化解除の実行中は、次の操作を実行できません。  
  
-   データベース内のファイル グループからのファイルの削除  
  
-   データベースの削除  
  
-   データベースのオフライン化  
  
-   データベースのデタッチ  
  
-   データベースまたはファイル グループの READ ONLY 状態への移行  
  
 CREATE DATABASE ENCRYPTION KEY、ALTER DATABASE ENCRYPTION KEY、DROP DATABASE ENCRYPTION KEY、または ALTER DATABASE...SET ENCRYPTION の各ステートメントの実行中は、次の操作を実行できません。  
  
-   データベース内のファイル グループからのファイルの削除  
  
-   データベースの削除。  
  
-   データベースのオフライン化  
  
-   データベースのデタッチ  
  
-   データベースまたはファイル グループの READ ONLY 状態への移行  
  
-   ALTER DATABASE コマンドの使用  
  
-   データベースまたはデータベース ファイルのバックアップの開始  
  
-   データベースまたはデータベース ファイルの復元の開始  
  
-   スナップショットの作成  
  
 次の操作または状況が発生すると、CREATE DATABASE ENCRYPTION KEY、ALTER DATABASE ENCRYPTION KEY、DROP DATABASE ENCRYPTION KEY、または ALTER DATABASE...SET ENCRYPTION の各ステートメントを実行できなくなります。  
  
-   データベースが読み取り専用であるか、読み取り専用のファイル グループを含んでいる。  
  
-   ALTER DATABASE コマンドが実行されている。  
  
-   データ バックアップが実行されている。  
  
-   データベースがオフラインまたは復元中である。  
  
-   スナップショットが実行されている。  
  
-   データベース メンテナンス タスク。  
  
 データベース ファイルを作成する際には、TDE が有効になっているとファイルの瞬時初期化を使用できません。  
  
 非対称キーでデータベース暗号化キーを暗号化するには、非対称キーが拡張キー管理プロバイダーに存在している必要があります。  
  
### <a name="transparent-data-encryption-and-transaction-logs"></a>Transparent Data Encryption とトランザクション ログ  
 データベースで TDE の使用を有効にすると、仮想トランザクション ログの残りの部分が "ゼロ設定" され、強制的に次の仮想トランザクション ログに移行します。 これにより、データベースが暗号化対象として設定された後にトランザクション ログにクリア テキストが残らないことが保証されます。 ログ ファイルの暗号化の状態を確認するには、次の例のように `encryption_state` ビュー内の `sys.dm_database_encryption_keys` 列を表示します。  
  
```  
USE AdventureWorks2012;  
GO  
/* The value 3 represents an encrypted state   
   on the database and transaction logs. */  
SELECT *  
FROM sys.dm_database_encryption_keys  
WHERE encryption_state = 3;  
GO  
```  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のログ ファイル アーキテクチャの詳細については、「[トランザクション ログ &#40;SQL Server&#41;](../../../relational-databases/logs/the-transaction-log-sql-server.md)」を参照してください。  
  
 データベース暗号化キーを変更する前にトランザクション ログに書き込まれたデータは、以前のデータベース暗号化キーで暗号化されます。  
  
 データベース暗号化キーを 2 回変更した後は、データベース暗号化キーを再度変更する前に、ログ バックアップを実行する必要があります。  
  
### <a name="transparent-data-encryption-and-the-tempdb-system-database"></a>Transparent Data Encryption と tempdb システム データベース  
 tempdb システム データベースは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス上の他のデータベースが TDE を使用して暗号化されると暗号化されます。 この場合、同じ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンス上にある暗号化されないデータベースのパフォーマンスに影響が生じることがあります。 tempdb システム データベースの詳細については、「 [tempdb データベース](../../../relational-databases/databases/tempdb-database.md)」を参照してください。  
  
### <a name="transparent-data-encryption-and-replication"></a>Transparent Data Encryption とレプリケーション  
 レプリケーションでは、TDE が有効になっているデータベースのデータが暗号化された形式で自動的にレプリケートされることはありません。 ディストリビューション データベースとサブスクライバー データベースを保護する場合は、TDE を個別に有効にする必要があります。 スナップショット レプリケーションでは、トランザクション レプリケーションとマージ レプリケーションへの最初のデータ ディストリビューションと同様に、暗号化されていない中間ファイル (bcp ファイルなど) にデータを格納できます。  トランザクション レプリケーションまたはマージ レプリケーション時に、暗号化を有効にして通信チャネルを保護することができます。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
### <a name="transparent-data-encryption-and-filestream-data"></a>Transparent Data Encryption と FILESTREAM データ  
 FILESTREAM データは TDE が有効になっている場合でも暗号化されません。  

<a name="scan-suspend-resume"></a>

## <a name="transparent-data-encryption-tde-scan"></a>Transparent Data Encryption (TDE) スキャン

データベースで Transparent Data Encryption (TDE) を有効にするには、各ページをデータ ファイルからバッファー プールに読み込み、暗号化されたページをディスクから書き戻す暗号化のスキャンを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で実行する必要があります。 ユーザーが暗号化のスキャンをより制御できるよう、構文の一時停止および再開が可能な、TDE スキャンが [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] に導入されています。これでは、システムでワークロードが多い場合やビジネスに極めて重要な時間のときはスキャンを一時停止し、後でスキャンを再開できます。

TDE 暗号化のスキャンを一時停止するには、次の構文を使用します。

```sql
ALTER DATABASE <db_name> SET ENCRYPTION SUSPEND;
```

同様に、次の構文で TDE 暗号化のスキャンを再開できます。

```sql
ALTER DATABASE <db_name> SET ENCRYPTION RESUME;
```

暗号化のスキャンの現在の状態を示すために、`sys.dm_database_encryption_keys` 動的管理ビューに `encryption_scan_state` が追加されています。 また、暗号化のスキャンの状態が最後に変更された日時を含む `encryption_scan_modify_date` という新しい列もあります。 暗号化のスキャンが一時停止中に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスが再開された場合、一時停止されている既存のスキャンがあることが起動時にエラー ログに記述されます。
  
## <a name="transparent-data-encryption-and-buffer-pool-extension"></a>Transparent Data Encryption とバッファー プール拡張機能  
 バッファー プール拡張機能 (BPE) に関連するファイルは、データベースが TDE を使用して暗号化される場合でも暗号化されません。 BPE 関連のファイルについては、BitLocker や EFS などのファイル システム レベルの暗号化ツールを使用する必要があります。  
  
## <a name="transparent-data-encryption-and-in-memory-oltp"></a>Transparent Data Encryption とインメモリ OLTP  
 TDE は、インメモリ OLTP オブジェクトを含むデータベースで有効にすることができます。 [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] と [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] では、TDE が有効な場合、インメモリ OLTP ログ レコードとデータが暗号化されます。 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] では、TDE が有効な場合、インメモリ OLTP ログ レコードは暗号化されますが、MEMORY_OPTIMIZED_DATA ファイルグループのファイルは暗号化されません。  
  
## <a name="related-tasks"></a>Related Tasks  
 [別の SQL Server への TDE で保護されたデータベースの移動](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md)  
 [EKM の使用による TDE の有効化](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
 [Azure Key Vault を使用する拡張キー管理 &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 [Azure SQL Database での Transparent Data Encryption](../../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md)  
 [SQL Data Warehouse での Transparent Data Encryption (TDE) の概要](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-encryption-tde-tsql/)  
 [SQL Server の暗号化](../../../relational-databases/security/encryption/sql-server-encryption.md)  
 [SQL Server とデータベースの暗号化キー &#40;データベース エンジン&#41;](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  
   
## <a name="see-also"></a>参照  
 [SQL Server データベース エンジンと Azure SQL Database のセキュリティ センター](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)   
 [FILESTREAM &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md)  
  
  
