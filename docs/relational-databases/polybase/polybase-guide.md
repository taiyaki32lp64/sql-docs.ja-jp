---
title: PolyBase とは | Microsoft Docs
ms.date: 06/10/2019
ms.prod: sql
ms.technology: polybase
ms.topic: overview
f1_keywords:
- PolyBase
- PolyBase, guide
helpviewer_keywords:
- PolyBase
- PolyBase, overview
- Hadoop import
- Hadoop export
- Hadoop export, PolyBase overview
- Hadoop import, PolyBase overview
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions||>=aps-pdw-2016||=azure-sqldw-latest'
ms.openlocfilehash: 7e9e09cece42b84e5fa9691aa0d353d2ed22431b
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710580"
---
# <a name="what-is-polybase"></a>PolyBase とは

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]

<!--SQL Server 2016/2017-->
::: moniker range="= sql-server-2016 || = sql-server-2017 || >= aps-pdw-2016 || = azure-sqldw-latest"

PolyBase を使用すると、SQL Server 2016 インスタンスで Hadoop からデータを読み取る Transact-SQL クエリを処理できるようになります。 同じクエリで SQL Server のリレーショナル テーブルにアクセスすることもできます。 また、PolyBase では、同じクエリで Hadoop と SQL Server のデータを結合させることもできます。 SQL Server では、[外部テーブル](../../t-sql/statements/create-external-table-transact-sql.md)または[外部データ ソース](../../t-sql/statements/create-external-data-source-transact-sql.md)によって Hadoop と接続します。

![PolyBase 論理](../../relational-databases/polybase/media/polybase-logical.png "PolyBase 論理")

PolyBase では、クエリ全体を最適化するために計算の一部が Hadoop ノードにプッシュされます。 しかし、PolyBase の外部アクセスは Hadoop だけではありません。 その他の構造化されていない非リレーショナル テーブルもサポートしています (区切られたテキスト ファイルなど)。

> [!TIP]
> SQL Server 2019 では、SQL Server、Oracle、Teradata、および MongoDB を含む新しい PolyBase 用のコネクタが導入されています。 詳細については、[ SQL Server 2019 用の PolyBase のドキュメント](polybase-guide.md?view=sql-server-ver15)に関するページを参照してください。

::: moniker-end
<!--SQL Server 2019-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

PolyBase を使用すると、外部データ ソースからデータを読み取る Transact-SQL クエリを SQL Server インスタンスで処理できるようになります。 SQL Server 2016 以降は、Hadoop と Azure Blob Storage 内の外部データにアクセスできます。 SQL Server 2019 以降、PolyBase を使用して、[SQL Server](polybase-configure-sql-server.md)、[Oracle](polybase-configure-oracle.md)、[Teradata](polybase-configure-teradata.md)、および [MongoDB](polybase-configure-mongodb.md) 内の外部データにアクセスできるようになりました。

外部データにアクセスするのと同じクエリでは、SQL Server インスタンス内のリレーショナル テーブルを対象にすることもできます。 これにより、外部ソースのデータとデータベース内の高価値のリレーショナル データを組み合わせることができます。 SQL Server では、[外部テーブル](../../t-sql/statements/create-external-table-transact-sql.md)または[外部データ ソース](../../t-sql/statements/create-external-data-source-transact-sql.md)によって Hadoop と接続します。

PolyBase では、クエリ全体を最適化するために計算の一部が Hadoop ノードにプッシュされます。 しかし、PolyBase の外部アクセスは Hadoop だけではありません。 その他の構造化されていない非リレーショナル テーブルもサポートしています (区切られたテキスト ファイルなど)。

::: moniker-end

### <a name="supported-sql-products-and-services"></a>サポートされる SQL 製品とサービス

PolyBase では、次の Microsoft の SQL 製品にこれらと同じ機能を提供します。

- SQL Server 2016 以降のバージョン (Windows のみ)
- Analytics Platform System (旧称 Parallel Data Warehouse)
- Azure SQL Data Warehouse

### <a name="azure-integration"></a>Azure との統合

下層 の PolyBase のサポートにより、T-SQL クエリでは Azure Blob Storage のデータをインポートおよびエクスポートすることもできます。 さらに、PolyBase によって、Azure SQL Data Warehouse で Azure Data Lake Store および Azure Blob Storage のデータをインポートおよびエクスポートできるようになります。

## <a name="why-use-polybase"></a>PolyBase を使用する理由

SQL Server のデータを外部データと結合することは、以前はもっと困難でした。 次の好ましくないオプションのどちらかを選択する必要がありました。

- すべてのデータをどちらか一方の形式に統一するために、片方のデータを転送する。
- 両方のデータのソースに対してクエリを実行した後、クライアント レベルでデータを結合および統合するためにカスタムのクエリ ロジックを記述する。

PolyBase では T-SQL を使用してデータを結合するので、これらの好ましくないオプションは不要になります。

シンプルさを保つため、Hadoop 環境に追加のソフトウェアをインストールしなくても PolyBase を使用することができます。 外部データを照会するには、データベース テーブルの照会に使用したのと同じ T-SQL 構文を使用します。 PolyBase が実装する補助的なアクションは、すべて透過的に実行されます。 クエリの作成者に Hadoop の知識は必要ありません。

### <a name="polybase-uses"></a>PolyBase の使用

PolyBase を使用すると、SQL Server で次のシナリオに対応できます。

- **SQL Server または PDW から Hadoop に格納されたデータのクエリを実行する。** ユーザーは、たとえば Hadoop など、コスト効果の高いスケーラブルな分散システムにデータを格納しています。 PolyBase を使用すると、T-SQL で簡単にデータを照会できます。

- **Azure Blob Storage に格納されたデータのクエリを実行する。** Azure BLOB ストレージは、Azure サービスによって使用されるデータを格納するのに便利な場所です。  PolyBase を使用すると、T-SQL で簡単にデータにアクセスできます。

- **Hadoop、Azure Blob Storage、Azure Data Lake Store からデータをインポートする。** Hadoop、Azure Blob Storage、または Azure Data Lake Store からリレーショナル テーブルにデータをインポートすることで、Microsoft SQL の高速な列ストア テクノロジおよび分析機能を活用できます。 ETL ツールやインポート ツールを個別に用意する必要はありません。

- **Hadoop、Azure BLOB ストレージ、Azure Data Lake Store にデータをエクスポートする。** データを Hadoop、Azure BLOB ストレージ、Azure Data Lake Store にアーカイブすることで、コスト効果の高いストレージを実現し、アクセスしやすいようにそのストレージをオンライン状態にしておくことができます。

- **BI ツールと統合する。** PolyBase を Microsoft のビジネス インテリジェンスや分析スタックと一緒に使用したり、SQL Server と互換性のあるサード パーティ ツールを使用したりすることができます。

## <a name="performance"></a>パフォーマンス

- **Hadoop に計算をプッシュする。** クエリ オプティマイザーはコスト ベースの決定を行い、クエリのパフォーマンスが向上する場合は Hadoop に計算をプッシュします。  コスト ベースの決定には、外部テーブルの統計が使用されます。 計算のプッシュでは、MapReduce ジョブが作成され、Hadoop の分散コンピューティング リソースが活用されます。

- **コンピューティング リソースをスケーリングする。** クエリのパフォーマンスを向上させるために、SQL Server [PolyBase スケールアウト グループ](../../relational-databases/polybase/polybase-scale-out-groups.md)を使用できます。 これにより、SQL Server インスタンスと Hadoop ノードの間の並列データ転送が可能になります。また、外部データに対する操作のためのコンピューティング リソースが追加されます。

<!--SQL Server 2016/2017-->
::: moniker range="=sql-server-2016||=sql-server-2017"

## <a name="next-steps"></a>次の手順

PolyBase を使用する前に [PolyBase 機能をインストールする](polybase-installation.md)必要があります。 その後、使用するデータ ソースに応じて、次の構成ガイドを参照してください。

- [Hadoop](polybase-configure-hadoop.md)
- [Azure Blob Storage](polybase-configure-azure-blob-storage.md)

::: moniker-end
<!--SQL Server 2019-->
::: moniker range=">= sql-server-linux-ver15||>= sql-server-ver15||=sqlallproducts-allversions"

## <a name="next-steps"></a>次の手順

PolyBase を使用する前に [PolyBase 機能をインストールする](polybase-installation.md)必要があります。 その後、使用するデータ ソースに応じて、次の構成ガイドを参照してください。
- [Hadoop](polybase-configure-hadoop.md)
- [Azure Blob Storage](polybase-configure-azure-blob-storage.md)
- [SQL Server](polybase-configure-sql-server.md)
- [Oracle](polybase-configure-oracle.md)
- [Teradata](polybase-configure-teradata.md)
- [MongoDB](polybase-configure-mongodb.md)
- [ODBC ジェネリック型](polybase-configure-odbc-generic.md)

::: moniker-end
