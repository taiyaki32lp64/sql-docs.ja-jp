---
title: 新機能
description: MPP SQL Server Parallel Data Warehouse をホストするスケールアウトオンプレミスアプライアンスである Microsoft Analytics Platform System の新機能について説明します。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3845470668e4cffeda7a48ed01c144eb53f671b9
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399420"
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>スケールアウト MPP データウェアハウスである Analytics Platform System の新機能
Microsoft Analytics Platform System (APS) の最新のアプライアンス更新プログラムの新機能を参照してください。 APS は、MPP SQL Server 並列データウェアハウスをホストする、スケールアウトされたオンプレミスのアプライアンスです。 

::: moniker range=">= aps-pdw-2016-au7 || = sqlallproducts-allversions"
<a name="h2-aps-cu7.5"></a>
## <a name="aps-cu75"></a>APS CU7.5
リリース日-2019 年9月

### <a name="alter-external-data-source"></a>外部データソースの変更
お客様は、CU 7.5 更新プログラムを使用して外部データソース定義を変更することができます。 Hadoop 名前ノードの高可用性を使用しているお客様は、フェールオーバーが発生したときに、データソースを変更して引数を変更できるようになりました。 APS の場合、場所、RESOURCE_MANAGER_LOCATION、資格情報のみを変更できます。 詳細については、「 [alter external data source](https://docs.microsoft.com/sql/t-sql/statements/alter-external-data-source-transact-sql?view=sql-server-2017) 」を参照してください。

### <a name="cdh-515-and-516-support-with-polybase"></a>CDH 5.15 と5.16 の PolyBase のサポート
CU 7.5 update を使用する APS の PolyBase では、Cloudera からの、CDH 5.15 および5.16 バージョンの Hadoop 配布がサポートされるようになりました。 CDH 5.x バージョンにはオプション6を使用します。 

### <a name="try_convert-and-try_cast-support"></a>Try_Convert と Try_Cast のサポート
CU 7.5 APS では、 [TRY_CAST](https://docs.microsoft.com/sql/t-sql/functions/try-cast-transact-sql?view=sql-server-2017)および[TRY_CONVERT](https://docs.microsoft.com/sql/t-sql/functions/try-convert-transact-sql?view=sql-server-2017) tsql 関数がサポートされるようになりました。 これらの関数は、変換が成功した場合に、指定したデータ型に変換された値を返します。それ以外の場合は null を返します。

<a name="h2-aps-cu7.4"></a>
## <a name="aps-cu74"></a>APS CU7.4
リリース日-2019 年5月

### <a name="loading-large-rows-with-dwloader"></a>Dwloader を使用した大きな行の読み込み
APS CU 7.4 以降では、新しい dwloader を使用して、32 KB (32768 バイト) を超えるテーブルに行を読み込むことができます。 新しい dwloader は、32768 ~ 33554432 (バイト単位) の整数値を受け取る-l スイッチをサポートしています。これにより、32 KB を超える行が読み込まれます。 このスイッチによってクライアントとサーバーにより多くのメモリが割り当てられ、負荷が低下する可能性があるため、このオプションは、大きい行 (32 KB を超える) を読み込む場合にのみ使用してください。 新しい dwloader は[ダウンロードサイト](https://www.microsoft.com/download/details.aspx?id=57472)からダウンロードできます。  

### <a name="hdp-30-and-31-support-with-polybase"></a>PolyBase を使用した HDP 3.0 と3.1 のサポート
APS の PolyBase は、この更新で HDP 3.0 および3.1 をサポートするようになりました。 HDP 3.x バージョンにはオプション7を使用します。 詳細については、「 [PolyBase connectivity](https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql) 」ページを参照してください。

### <a name="utf16-file-support-with-polybase"></a>PolyBase を使用した UTF16 ファイルのサポート
PolyBase は、UTF16 (LE) エンコード形式の区切られたテキストファイルの読み取りをサポートするようになりました。 詳細については、「セットアップの[外部ファイル形式を作成](https://docs.microsoft.com/sql/t-sql/statements/create-external-file-format-transact-sql)する」を参照してください。 

<a name="h2-aps-cu7.3"></a>
## <a name="aps-cu73"></a>APS CU7.3
リリース日-2018 年12月

### <a name="common-subexpression-elimination"></a>共通部分式の削除
APS CU 7.3 では、SQL クエリオプティマイザーにおける共通部分式の削除によって、クエリのパフォーマンスが向上します。 改善により、2つの方法でクエリが向上します。 1つ目の利点は、このような式を特定して削除することで、SQL のコンパイル時間を短縮できることです。 2つ目の重要な利点は、これらの冗長な部分式に対するデータ移動操作が不要になるため、クエリの実行時間が短縮されます。 この機能の詳細については、[こちら](common-sub-expression-elimination.md)を参照してください。

### <a name="aps-informatica-connector-for-informatica-1020-published"></a>Informatica 10.2.0 公開された APS Informatica connector
Informatica バージョン10.2.0 および10.2.0 修正プログラム1で動作する APS 用の Informatica コネクタの新しいバージョンをリリースしました。 新しいコネクタは、[ダウンロードサイト](https://www.microsoft.com/download/details.aspx?id=57472)からダウンロードできます。

#### <a name="supported-versions"></a>サポートされているバージョン

| APS バージョン | Informatica PowerCenter | ドライバー |
|:---|:---|:---|
| APS 2016 | 9.6.1 | SQL Server Native Client 2.x |
| APS 2016 以降 | 10.2.0、10.2.0 Hotfix 1 | SQL Server Native Client 2.x |

<a name="h2-aps-cu7.2"></a>
## <a name="aps-cu72"></a>APS CU7.2
リリース日-2018 年10月

### <a name="support-for-tls-12"></a>TLS 1.2 のサポート
APS CU 7.2 は、TLS 1.2 をサポートしています。 クライアントコンピューターから APS への通信と、TLS 1.2 経由でのみ通信を行うように設定できるようになりました。 TLS 1.2 経由でのみ通信するように設定されているクライアントコンピューターにインストールされている SSDT、SSIS、Dwloader などのツールは、TLS 1.2 を使用して APS に接続できるようになりました。 既定では、AP は旧バージョンとの互換性のために、すべての TLS (1.0、1.1、および 1.2) バージョンをサポートします。 TLS 1.2 を厳密に使用するように APS アプライアンスを設定する場合は、レジストリ設定を変更します。 

詳細については、「 [APS での tls 1.2 の構成](configure-tls12-aps.md)」を参照してください。

### <a name="hadoop-encryption-zone-support-for-polybase"></a>PolyBase の Hadoop 暗号化ゾーンのサポート
PolyBase が Hadoop 暗号化ゾーンと通信できるようになりました。 「 [Hadoop のセキュリティを構成する](polybase-configure-hadoop-security.md#encryptionzone)」で必要な APS 構成の変更を参照してください。

### <a name="insert-select-maxdop-options"></a>挿入-maxdop オプションを選択する
挿入選択操作に対して1を超える maxdop 設定を選択できる[機能スイッチ](appliance-feature-switch.md)が追加されました。 Maxdop 設定を0、1、2、または4に設定できるようになりました。 既定値は 1 です。

> [!IMPORTANT]  
> Maxdop を増やすと、操作やデッドロックエラーが発生することがあります。 その場合は、設定を maxdop 1 に戻してから、操作を再試行してください。

### <a name="columnstore-index-health-dmv"></a>列ストアインデックスの正常性 DMV
**Dm_pdw_nodes_db_column_store_row_group_physical_stats** dmv を使用して、列ストアインデックスの正常性に関する情報を表示できます。 断片化を確認し、列ストアインデックスを再構築または再構成するタイミングを決定するには、次のビューを使用します。

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[pdw_node_id]    = nt.[pdw_node_id]                                          
)
select *
from cte;
```

### <a name="polybase-date-range-increase-for-orc-and-parquet-files"></a>ORC および Parquet ファイルの PolyBase 日付範囲の増加
PolyBase を使用した日付データ型の読み取り、インポート、およびエクスポートでは、1970-01-01 より前の日付と ORC および Parquet ファイルの種類の2038-01-20 以降がサポートされるようになりました。

### <a name="ssis-destination-adapter-for-sql-server-2017-as-target"></a>ターゲットとして SQL Server 2017 の SSIS 変換先アダプター
SQL Server 2017 をサポートする新しい APS SSIS 変換先アダプター (展開ターゲットは[ダウンロードサイト](https://www.microsoft.com/download/details.aspx?id=57472)からダウンロードできます)。

<a name="h2-aps-cu7.1"></a>
## <a name="aps-cu71"></a>APS CU7.1
リリース日-2018 年7月

### <a name="dbcc-commands-do-not-consume-concurrency-slots-behavior-change"></a>DBCC コマンドは同時実行スロットを使用しません (動作の変更)
APS は、 [DBCC DROPCLEANBUFFERS](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql)などの t-sql [dbcc コマンド](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-transact-sql)のサブセットをサポートしています。 以前は、これらのコマンドは[コンカレンシー スロット](https://docs.microsoft.com/sql/analytics-platform-system/workload-management?view=aps-pdw-2016-au7#concurrency-slots)を消費したので、実行できるユーザー負荷/クエリの数が減少しました。 `DBCC`コマンドは、ユーザーの同時実行スロットを使用しないローカルキューで実行されるようになりました。これにより、全体的なクエリ実行パフォーマンスが向上します。

### <a name="replaces-some-metadata-calls-with-catalog-objects"></a>一部のメタデータ呼び出しをカタログオブジェクトに置き換えます。
SMO を使用する代わりに、メタデータ呼び出しに catalog オブジェクトを使用すると、APS のパフォーマンスが向上しています。 CU 7.1 以降、これらのメタデータ呼び出しの一部では、既定でカタログオブジェクトが使用されるようになりました。 メタデータクエリを使用しているお客様が問題が発生した場合は、[機能スイッチ](appliance-feature-switch.md)でこの動作を無効にすることができます。

### <a name="bug-fixes"></a>バグ修正
APS CU 7.1 で SQL Server 2016 SP2 CU2 にアップグレードしました。 このアップグレードでは、以下に示すいくつかの問題が修正されます。

| タイトル | 説明 |
|:---|:---|
| **考えられる組ムーバーのデッドロック** |このアップグレードでは、分散トランザクションと組ムーバーのバックグラウンドスレッドでデッドロックが発生する可能性があることを修正しました。 CU 7.1 をインストールした後、TF634 を使用してタプルムーバーを停止すると SQL Server スタートアップパラメーターまたはグローバルトレースフラグとして削除できます。 | 
| **特定のラグ/リードクエリが失敗する** |遅延/リード関数が入れ子になっている CCI テーブルに対する特定のクエリは、このアップグレードによって修正されました。 | 


<a name="h2-aps-au7"></a>
## <a name="aps-au7"></a>APS AU7
リリース日-2018 年5月

APS 2016 は、AU7 にアップグレードするための前提条件です。 APS AU7 の新機能は次のとおりです。

### <a name="auto-create-and-auto-update-statistics"></a>統計の自動作成と自動更新
既定では、APS AU7 によって統計が自動的に作成および更新されます。 統計設定を更新するために、管理者は[Configuration Manager](appliance-configuration.md#CMTasks)の新しい機能の切り替えメニュー項目を使用できます。 [機能スイッチ](appliance-feature-switch.md)は、統計の自動作成、自動更新、および非同期更新の動作を制御します。 また、 [ALTER database (Parallel Data Warehouse)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)ステートメントを使用して、統計設定を更新することもできます。

### <a name="t-sql"></a>T-SQL
Select @varがサポートされるようになりました。 詳細については、「 [select local variable](/sql/t-sql/language-elements/select-local-variable-transact-sql) 」を参照してください。 

クエリヒントのハッシュと順序グループがサポートされるようになりました。 詳細については、「[ヒント (transact-sql)-Query](/sql/t-sql/queries/hints-transact-sql-query) 」を参照してください。

### <a name="feature-switch"></a>機能スイッチ
APS AU7 には[Configuration Manager](launch-the-configuration-manager.md)の機能スイッチが導入されています。 AutoStatsEnabled と DmsProcessStopMessageTimeoutInSeconds は、管理者が変更できる構成可能なオプションになりました。

### <a name="known-issues"></a>の既知の問題
APS AU7 ソフトウェアでは、Intel BIOS の更新プログラムが提供されており、予測*実行のサイドチャネル攻撃*として説明されている問題を修正します。 攻撃は、 *Spectre と Meltdown の脆弱性*と呼ばれるものを悪用することを目的としています。 APS と共にパッケージ化されますが、BIOS の更新プログラムは、APS AU7 ソフトウェアのインストールの一部としてではなく、手動でインストールされます。

Microsoft は、すべてのお客様に BIOS の更新をインストールするようにアドバイスします。 Microsoft は、さまざまな環境におけるさまざまな SQL ワークロードに対して、カーネル仮想アドレスシャドウ (KVAS)、カーネルページテーブル間接 (中 TI)、および間接分岐予測軽減 (IBP) の影響を測定しました。 この測定では、一部のワークロードで大幅な低下が見られました。 結果に基づいて、BIOS 更新を有効にした場合のパフォーマンスへの影響をテストしてから、運用環境に展開することをお勧めします。 SQL Server ガイダンスを参照し[てください。](https://support.microsoft.com/help/4073225/guidance-protect-sql-server-against-spectre-meltdown)

::: moniker-end
::: moniker range=">= aps-pdw-2016 || = sqlallproducts-allversions"
<a name="h2-aps-au6"></a>
## <a name="aps-2016"></a>APS 2016
このセクションでは、APS 2016-AU6 の新機能について説明します。

### <a name="sql-server-2016"></a>SQL Server 2016

APS AU6 は、最新の SQL Server 2016 リリースで実行され、既定のデータベース互換性レベル130を使用します。 SQL Server 2016 では、次のような新機能がサポートされるようになります。

- クラスター化列ストアインデックスのセカンダリインデックス。
- PolyBase の Kerberos。

### <a name="t-sql"></a>T-SQL
APS AU6 では、これらの T-sql 互換性の向上がサポートされています。  これらの追加の言語要素を使用すると、SQL Server およびその他のデータソースからの移行が容易になります。 

- Windows 照合順序に加えて、[列レベルの SQL 照合順序][]がサポートされるようになりました。
- クラスター化[列ストアインデックスの非クラスター化インデックス][]は、クラスター化列ストアインデックス内の特定の値を検索するクエリのパフォーマンスを向上させます。 
- [選択...ドラッグ][] 
- [sp_spaceused ()][]は、テーブルまたはデータベースで使用されているか予約されているディスク領域を表示します。
- [幅の広いテーブル][]のサポートは SQL Server 2016 と同じです。 以前の行サイズに対する 32 K の制限は存在しません。 

**データの種類**

- [VARCHAR (max)][]、 [NVARCHAR (max)][] 、および[VARBINARY (max)][]です。 これらの LOB データ型の最大サイズは 2 GB です。 これらのオブジェクトを読み込むには、 [Bcp ユーティリティ][]を使用します。 PolyBase と dwloader では、現在、これらのデータ型はサポートされていません。 
- [SYSNAME][]
- [一意][]
- [NUMERIC][]および DECIMAL データ型。

**ウィンドウ関数**

- SELECT ステートメントの OVER 句の[行または範囲][]。
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

**セキュリティ関数**

- [CHECKSUM ()][]と[BINARY_CHECKSUM ()][]
- [HAS_PERMS_BY_NAME ()][]

**その他の関数**

- [NEWID ()][]
- [RAND ()][]

### <a name="polybasehadoop-enhancements"></a>PolyBase/Hadoop の機能強化

- Hortonworks HDP 2.4 および HDP 2.5 との互換性
- データベーススコープの資格情報を使用した Kerberos のサポート
- Azure Storage Blob を使用した資格情報のサポート

### <a name="install-and-upgrade-enhancements"></a>インストールとアップグレードの機能強化

**エンタープライズアーキテクチャの更新**既存のアプライアンスを APS AU6 にアップグレードすると、最新のファームウェアとドライバーの更新プログラムがインストールされます。これには、セキュリティ修正が含まれます。 

HPE または DELL の新しいアプライアンスには、最新の更新プログラムがすべて含まれています。

- 最新世代プロセッサのサポート (Broadwell)
- DDR4 Dimm への更新
- DIMM スループットの向上

**結合**

- 完全修飾ドメイン名 (FQDN) のサポートにより、アプライアンスに対するドメインの信頼を設定できます。 
- FQDN を使用するには、アップグレード中に完全なアップグレードとオプトインを行う必要があります。 

**ダウンタイムの短縮**APS AU6 のインストールまたはアップグレードには時間がかかり、以前のリリースよりもダウンタイムが少なくて済みます。 ダウンタイムを短縮するには、次のようにインストールまたはアップグレードします。 

 - 2016年6月までのすべての更新プログラムを含むイメージを使用して、WSUS の更新プログラムの適用を効率化します。
 - ドライバーとファームウェアの更新プログラムを使用してセキュリティ更新プログラムを適用する
 - では、最新の修正プログラムとアプライアンス検証ユーティリティ (PAV) がアプライアンスに配置されるので、インストールする準備ができています。ダウンロードする必要はありません。

::: moniker-end

<!--
Link references to other articles in this same GitHub repo.

The link format that starts with '/sql/what-ever/my-artlcle' is not appropriate for common links within the same repo (as most of these link are).  The first couple links have been edited to show the proper syntax, but all other links in this article need to be similarly edited.
The proper formats have at least two big advantages.  One big advantage is that the proper formats enable the OPS Build system to detect broken links at Pull Request build time, instead of only later during run time.
-->
[database compatibility level 130]: ../t-sql/statements/alter-database-transact-sql-compatibility-level.md
[列レベルの SQL 照合順序]: ~/relational-databases/collations/collation-and-unicode-support.md

[クラスター化列ストアインデックスの非クラスター化インデックス]:/sql/t-sql/statements/create-index-transact-sql
[VARCHAR (MAX)]:/sql/t-sql/data-types/char-and-varchar-transact-sql
[NVARCHAR (MAX)]:/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql
[VARBINARY (MAX)]:/sql/t-sql/data-types/binary-and-varbinary-transact-sql
[SYSNAME]:/sql/relational-databases/system-catalog-views/sys-types-transact-sql
[選択...ドラッグ]:/sql/t-sql/queries/select-into-clause-transact-sql
[sp_spaceused ()]:/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql
[幅の広いテーブル]:/sql/sql-server/maximum-capacity-specifications-for-sql-server
[BULK INSERT]:/sql/t-sql/statements/bulk-insert-transact-sql
[bcp ユーティリティ]:/sql/tools/bcp-utility
[一意]:/sql/t-sql/data-types/uniqueidentifier-transact-sql
[番号]:/sql/t-sql/data-types/decimal-and-numeric-transact-sql
[行または範囲]:/sql/t-sql/queries/select-over-clause-transact-sql
[FIRST_VALUE]:/sql/t-sql/functions/first-value-transact-sql
[LAST_VALUE]:/sql/t-sql/functions/last-value-transact-sql
[CUME_DIST]:/sql/t-sql/functions/cume-dist-transact-sql
[PERCENT_RANK]:/sql/t-sql/functions/percent-rank-transact-sql
[CHECKSUM ()]:/sql/t-sql/functions/checksum-transact-sql
[BINARY_CHECKSUM ()]:/sql/t-sql/functions/binary-checksum-transact-sql
[HAS_PERMS_BY_NAME ()]:/sql/t-sql/functions/has-perms-by-name-transact-sql
[NEWID ()]:/sql/t-sql/functions/newid-transact-sql
[RAND ()]:/sql/t-sql/functions/rand-transact-sql


  

  


