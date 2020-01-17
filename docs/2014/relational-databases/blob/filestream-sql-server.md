---
title: FILESTREAM (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server]
- FILESTREAM [SQL Server], about
- FILESTREAM [SQL Server], overview
ms.assetid: 9a5a8166-bcbe-4680-916c-26276253eafa
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9c4d9b65fed30d09bf739271131d3b83afcd0902
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010138"
---
# <a name="filestream-sql-server"></a>FILESTREAM (SQL Server)
  FILESTREAM を使用すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ベースのアプリケーションで非構造化データ (ドキュメントやイメージなど) をファイル システムに格納できます。 これにより、ファイル システムの豊富なストリーミング API と高いパフォーマンスをアプリケーションで活用できるほか、非構造化データとそれに対応する構造化データの間でトランザクションの一貫性も維持されます。  
  
 FILESTREAM の統合、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]と NTFS ファイル システムを格納する、`varbinary(max)`ファイル システム上のファイルとしてバイナリ ラージ オブジェクト (BLOB) データ。 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントでは、FILESTREAM データの挿入、更新、クエリ、検索、およびバックアップを行うことができます。 Win32 ファイル システム インターフェイスによるデータへのストリーミング アクセスが可能になります。  
  
 FILESTREAM では、NT システム キャッシュを使用してファイル データをキャッシュします。 これにより、FILESTREAM データが [!INCLUDE[ssDE](../../includes/ssde-md.md)] のパフォーマンスに与える影響を軽減できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバッファー プールは使用されないため、そのメモリはクエリの処理に使用できます。  
  
 FILESTREAM は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をインストールまたはアップグレードしたときに自動的には有効になりません。 FILESTREAM は、SQL Server 構成マネージャーと [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用して有効にする必要があります。 FILESTREAM を使用するには、特殊なファイル グループを格納するためにデータベースを作成または変更する必要があります。 次に、テーブルを作成または変更して、FILESTREAM 属性を格納する `varbinary(max)` 列を含めます。 これらの手順を完了すると、 [!INCLUDE[tsql](../../includes/tsql-md.md)] および Win32 を使用して FILESTREAM データを管理できるようになります。  
  
 インストールして、FILESTREAM の使用の詳細については、の一覧を参照してください。[関連タスク](#reltasks)します。  
  
##  <a name="whentouse"></a> FILESTREAM を使用する場合  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では BLOB を、データをテーブルに格納する標準の `varbinary(max)` データとして使用することも、データをファイル システムに格納する FILESTREAM `varbinary(max)` オブジェクトとして使用することもできます。 データベース ストレージとファイル システム ストレージのどちらを使用するかは、データのサイズと用途によって決まります。 次の条件が true の場合は、FILESTREAM を使用することを検討する必要があります。  
  
-   格納するオブジェクトの平均的なサイズが 1 MB より大きい。  
  
-   高速な読み取りアクセスが重要とされる。  
  
-   アプリケーション ロジックに中間層を使用するアプリケーションを開発している。  
  
 比較的小さなオブジェクトの場合は、`varbinary(max)` BLOB をデータベースに格納する方が一般に高いストリーミング パフォーマンスが得られます。  
  
  
##  <a name="storage"></a> FILESTREAM ストレージ  
 FILESTREAM ストレージは、データを BLOB としてファイル システムに格納する `varbinary(max)` 列として実装されます。 BLOB のサイズはファイル システムのボリューム サイズによってのみ制限されます。 ファイル システムに格納される BLOB には、標準の `varbinary(max)` の制限 (ファイル サイズ 2 GB) は適用されません。  
  
 列のデータをファイル システムに格納するように指定するには、`varbinary(max)` 列で FILESTREAM 属性を指定します。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] では、これにより、その列のすべてのデータがファイル システム (データベース ファイル以外の場所) に格納されるようになります。  
  
 FILESTREAM データは FILESTREAM ファイル グループに格納する必要があります。 FILESTREAM ファイル グループは特殊なファイル グループで、ファイルそのものではなくファイル システム ディレクトリが含まれます。 これらのファイル システム ディレクトリは、 *データ コンテナー*と呼ばれます。 データ コンテナーは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ストレージとファイル システム ストレージの間のインターフェイスです。  
  
 FILESTREAM ストレージを使用する際は、以下の点を考慮してください。  
  
-   テーブルに FILESTREAM 列が含まれている場合には、各行に NULL でない一意の行 ID が必要です。  
  
-   FILESTREAM ファイル グループには、複数のデータ コンテナーを追加できます。  
  
-   FILESTREAM データ コンテナーを入れ子にすることはできません。  
  
-   フェールオーバー クラスタリングを使用している場合は、FILESTREAM ファイル グループが共有ディスク リソース上に存在する必要があります。  
  
-   FILESTREAM ファイル グループは、圧縮されたボリューム上にあってもかまいません。  
  
### <a name="integrated-management"></a>管理の統合  
 FILESTREAM は `varbinary(max)` 列として実装され、直接[!INCLUDE[ssDE](../../includes/ssde-md.md)]に統合されているため、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の管理ツールや関数のほとんどを FILESTREAM データで使用できます。FILESTREAM データに変更を加える必要もありません。 たとえば、すべてのバックアップ モデルと復旧モデルを FILESTREAM データで使用できるため、FILESTREAM データをデータベースの構造化データと共にバックアップできます。 FILESTREAM データをリレーショナル データと共にバックアップしない場合は、部分バックアップを使用して FILESTREAM ファイル グループを除外できます。  

  
### <a name="integrated-security"></a>Integrated Security  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の FILESTREAM データは、その他のデータと同じように、テーブルまたは列のレベルで権限を与えることによってセキュリティで保護されます。 テーブルの FILESTREAM 列に対する権限を持つユーザーは、関連付けられているファイルを開くことができます。  
  
> [!NOTE]  
>  FILESTREAM データでは暗号化はサポートされていません。  
  
 FILESTREAM コンテナーへの NTFS アクセス許可が与えられるのは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントが実行されているアカウントだけです。 その他のアカウントにはデータ コンテナーに対するアクセス許可を与えないようにすることをお勧めします。  
  
> [!NOTE]  
>  SQL ログインは、FILESTREAM コンテナーで使用できません。 FILESTREAM コンテナーでは NTFS 認証のみを使用できます。  
  
##  <a name="dual"></a> Transact-SQL およびファイル システム ストリーミング アクセスによる BLOB データへのアクセス  
 FILESTREAM 列にデータを格納した後、それらのファイルにアクセスするには、 [!INCLUDE[tsql](../../includes/tsql-md.md)] トランザクションか Win32 API を使用します。  
  
### <a name="transact-sql-access"></a>Transact-SQL アクセス  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、FILESTREAM データの挿入、更新、および削除を行うことができます。  
  
-   挿入操作を使用すると、null 値、空の値、または比較的短いインライン データを FILESTREAM フィールドに事前設定することができます。 ただし、大量のデータをファイルにストリーミングする場合は、Win32 インターフェイスを使用する方が効率的です。  
  
-   FILESTREAM フィールドを更新すると、その基となるファイル システムの BLOB データが変更されます。 FILESTREAM フィールドを NULL に設定すると、フィールドに関連付けられている BLOB データが削除されます。 UPDATE [!INCLUDE[tsql](../../includes/tsql-md.md)] .**Write() として実装されている**の大量の更新を使用してデータの部分更新を実行することはできません。  
  
-   FILESTREAM データを含む行を削除したり、FILESTREAM データを含むテーブルを削除したり切り捨てたりすると、その基となるファイル システムの BLOB データが削除されます。  
  
### <a name="file-system-streaming-access"></a>ファイル システム ストリーミング アクセス  
 Win32 のストリーミング サポートを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] トランザクションのコンテキストで使用できます。 トランザクション内で、まず、FILESTREAM 関数を使用してファイルの論理 UNC ファイル システム パスを取得します。 次に、OpenSqlFilestream API を使用してファイル ハンドルを取得します。 そのハンドルを Win32 ファイル ストリーミング インターフェイス (ReadFile() や WriteFile() など) で使用することにより、ファイル システム経由でファイルにアクセスしてファイルを更新できます。  
  
 ファイル操作はトランザクション処理なので、ファイル システムを通じて FILESTREAM ファイルを削除したりその名前を変更したりすることはできません。  
  
 **ステートメント モデル**  
  
 FILESTREAM のファイル システム アクセスは、ファイルのオープンとクローズを使用して [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実現しています。 ファイル ハンドルを開くとステートメントが開始され、ハンドルを閉じると終了します。 たとえば、書き込みハンドルを閉じると、UPDATE ステートメントが完了したときのように、テーブルに登録されている AFTER トリガーが起動します。  
  
 **ストレージの名前空間**  
  
 FILESTREAM では、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] が BLOB の物理ファイル システムの名前空間を制御します。 新しい組み込み関数の [PathName](/sql/relational-databases/system-functions/pathname-transact-sql)を使用すると、テーブルの各 FILESTREAM セルに対応する BLOB の論理 UNC パスを取得できます。 アプリケーションでは、この論理パスを使用して Win32 ハンドルを取得し、標準の Win32 ファイル システム インターフェイスを使用して BLOB データを操作します。 この関数は、FILESTREAM 列の値が NULL の場合は NULL を返します。  
  
 **ファイル システム アクセスのトランザクション処理**  
  
 新しい組み込み関数の [GET_FILESTREAM_TRANSACTION_CONTEXT()](/sql/t-sql/functions/get-filestream-transaction-context-transact-sql)を使用すると、セッションが関連付けられている現在のトランザクションを表すトークンを取得できます。 このトランザクションは、既に開始され、まだ中止もコミットもされていないトランザクションである必要があります。 アプリケーションでは、トークンを取得することにより、FILESTREAM のファイル システム ストリーミング操作を、既に開始されているトランザクションにバインドできます。 この関数は、明示的に開始されたトランザクションがない場合は NULL を返します。  
  
 トランザクションをコミットしたり中止したりする前にすべてのファイル ハンドルを閉じる必要があります。 トランザクションのスコープを超えてもハンドルが開いたままになっていると、そのハンドルに対するその後の読み取りが失敗します。そのハンドルに対するその後の書き込みは成功しますが、ディスクに実際のデータが書き込まれません。 同様に、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のデータベースやインスタンスがシャットダウンすると、開いているハンドルはすべて無効になります。  
  
 **トランザクションの持続性**  
  
 FILESTREAM では、トランザクションのコミット時に、ファイル システム ストリーミング アクセスから変更された FILESTREAM BLOB データのトランザクションの持続性が [!INCLUDE[ssDE](../../includes/ssde-md.md)] によって確保されます。  
  
 **分離のセマンティクス**  
  
 分離のセマンティクスは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のトランザクション分離レベルに従います。 [!INCLUDE[tsql](../../includes/tsql-md.md)] およびファイル システム アクセスでは、Read Committed 分離レベルがサポートされます。 Repeatable Read 操作、およびシリアル化可能な分離やスナップショット分離もサポートされます。 ダーティ リードはサポートされません。  
  
 ファイル システム アクセスのオープン操作はロックを待機しません。 トランザクション分離のためにデータにアクセスできない場合、オープン操作はすぐに失敗します。 分離違反のためにオープン操作を続行できない場合は、ストリーミング API 呼び出しが ERROR_SHARING_VIOLATION で失敗します。  
  
 アプリケーションでは、部分更新を実行できるようにするために、デバイス FS 制御 (FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT) を発行して、開いているハンドルが参照しているファイルに古い内容をフェッチすることができます。 これにより、サーバー側の古い内容がコピーされます。 アプリケーションのパフォーマンスが低下したり、非常に大きなファイルを操作する際にタイムアウトになったりしないように、非同期 I/O を使用することをお勧めします。  
  
 ハンドルへの書き込みが行われた後に FSCTL を発行すると、最後の書き込み操作は維持され、それより前の書き込みは失われます。  
  
 **ファイル システム API とサポートされる分離レベル**  
  
 分離違反が原因でファイル システム API がファイルを開くことができない場合、ERROR_SHARING_VIOLATION 例外が返されます。 この分離違反は、2 つのトランザクションが同じファイルにアクセスしようとしたときに発生します。 アクセス操作の結果は、ファイルが開かれたモードと、トランザクションが実行されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンに依存します。 次の表に、同じファイルにアクセスする 2 つのトランザクションで得られる可能性のある結果を示します。  
  
|トランザクション 1|トランザクション 2|SQL Server 2008 での結果|SQL Server 2008 R2 以降のバージョンでの結果|  
|-------------------|-------------------|--------------------------------|------------------------------------------------------|  
|読み取り用に開く。|読み取り用に開く。|どちらも成功します。|どちらも成功します。|  
|読み取り用に開く。|書き込み用に開く。|どちらも成功します。 トランザクション 2 の書き込み操作は、トランザクション 1 で実行される読み取り操作に影響しません。|どちらも成功します。 トランザクション 2 の書き込み操作は、トランザクション 1 で実行される読み取り操作に影響しません。|  
|書き込み用に開く。|読み取り用に開く。|トランザクション 2 の開く操作は、ERROR_SHARING_VIOLATION 例外で失敗します。|どちらも成功します。|  
|書き込み用に開く。|書き込み用に開く。|トランザクション 2 の開く操作は、ERROR_SHARING_VIOLATION 例外で失敗します。|トランザクション 2 の開く操作は、ERROR_SHARING_VIOLATION 例外で失敗します。|  
|読み取り用に開く。|SELECT 用に開く。|どちらも成功します。|どちらも成功します。|  
|読み取り用に開く。|UPDATE または DELETE 用に開く。|どちらも成功します。 トランザクション 2 の書き込み操作は、トランザクション 1 で実行される読み取り操作に影響しません。|どちらも成功します。 トランザクション 2 の書き込み操作は、トランザクション 1 で実行される読み取り操作に影響しません。|  
|書き込み用に開く。|SELECT 用に開く。|トランザクション 2 は、トランザクション 1 がコミットまたは終了するか、トランザクション ロックがタイムアウトするまで、ブロックされます。|どちらも成功します。|  
|書き込み用に開く。|UPDATE または DELETE 用に開く。|トランザクション 2 は、トランザクション 1 がコミットまたは終了するか、トランザクション ロックがタイムアウトするまで、ブロックされます。|トランザクション 2 は、トランザクション 1 がコミットまたは終了するか、トランザクション ロックがタイムアウトするまで、ブロックされます。|  
|SELECT 用に開く。|読み取り用に開く。|どちらも成功します。|どちらも成功します。|  
|SELECT 用に開く。|書き込み用に開く。|どちらも成功します。 トランザクション 2 の書き込み操作は、トランザクション 1 に影響しません。|どちらも成功します。 トランザクション 2 の書き込み操作は、トランザクション 1 に影響しません。|  
|UPDATE または DELETE 用に開く。|読み取り用に開く。|トランザクション 2 の開く操作は、ERROR_SHARING_VIOLATION 例外で失敗します。|どちらも成功します。|  
|UPDATE または DELETE 用に開く。|書き込み用に開く。|トランザクション 2 の開く操作は、ERROR_SHARING_VIOLATION 例外で失敗します。|トランザクション 2 の開く操作は、ERROR_SHARING_VIOLATION 例外で失敗します。|  
|Repeatable Read の SELECT 用に開く。|読み取り用に開く。|どちらも成功します。|どちらも成功します。|  
|Repeatable Read の SELECT 用に開く。|書き込み用に開く。|トランザクション 2 の開く操作は、ERROR_SHARING_VIOLATION 例外で失敗します。|トランザクション 2 の開く操作は、ERROR_SHARING_VIOLATION 例外で失敗します。|  
  
 **リモート クライアントからのライトスルー**  
  
 FILESTREAM データへのリモート ファイル システム アクセスは、サーバー メッセージ ブロック (SMB) プロトコルによって実現されます。 クライアントがリモート クライアントの場合は、書き込み操作がクライアント側でキャッシュされず、 常にサーバーに送信されます。 サーバー側でデータをキャッシュできます。 リモート クライアントで実行されるアプリケーションでは、小さな書き込み操作を統合して、大きなデータ サイズを使用して書き込み操作を減らすことをお勧めします。  
  
 FILESTREAM ハンドルを使用してメモリ マップ表示 (メモリ マップ I/O) を作成することはできません。 FILESTREAM データに対してメモリ マッピングを使用すると、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] でデータの一貫性および持続性やデータベースの整合性を保証できなくなります。  
  
##  <a name="reltasks"></a> 関連タスク  
 [FILESTREAM の有効化と構成](enable-and-configure-filestream.md)  
  [FILESTREAM が有効なデータベースを作成する方法](create-a-filestream-enabled-database.md)  
  [FILESTREAM データを格納するテーブルを作成する方法](create-a-table-for-storing-filestream-data.md)  
  [Transact-SQL による FILESTREAM データへのアクセス](access-filestream-data-with-transact-sql.md)  
  [FILESTREAM データ用のクライアント アプリケーションの作成](create-client-applications-for-filestream-data.md)  
  [OpenSqlFilestream による FILESTREAM データへのアクセス](access-filestream-data-with-opensqlfilestream.md)  
  [FILESTREAM データの部分的な更新](make-partial-updates-to-filestream-data.md)  
  [FILESTREAM アプリケーションでのデータベース操作との競合の回避](avoid-conflicts-with-database-operations-in-filestream-applications.md)  
  [FILESTREAM が有効なデータベースの移動](move-a-filestream-enabled-database.md)  
  [フェールオーバー クラスターでの FILESTREAM の設定](set-up-filestream-on-a-failover-cluster.md)  
  [FILESTREAM アクセスのためのファイアウォールの構成](configure-a-firewall-for-filestream-access.md)  
  
##  <a name="relcontent"></a> 関連コンテンツ  
 [FILESTREAM と SQL Server のその他の機能との互換性](filestream-compatibility-with-other-sql-server-features.md)  
  
