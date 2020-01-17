---
title: SQL Server の最大容量仕様 | Microsoft Docs
ms.date: 10/07/2019
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- objects [SQL Server]
- number capacity specifications [SQL Server]
- size [SQL Server], capacity specifications
- number of objects
- capacity specifications [SQL Server]
- maximum capacity specifications [SQL Server]
- size [SQL Server]
- replication capacity specifications [SQL Server]
- objects [SQL Server], capacity specifications
- Database Engine [SQL Server], capacity specifications
ms.assetid: 13e95046-0e76-4604-b561-d1a74dd824d7
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0fae5c47de0b8017d3f374afe18e926eea9818cc
ms.sourcegitcommit: 84e6922a57845a629391067ca4803e8d03e0ab90
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72008437"
---
# <a name="maximum-capacity-specifications-for-sql-server"></a>SQL Server の最大容量仕様
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  次の各表に、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] コンポーネントで定義される各種オブジェクトの最大サイズと最大数を示します。 各 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] テクノロジの表に移動するには、それぞれのリンクをクリックしてください。  
  
 [SQL Server データベース エンジン オブジェクト](#Engine)  
  
 [SQL Server ユーティリティ オブジェクト](#Utility)  
  
 [SQL Server データ層アプリケーション オブジェクト](#DAC)  
  
 [SQL Server レプリケーション オブジェクト](#Replication)  
  
##  <a name="Engine"></a> [!INCLUDE[ssDE](../includes/ssde-md.md)] オブジェクト  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースで定義される各種オブジェクト、または [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントで参照される各種オブジェクトの最大サイズと最大数。  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] オブジェクト (object)||最大サイズ/最大数 ( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 64 ビットの場合)|追加情報|  
|---------------------------------------------------------|-|------------------------------------------------------------------|----------------------------|  
|[バッチ サイズ]||65,536 * ネットワーク パケット サイズ|ネットワーク パケット サイズとは、アプリケーションとリレーショナル [!INCLUDE[ssDE](../includes/ssde-md.md)]の間の通信に使用される表形式データ ストリーム (TDS) パケットのサイズです。 既定のパケット サイズは 4 KB であり、network packet size 構成オプションによって制御されます。|  
|通常の string 列ごとのバイト数||8,000||  
|GROUP BY、ORDER BY ごとのバイト数||8,060||  
|インデックス キーごとのバイト数||1 つのクラスター化インデックスにつき 900 バイト。 1 つの非クラスター化インデックスにつき 1,700 バイト。|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]では、クラスター化インデックス キーの最大バイト数を 900 以下にする必要があります。 非クラスター化インデックス キーの場合は、最大 1,700 バイト。<br /><br /> 最大サイズを合計すると制限を超える可変長列を使用して、キーを定義できます。 ただし、これらの列のデータのサイズ合計が、制限を超えることはできません。<br /><br /> 非クラスター化インデックスには、追加の非キー列を含めることができ、それらはキーのサイズ制限にはカウントされません。 非キー列は、一部のクエリ パフォーマンスの向上に役立つ場合があります。|  
|メモリ最適化テーブルのインデックス キーごとのバイト数||1 つの非クラスター化インデックスにつき 2,500 バイト。 すべてのインデックス キーが行内に収まる限り、ハッシュ インデックスに制限はなし。|メモリ最適化テーブルでは、非クラスター化インデックスは、宣言された最大サイズが 2,500 バイトを超えるキー列を持つことはできません。 キー列の実際のデータが、宣言されている最大サイズよりも小さいかどうかには関係ありません。<br /><br /> ハッシュ インデックス キーの場合、サイズにハード リミットはありません。<br /><br /> メモリ最適化テーブルのインデックスの場合、すべてのインデックスがすべての列を本質的にカバーするため、付加列の概念はありません。<br /><br /> メモリ最適化テーブルの場合、行のサイズが 8,060 バイトでも、一部の可変長列をこの 8,060 バイトの外側に物理的に保存できます。 ただし、テーブルのすべてのインデックスのすべてのキー列の宣言された最大サイズと、テーブル内の追加の固定長列のすべてが、8,060 バイトに収まる必要があります。|  
|外部キーごとのバイト数||900||  
|主キーごとのバイト数||900||  
|行ごとのバイト数||8,060|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 行オーバーフロー ストレージがサポートされています。これにより、可変長列の行外への移動が可能になります。 行外に移動される可変長列のうち、ルートの 24 バイトだけが本体のレコードに格納されます。これにより、実際の行制限は、以前のリリースの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]よりも大きい値になります。 詳細については、[大量の行のサポート](../relational-databases/pages-and-extents-architecture-guide.md#large-row-support)に関する記事を参照してください。|  
|メモリ最適化テーブル内の行ごとのバイト数||8,060|[!INCLUDE[ssSQL15](../includes/sssql15-md.md)] から、メモリ最適化テーブルで行外ストレージがサポートされます。 テーブル内のすべての列の最大サイズが 8,060 バイトを超える場合、可変長列が行外に押し出されます。コンパイル時の決定です。 行外に保存された列用に、8 バイトの参照だけが行内に保存されます。 詳細については、「 [メモリ最適化テーブルのテーブルと行のサイズ](../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)」を参照してください。|  
|ストアド プロシージャのソース テキスト内のバイト数||バッチ サイズまたは 250 MB のいずれか小さい方||  
|**varchar (max)** 、 **varbinary (max)** 、 **xml**、 **テキスト**、または **イメージ** あたりのバイト数||2^31-1||  
|**ntext** または **nvarchar (max)** あたりの文字数||2^30-1||  
|テーブルごとのクラスター化インデックス数||1||  
|GROUP BY、ORDER BY の列数||バイト数のみによって制限されます。||  
|GROUP BY WITH CUBE または WITH ROLLUP ステートメント内の列または式の数||10||  
|インデックス キーごとの列数||32|テーブルに 1 つ以上の XML インデックスが含まれている場合は、XML 列がプライマリ XML インデックスのクラスター化キーに追加されるため、ユーザー テーブルのクラスター化キーが 31 列までに制限されます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]では、キー列数が最大キー列数制限の 32 を越えないように、非クラスター化インデックスに非キー列を含めることができます。 詳細については、「 [付加列インデックスの作成](../relational-databases/indexes/create-indexes-with-included-columns.md)」を参照してください。|  
|外部キーまたは主キーごとの列数||32||  
|`INSERT` ステートメントごとの列数||4,096||  
|`SELECT` ステートメントごとの列数||4,096||  
|テーブルごとの列数||1,024|スパース列セットを含むテーブルには、最大 30,000 列が含まれます。 「[スパース列セット](../relational-databases/tables/use-column-sets.md)」を参照してください。|  
|`UPDATE` ステートメントごとの列数||4,096|[スパース列セット](../relational-databases/tables/use-column-sets.md)には、異なる制限が適用されます。|  
|ビューごとの列数||1,024||  
|クライアントごとの接続数||構成した接続の最大値||  
|データベース サイズ||524,272 テラバイト||  
|インスタンスごとのデータベース数 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]||32,767||  
|データベースごとのファイル グループ数||32,767||  
|メモリ最適化データに対応する、データベースごとのファイル グループ||1||  
|データベースごとのファイル数||32,767||  
|ファイル サイズ (データ)||16 テラバイト||  
|ファイル サイズ (ログ)||2 テラバイト||  
|データベースごとのメモリ最適化データに対応するデータ ファイル||[!INCLUDE[ssSQL14](../includes/ssSQL14-md.md)] では 4,096。 それより後のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] には、このような厳密な制限はありません。||  
|メモリ最適化データに対応するデータ ファイルごとのデルタ ファイル||1||  
|テーブルごとの外部キー テーブル参照数||発信 = 253。 着信 = 10,000。|制限については、「 [Create Foreign Key Relationships](../relational-databases/tables/create-foreign-key-relationships.md)」を参照してください。|  
|識別子長 (文字数)||128||  
|コンピューターごとのインスタンス数||スタンドアロン サーバー上に 50 個のインスタンス。<br /><br /> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、クラスター インストールのストレージ オプションとして共有クラスター ディスクを使用する場合、フェールオーバー クラスター上に 25 個のインスタンスがサポートされます。クラスター インストールのストレージ オプションとして SMB ファイル共有を選択する場合は、フェールオーバー クラスター上に 50 個のインスタンスがサポートされます。||  
|メモリ最適化テーブルごとのインデックス||[!INCLUDE[ssSQL17](../includes/ssSQL17-md.md)] 以降および [!INCLUDE[ssSDSFull](../includes/ssSDSFull-md.md)] では 999<br/>[!INCLUDE[ssSQL14](../includes/ssSQL14-md.md)] および [!INCLUDE[ssSQL15](../includes/ssSQL15-md.md)] では 8||  
|SQL ステートメントが含まれた文字列の長さ (バッチ サイズ)||65,536 * ネットワーク パケット サイズ|ネットワーク パケット サイズとは、アプリケーションとリレーショナル [!INCLUDE[ssDE](../includes/ssde-md.md)]の間の通信に使用される表形式データ ストリーム (TDS) パケットのサイズです。 既定のパケット サイズは 4 KB であり、network packet size 構成オプションによって制御されます。|  
|接続ごとのロック数||サーバーごとの最大ロック数||  
|のインスタンスごとのロック数 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]||メモリのみによって制限されます。|これは静的ロック割り当てに対する値です。 動的ロックの場合は、メモリのみによって制限されます。|  
|ストアド プロシージャの入れ子レベル数||32|ストアド プロシージャが 65 個以上のデータベースにアクセスするか、またはインターリーブ時に 3 つ以上のデータベースにアクセスすると、エラーが返されます。|  
|入れ子にしたサブクエリの数||32||    
|入れ子構造のトランザクション||4,294,967,296||     
|トリガーの入れ子レベル数||32||  
|テーブルごとの非クラスター化インデックス数||999||  
|次のいずれかが存在する場合の、GROUP BY 句に含まれる個別の式の数:CUBE、ROLLUP、GROUPING SETS、WITH CUBE、WITH ROLLUP||32||  
|GROUP BY 句内の演算子によって生成されるグループ化セットの数||4,096||  
|ストアド プロシージャごとのパラメーター数||2,100||  
|ユーザー定義関数ごとのパラメーター数||2,100||  
|テーブルごとの参照数||253||  
|テーブルごとの行数||使用可能な記憶領域によって制限されます。||  
|データベースごとのテーブル数||データベース内のオブジェクト数によって制限されます。|データベース オブジェクトには、テーブル、ビュー、ストアド プロシージャ、ユーザー定義関数、トリガー、ルール、デフォルト、制約などのオブジェクトが含まれます。 1 つのデータベース内のオブジェクトの合計数は 2,147,483,647 以下にする必要があります。|  
|パーティション テーブルまたはインデックスごとのパーティション数||15,000||  
|インデックス付けされていない列の統計||30,000|| 
|SELECT ステートメントごとのテーブル数||使用可能なリソースのみによって制限されます。||  
|テーブルごとのトリガー数||データベース内のオブジェクト数によって制限されます。|データベース オブジェクトには、テーブル、ビュー、ストアド プロシージャ、ユーザー定義関数、トリガー、ルール、デフォルト、制約などのオブジェクトが含まれます。 1 つのデータベース内のオブジェクトの合計数は 2,147,483,647 以下にする必要があります。|  
|ユーザー接続数||32,767||  
|XML インデックス数||249||  
  
##  <a name="Utility"></a> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティ オブジェクト  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティでテストされた各種オブジェクトの最大サイズと最大数。  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティ オブジェクト||最大サイズ/最大数 ( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 64 ビットの場合)|  
|----------------------------------------------|-|------------------------------------------------------------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティごとのコンピューター数 (物理コンピューターまたは仮想マシン)||100|  
|コンピューターごとの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンス数||5|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティごとの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンス総数||200*|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のインスタンス (データ層アプリケーションを含む) ごとのユーザー データベース数||50|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティごとのユーザー データベース総数||1,000|  
|データベースごとのファイル グループ数||1|  
|ファイル グループごとのデータ ファイル数||1|  
|データベースごとのログ ファイル数||1|  
|コンピューターごとのボリューム数||3|  
  
 \* [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティでサポートされる [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のマネージド インスタンスの最大数は、サーバーのハードウェア構成によって異なる場合があります。 概要情報については、「 [SQL Server ユーティリティの機能とタスク](../relational-databases/manage/sql-server-utility-features-and-tasks.md)」を参照してください。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ユーティリティ コントロール ポイントは、 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]のすべてのエディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](https://msdn.microsoft.com/library/cc645993.aspx)」を参照してください。    
  
##  <a name="DAC"></a> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データ層アプリケーション オブジェクト  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データ層アプリケーション (DAC) でテストされた各種オブジェクトの最大サイズと最大数。  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] DAC オブジェクト||最大サイズ/最大数 ( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 64 ビットの場合)|  
|------------------------------------------|-|------------------------------------------------------------------|  
|DAC ごとのデータベース数||1|  
|DAC ごとのオブジェクト数*||データベース内のオブジェクト数または使用可能なメモリによって制限されます。|  
  
 *制限の対象となるオブジェクトの種類は、ユーザー、テーブル、ビュー、ストアド プロシージャ、ユーザー定義関数、ユーザー定義データ型、データベース ロール、スキーマ、およびユーザー定義テーブル型です。  
  
##  <a name="Replication"></a> レプリケーション オブジェクト  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] レプリケーションで定義される各種オブジェクトの最大サイズと最大数。  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] レプリケーション オブジェクト||最大サイズ/最大数 (SQL Server 64 ビットの場合)|  
|--------------------------------------------------|-|---------------------------------------------------|  
|アーティクル数 (マージ パブリケーション)||2048|  
|アーティクル数 (スナップショットまたはトランザクション パブリケーション)||32,767|  
|テーブル内の列数* (マージ パブリケーション)||246|  
|テーブル内の列数** ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のスナップショットまたはトランザクション パブリケーション)||1,000|  
|テーブル内の列数** (Oracle のスナップショットまたはトランザクション パブリケーション)||995|  
|行フィルターで使用される列のバイト数 (マージ パブリケーション)||1,024|  
|行フィルターで使用される列のバイト数 (スナップショットまたはトランザクション パブリケーション)||8,000|  

 *行レベルの追跡を使用して競合を検出する場合 (既定値)、ベース テーブルには最大 1,024 列含めることができますが、最大 246 列がパブリッシュされるようにアーティクルから列をフィルター選択する必要があります。 列の追跡を使用する場合、ベース テーブルには最大 246 列を含めることができます。  
  
 **ベース テーブルには、パブリケーション データベースで許容される最大数 ( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の場合は 1,024) の列を含めることができますが、列数がパブリケーション タイプに対して指定された最大数を超える場合は、アーティクルから列をフィルター選択する必要があります。  
  
## <a name="see-also"></a>参照  
 [SQL Server 2016 のインストールに必要なハードウェアおよびソフトウェア](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [システム構成チェッカーの検査パラメーター](../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)   
 [SQL Server ユーティリティの機能とタスク](../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
