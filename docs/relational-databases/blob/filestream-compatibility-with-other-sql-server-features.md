---
title: FILESTREAM の互換性 | Microsoft Docs
description: FILESTREAM と SQL Server のその他の機能との互換性
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], other SQL Server features and
- FILESTREAM [SQL Server], limitations
ms.assetid: d2c145dc-d49a-4f5b-91e6-89a2b0adb4f3
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c4d32598cfab0cc08ece6721b0ff593c8577394d
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245395"
---
# <a name="filestream-compatibility-with-other-sql-server-features"></a>FILESTREAM と SQL Server のその他の機能との互換性

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  ここでは、FILESTREAM データがファイル システムに存在することに関連して、FILESTREAM を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の次の機能と共に使用する際の注意事項、ガイドライン、および制限事項について説明します。  
  
-   [SQL Server Integration Services (SSIS)](#ssis)  
  
-   [分散クエリおよびリンク サーバー](#distqueries)  
  
-   [暗号化](#encryption)  
  
-   [データベース スナップショット](#DatabaseSnapshot)  
  
-   [レプリケーション](#Replication)  
  
-   [ログ配布](#LogShipping)  
  
-   [データベース ミラーリング](#DatabaseMirroring)  
  
-   [フルテキスト インデックス作成](#FullText)  
  
-   [フェールオーバー クラスタリング](#FailoverClustering)  
  
-   [SQL Server Express](#SQLServerExpress)  
  
-   [包含データベース](#contained)  
  
##  <a name="ssis"></a> SQL Server Integration Services (SSIS)  
 SQL Server Integration Services (SSIS) では、DT_IMAGE SSIS データ型を使用して、他の BLOB データと同様にデータ フローの FILESTREAM データを処理します。  
  
 列インポート変換を使用すると、ファイル システムから FILESTREAM 列にファイルを読み込むことができます。 また、列エクスポート変換を使用すると、FILESTREAM 列からファイル システム内の別の場所にファイルを抽出できます。  
  
##  <a name="distqueries"></a> 分散クエリおよびリンク サーバー  
 FILESTREAM データは、 **varbinary(max)** データとして扱うことにより、分散クエリおよびリンク サーバーを介して利用することができます。 4 部構成の名前を使用する分散クエリでは、FILESTREAM の **PathName()** 関数を使用することはできません。その名前がローカル サーバーを指し示す場合も同様です。 ただし、 **OPENQUERY()** を使用するパススルー クエリの内側のクエリでは **PathName()** を使用できます。  
  
##  <a name="encryption"></a> 暗号化  
 FILESTREAM データは、透過的なデータ暗号化が有効になっている場合でも暗号化されません。  
  
##  <a name="DatabaseSnapshot"></a> データベース スナップショット  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、FILESTREAM ファイル グループの [データベース スナップショット](../../relational-databases/databases/database-snapshots-sql-server.md) をサポートしていません。 CREATE DATABASE ON 句に FILESTREAM ファイル グループが含まれていると、ステートメントが失敗してエラーが発生します。  
  
 FILESTREAM を使用している場合は、標準の (FILESTREAM ファイル グループではない) ファイル グループのデータベース スナップショットを作成できます。 FILESTREAM ファイル グループは、それらのデータベース スナップショットに対してオフラインとしてマークされます。  
  
 データベース スナップショットの FILESTREAM テーブルに対して実行する SELECT ステートメントには、FILESTREAM 列を含めないようにする必要があります。FILESTREAM 列が含まれていると、次のエラー メッセージが返されます。  
  
 `Could not continue scan with NOLOCK due to data movement.`  
  
##  <a name="Replication"></a> Replication  
 パブリッシャーで FILESTREAM 属性が有効になっている **varbinary(max)** 列は、FILESTREAM 属性を含めてサブスクライバーにレプリケートすることも、含めずにレプリケートすることもできます。 列をレプリケートする方法を指定するには、 **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスを使用するか、[sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) または [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) の @schema_option パラメーターを使用します。 FILESTREAM 属性を持たない **varbinary(max)** 列にレプリケートされるデータは、このデータ型の制限 (2 GB) を超えないようにする必要があります。この制限を超えると実行時エラーが発生します。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]にデータをレプリケートする場合以外は、FILESTREAM 属性をレプリケートすることをお勧めします。 指定するスキーマ オプションに関係なく、FILESTREAM 列を含むテーブルを [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] サブスクライバーにレプリケートすることはサポートされていません。  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] から [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] サブスクライバーにレプリケートできるデータ値の大きさは、最大 256 MB に制限されています。 詳細については、「 [最大容量仕様](https://go.microsoft.com/fwlink/?LinkId=103810)」を参照してください。  
  
### <a name="considerations-for-transactional-replication"></a>トランザクション レプリケーションに関する注意点  
 トランザクション レプリケーション用にパブリッシュされるテーブルで FILESTREAM 列を使用する場合は、次のことに注意してください。  
  
-   FILESTREAM 属性を持つ列を含むテーブルがある場合は、[sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) の @sync_method プロパティに対して値 *database snapshot* および *database snapshot character* を使用することはできません。  
  
-   max text repl size オプションは、レプリケーション用にパブリッシュされる列に挿入できるデータの最大サイズを指定します。 このオプションを使用すると、レプリケートされる FILESTREAM データのサイズを制御できます。  
  
-   FILESTREAM 属性をレプリケートするスキーマ オプションを指定しても、FILESTREAM で必要な **uniqueidentifier** 列をフィルターで除外したり、この列の UNIQUE 制約をレプリケートしないように指定したりすると、FILESTREAM 属性はレプリケートされません。 その列は、 **varbinary(max)** 列としてのみレプリケートされます。  
  
### <a name="considerations-for-merge-replication"></a>マージ レプリケーションに関する注意点  
 マージ レプリケーション用にパブリッシュされるテーブルで FILESTREAM 列を使用する場合は、次のことに注意してください。  
  
-   マージ レプリケーションと FILESTREAM では、テーブルの各行を識別するために **uniqueidentifier** データ型の列が必要になります。 マージ レプリケーションでは、この列がテーブルに含まれていなければ自動的に追加されます。 またその列で、ROWGUIDCOL プロパティと、NEWID() または NEWSEQUENTIALID() の既定値が設定されている必要があります。 FILESTREAM ではさらに、この列に対して UNIQUE 制約が定義されている必要もあります。 これらの要件により、次のような結果になります。  
  
    -   既にマージ レプリケーション用にパブリッシュされているテーブルに FILESTREAM 列を追加する場合は、 **uniqueidentifier** 列に UNIQUE 制約があることを確認してください。 UNIQUE 制約がない場合は、パブリケーション データベースのテーブルに名前付き制約を追加します。 既定では、マージ レプリケーションによってこのスキーマ変更がパブリッシュされ、各サブスクリプション データベースに適用されます。  
  
         上の説明に従って手動で UNIQUE 制約を追加した場合は、マージ レプリケーションを削除する際に先に UNIQUE 制約を削除する必要があります。そうしないと、レプリケーションの削除に失敗します。  
  
    -   NEWID() より NEWSEQUENTIALID() の方がパフォーマンスが高いため、マージ レプリケーションでは既定で NEWSEQUENTIALID() が使用されます。 マージ レプリケーション用にパブリッシュされるテーブルに **uniqueidentifier** 列を追加する場合は、NEWSEQUENTIALID() を既定値として指定してください。  
  
-   マージ レプリケーションには、ラージ オブジェクト型のレプリケーションを最適化する機能が含まれています。 この機能は、[sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) の @stream_blob_columns パラメーターによって制御されます。 FILESTREAM 属性をレプリケートするスキーマ オプションを設定すると、@stream_blob_columns パラメーターの値が **true** に設定されます。 この値をオーバーライドするには、 [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)を使用します。 このストアド プロシージャを使用すると、@stream_blob_columns を **false** に設定できます。 既にマージ レプリケーション用にパブリッシュされているテーブルに FILESTREAM 列を追加する場合は、sp_changemergearticle を使用してこのオプションを **true** に設定することをお勧めします。  
  
-   アーティクルが作成された後に FILESTREAM のスキーマ オプションを有効にすると、FILESTREAM 列のデータが 2 GB を超えていて、レプリケーションの間に競合が発生した場合に、レプリケーションが失敗します。 この状況が発生することが予想される場合は、いったんテーブル アーティクルを削除して、適切な FILESTREAM スキーマ オプションを有効にした状態で再作成することをお勧めします。  
  
-   マージ レプリケーションでは、 [Web 同期](../../relational-databases/replication/web-synchronization-for-merge-replication.md)を使用して FILESTREAM データを HTTPS 接続経由で同期させることができます。 その際には、データが Web 同期の制限 (50 MB) に収まっている必要があります。データがこの制限を超えていると、実行時エラーが発生します。  
  
##  <a name="LogShipping"></a> ログ配布  
 [ログ配布](../../database-engine/log-shipping/about-log-shipping-sql-server.md) は FILESTREAM をサポートしています。 プライマリ サーバーとセカンダリ サーバーの両方で [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]以降のバージョンが実行されていて、FILESTREAM が有効になっている必要があります。  
  
##  <a name="DatabaseMirroring"></a> データベース ミラーリング  
 データベース ミラーリングは FILESTREAM をサポートしていません。 プリンシパル サーバー上に FILESTREAM ファイル グループを作成することはできません。 FILESTREAM ファイル グループを含むデータベースに対してデータベース ミラーリングを構成することはできません。  
  
##  <a name="FullText"></a> フルテキスト インデックス作成  
 [フルテキスト インデックス作成](../../relational-databases/search/populate-full-text-indexes.md) では、FILESTREAM 列が **varbinary(max)** 列と同じように処理されます。 FILESTREAM テーブルに、各 FILESTREAM BLOB のファイル名拡張子を含む列が含まれている必要があります。 詳細については、「[フルテキスト検索でのクエリ](../../relational-databases/search/query-with-full-text-search.md)」、「[検索用フィルターの構成と管理](../../relational-databases/search/configure-and-manage-filters-for-search.md)」、および「[sys.fulltext_document_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md)」を参照してください。  
  
 フルテキスト エンジンは、FILESTREAM BLOB の内容のインデックスを作成します。 イメージなど、インデックスを作成しても役に立たないファイルもあります。 FILESTREAM BLOB が更新されると、インデックスが再作成されます。  
  
##  <a name="FailoverClustering"></a> フェールオーバー クラスタリング  
 フェールオーバー クラスタリングでは、FILESTREAM ファイル グループが共有ディスク上に配置されている必要があります。 また、FILESTREAM インスタンスをホストするクラスターの各ノードで FILESTREAM が有効になっている必要もあります。 詳細については、「 [フェールオーバー クラスターでの FILESTREAM の設定](../../relational-databases/blob/set-up-filestream-on-a-failover-cluster.md)」を参照してください。  
  
##  <a name="SQLServerExpress"></a> SQL Server Express  
 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] は FILESTREAM をサポートしています。 FILESTREAM データ コンテナーは 10 GB のデータベース サイズの制限に含まれません。  
  
##  <a name="contained"></a> 包含データベース  
 FILESTREAM 機能では、データベースの外部での構成が一部必要となります。 そのため、FILESTREAM または FileTable を使用するデータベースは完全包含ではありません。  
  
 包含データベースの特定の機能 (包含ユーザーなど) を使用する場合は、データベースの包含を PARTIAL に設定します。 ただし、この場合、一部のデータベース設定はデータベースに含まれないため、データベースを移動するときに自動的には移動されないことに注意してください。  
  
## <a name="see-also"></a>参照  
 [バイナリ ラージ オブジェクト &#40;Blob&#41; データ &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)  
  
  
