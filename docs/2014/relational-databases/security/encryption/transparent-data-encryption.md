---
title: 透過的なデータ暗号化 (TDE) | Microsoft Docs
ms.custom: ''
ms.date: 11/23/2015
ms.prod: sql-server-2014
ms.reviewer: ''
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
manager: craigg
ms.openlocfilehash: e73098a63f193ab868854674d2e77c3ba372c29c
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957116"
---
# <a name="transparent-data-encryption-tde"></a>透過的なデータ暗号化 (TDE)
  *Transparent Data Encryption* (tde) は[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 、 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]保存データの暗号化と呼ばれるデータファイルを暗号化します。 セキュリティで保護されたシステムの設計、機密資産の暗号化、データベース サーバーに対するファイアウォールの構築などの、データベースを保護するいくつかの対策を講じることができます。 ただし、物理メディア (ドライブやバックアップ テープなど) が盗まれるシナリオでは、悪意のある第三者がデータベースを復元するかアタッチするだけでデータを閲覧することができます。 ソリューションの 1 つとして、データベース内の機密データを暗号化し、証明書を使用してデータを暗号化するために使用するキーを保護することが挙げられます。 これにより、キーを持たない人物によるデータの使用を防止できますが、このような保護は事前に計画する必要があります。  
  
 TDE は、データとログ ファイルの I/O 暗号化と複合化をリアルタイムで実行します。 暗号化は、復旧中に、可用性のためのデータベース ブート レコードに格納されるデータベース暗号化キー (DEK) を使用します。 DEK は、サーバーの master データベースに保存されている証明書を使用して保護される対称キーか、EKM モジュールによって保護される非対称キーです。 TDE は、"保存" データ、つまりデータとログ ファイルを保護します。 多数の法律、規制、さまざまな業界で制定されたガイドラインに準拠する機能を提供します。 これによりソフトウェア開発者は、既存のアプリケーションを変更することなく、AES および 3DES 暗号化アルゴリズムを使用してデータを暗号化できます。  
  
> [!IMPORTANT]
>  TDE では、通信チャネル全体を暗号化することはできません。 通信チャネル全体でデータを暗号化する方法の詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
> 
>  **関連トピック:**  
> 
>  -   [Azure SQL Database での Transparent Data Encryption](../../../database-engine/transparent-data-encryption-with-azure-sql-database.md)  
> -   [TDE で保護されたデータベースを別の SQL Server に移動する](move-a-tde-protected-database-to-another-sql-server.md)  
> -   [EKM を使用して TDE を有効にする](enable-tde-on-sql-server-using-ekm.md)  
  
## <a name="about-tde"></a>TDE について  
 データベース ファイルの暗号化は、ページ レベルで実行されます。 暗号化されたデータベースのページは、ディスクに書き込まれる前に暗号化され、メモリに読み込まれるときに暗号化解除されます。 TDE では、暗号化されたデータベースのサイズが増えることはありません。  
  
 **に適用される情報[!INCLUDE[ssSDS](../../../includes/sssds-md.md)]**  
  
 TDE を [!INCLUDE[sqldbesa](../../../includes/sqldbesa-md.md)] V12 ([一部のリージョンではプレビュー版](https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)) と一緒に使用すると、マスター データベースに格納されるサーバー レベルの証明書が [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]によって自動的に作成されます。 
  [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] で TDE データベースを移動するには、データベースの暗号化を解除してデータベースを移動し、移動先の [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]で TDE を再度有効にする必要があります。 
  [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]での TDE に関する詳細な手順については、「 [Transparent Data Encryption with Azure SQL Database](../../../database-engine/transparent-data-encryption-with-azure-sql-database.md)」を参照してください。  
  
 TDE のプレビューの状態は、 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] のバージョン ファミリ V12 が現在一般提供の段階にあると発表されている地理的リージョンのサブセットにおいても適用されます。 TDE がプレビューから GA に昇格されたことを [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] が発表するまで、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 用の TDE の実稼働データベースでの使用は想定されていません。 
  [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] V12 の詳細については、「 [Azure SQL Database の新機能](https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/)」をご覧ください。  
  
 **に適用される情報[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**  
  
 セキュリティで保護されたデータベースは、正しい証明書を使用することで復元できます。 証明書の詳細については、「 [SQL Server Certificates and Asymmetric Keys](../sql-server-certificates-and-asymmetric-keys.md)」をご覧ください。  
  
 TDE を有効にしたら、証明書とそれに関連付けられた秘密キーを直ちにバックアップする必要があります。 証明書が使用できなくなった場合、またはデータベースを別のサーバーに復元またはアタッチする必要がある場合に、証明書と秘密キーの両方のバックアップが必要です。これらのバックアップがない場合は、データベースを開けません。 暗号化証明書は、データベースで TDE を無効にした場合でも保持する必要があります。 データベースが暗号化されていない場合でも、トランザクション ログの一部はまだ保護されたままである場合があるため、データベースの完全バックアップが実行されるまでは、一部の操作では証明書が必要な場合があります。 有効期限の日付を過ぎた証明書であっても、TDE によりデータを暗号化および暗号化解除できる場合があります。  
  
 **暗号化階層**  
  
 TDE 暗号化のアーキテクチャを次の図に示します。 
  [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]で TDE を使用する場合に、ユーザーによって構成可能なのは、データベース レベルの項目 (データベース暗号化キーと ALTER DATABASE の部分) のみです。  
  
 ![トピックで説明された階層。](../../../database-engine/media/tde-architecture.gif "トピックで説明された階層。")  
  
## <a name="using-transparent-data-encryption"></a>Transparent Data Encryption の使用  
 TDE を使用するには、次の手順を実行します。  
  
||  
|-|  
|**適用対象**: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。|  
  
-   マスター キーを作成します。  
  
-   マスター キーで保護された証明書を作成または取得します。  
  
-   データベース暗号化キーを作成し、証明書で保護します。  
  
-   暗号化を使用するようにデータベースを設定します。  
  
 次の例では、 `AdventureWorks2012` という名前のサーバーにインストールされた証明書を使用して、 `MyServerCert`データベースを暗号化および暗号化解除しています。  
  
```  
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
>  TDE が有効になっているデータベースのバックアップ ファイルも、データベース暗号化キーを使用して暗号化されます。 このため、このバックアップを復元するときには、データベース暗号化キーを保護している証明書が必要です。 つまり、データの損失を防ぐには、データベースをバックアップするだけでなく、サーバー証明書のバックアップも確実に保守する必要があります。 証明書が使用できなくなると、データの損失が発生します。 詳細については、「 [SQL Server Certificates and Asymmetric Keys](../sql-server-certificates-and-asymmetric-keys.md)」をご覧ください。  
  
## <a name="commands-and-functions"></a>コマンドと関数  
 TDE の証明書を次に示すステートメントで処理できるようにするには、この証明書をデータベース マスター キーで暗号化する必要があります。 パスワードだけで暗号化された証明書は、ステートメントで暗号化機能として受け付けられません。  
  
> [!IMPORTANT]  
>  TDE で使用された証明書をパスワードで保護するように変更すると、再起動後にデータベースにアクセスできなくなります。  
  
 次の表に、TDE のコマンドと関数の説明とリンクを示します。  
  
|コマンドまたは関数|目的|  
|-------------------------|-------------|  
|[Transact-sql&#41;&#40;データベース暗号化キーを作成する](/sql/t-sql/statements/create-database-encryption-key-transact-sql)|データベースの暗号化に使用されるキーを作成します。|  
|[Transact-sql&#41;&#40;データベース暗号化キーの変更](/sql/t-sql/statements/alter-database-encryption-key-transact-sql)|データベースの暗号化に使用されるキーを変更します。|  
|[Transact-sql&#41;&#40;データベース暗号化キーを削除します。](/sql/t-sql/statements/drop-database-transact-sql)|データベースの暗号化に使用されたキーを削除します。|  
|[Transact-sql&#41;&#40;の ALTER DATABASE SET オプション](/sql/t-sql/statements/alter-database-transact-sql-set-options)|TDE を有効にするために使用される `ALTER DATABASE` オプションについて説明します。|  
  
## <a name="catalog-views-and-dynamic-management-views"></a>カタログ ビューと動的管理ビュー  
 次の表に、TDE のカタログ ビューと動的管理ビューを示します。  
  
|カタログ ビューまたは動的管理ビュー|目的|  
|---------------------------------------------|-------------|  
|[データベース &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)|データベース情報を表示するカタログ ビュー|  
|[sys. 証明書 &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-certificates-transact-sql)|データベース内の証明書を表示するカタログ ビュー|  
|[dm_database_encryption_keys &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)|データベースで使用されている暗号化キー、およびデータベースの暗号化の状態に関する情報を表示する動的管理ビュー|  
  
## <a name="permissions"></a>アクセス許可  
 TDE の各機能とコマンドには、上の表で説明されているように、個別の権限要件があります。  
  
 TDE に関係するメタデータを表示するには、証明書に対する VIEW DEFINITION 権限が必要です。  
  
## <a name="considerations"></a>考慮事項  
 データベース暗号化操作の再暗号化スキャンが実行されている間は、データベースに対するメンテナンス操作が無効になります。 メンテナンス操作を実行するには、データベースに対してシングル ユーザー モード設定を使用します。 詳細については、「 [データベースをシングル ユーザー モードに設定する](../../databases/set-a-database-to-single-user-mode.md)」を参照してください。  
  
 データベースの暗号化の状態を確認するには、sys.dm_database_encryption_keys 動的管理ビューを使用します。 詳細については、このトピックの「カタログ ビューと動的管理ビュー」を参照してください。  
  
 TDE では、データベース内のすべてのファイルとファイル グループが暗号化されます。 データベースに READ ONLY とマークされているファイル グループがあると、データベースの暗号化操作は失敗します。  
  
 データベースがデータベース ミラーリングまたはログ配布で使用されている場合は、両方のデータベースが暗号化されます。 トランザクション ログは、2 つのデータベースの間で送信されるときに暗号化されます。  
  
> [!IMPORTANT]  
>  データベースを暗号化の対象として設定すると、新しいフルテキスト インデックスが暗号化されるようになります。 以前に作成されたフルテキスト インデックスは、アップグレード時にインポートされ、データが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]に読み込まれると TDE で暗号化されます。 列でフルテキスト インデックスを有効にすると、フルテキスト インデックス スキャンの実行時に、その列のデータがプレーンテキストでディスクに書き込まれる可能性があります。 暗号化された機密データにはフルテキスト インデックスを作成しないことをお勧めします。  
  
 暗号化されたデータは、暗号化されていない同等のデータより、圧縮比率が大幅に下がります。 TDE を使用してデータベースを暗号化した場合、バックアップの圧縮によってバックアップ ストレージが大幅に圧縮されることはありません。 したがって、TDE とバックアップの圧縮を併用することはお勧めしません。  
  
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
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のログ ファイル アーキテクチャの詳細については、「[トランザクション ログ &#40;SQL Server&#41;](../../logs/the-transaction-log-sql-server.md)」を参照してください。  
  
 データベース暗号化キーを変更する前にトランザクション ログに書き込まれたデータは、以前のデータベース暗号化キーで暗号化されます。  
  
 データベース暗号化キーを 2 回変更した後は、データベース暗号化キーを再度変更する前に、ログ バックアップを実行する必要があります。  
  
### <a name="transparent-data-encryption-and-the-tempdb-system-database"></a>Transparent Data Encryption と tempdb システム データベース  
 tempdb システム データベースは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス上の他のデータベースが TDE を使用して暗号化されると暗号化されます。 この場合、同じ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンス上にある暗号化されないデータベースのパフォーマンスに影響が生じることがあります。 tempdb システム データベースの詳細については、「 [tempdb データベース](../../databases/tempdb-database.md)」を参照してください。  
  
### <a name="transparent-data-encryption-and-replication"></a>Transparent Data Encryption とレプリケーション  
 レプリケーションでは、TDE が有効になっているデータベースのデータが暗号化された形式で自動的にレプリケートされることはありません。 ディストリビューション データベースとサブスクライバー データベースを保護する場合は、TDE を個別に有効にする必要があります。 スナップショット レプリケーションでは、トランザクション レプリケーションとマージ レプリケーションへの最初のデータ ディストリビューションと同様に、暗号化されていない中間ファイル (bcp ファイルなど) にデータを格納できます。  トランザクション レプリケーションまたはマージ レプリケーション時に、暗号化を有効にして通信チャネルを保護することができます。 詳細については、「[データベースエンジン &#40;SQL Server 構成マネージャー&#41;への暗号化接続の有効化](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
### <a name="transparent-data-encryption-and-filestream-data"></a>Transparent Data Encryption と FILESTREAM データ  
 FILESTREAM データは TDE が有効になっている場合でも暗号化されません。  
  
### <a name="transparent-data-encryption-and-buffer-pool-extension"></a>Transparent Data Encryption とバッファー プール拡張機能  
 バッファー プール拡張機能 (BPE) に関連するファイルは、データベースが TDE を使用して暗号化される場合でも暗号化されません。 BPE 関連のファイルについては、Bitlocker や EFS などのファイル システム レベルの暗号化ツールを使用する必要があります。  
  
## <a name="transparent-data-encryption-and-in-memory-oltp"></a>Transparent Data Encryption とインメモリ OLTP  
 TDE は、インメモリ OLTP オブジェクトを含むデータベースで有効にすることができます。 TDE が有効な場合、インメモリ OLTP ログ レコードが暗号化されます。 MEMORY_OPTIMIZED_DATA ファイル グループのデータは、TDE が有効な場合は暗号化されません。  
  
## <a name="see-also"></a>参照  
 [TDE で保護されたデータベースを別の SQL Server に移動する](move-a-tde-protected-database-to-another-sql-server.md)   
 [EKM を使用して TDE を有効にする](enable-tde-on-sql-server-using-ekm.md)   
 [Azure SQL Database での Transparent Data Encryption](../../../database-engine/transparent-data-encryption-with-azure-sql-database.md)   
 [SQL Server 暗号化](sql-server-encryption.md)   
 [SQL Server とデータベースの暗号化キー &#40;データベースエンジン&#41;](sql-server-and-database-encryption-keys-database-engine.md)   
 [SQL Server データベースエンジンおよび Azure SQL Database の Security Center](../security-center-for-sql-server-database-engine-and-azure-sql-database.md)   
 [FILESTREAM &#40;SQL Server&#41;](../../blob/filestream-sql-server.md)  
  
  
