---
title: マスター インスタンスとは
titleSuffix: SQL Server big data clusters
description: この記事では、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]の SQL Server マスター インスタンスについて説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 42e16066a08c0b30fd8b43eaf481525c4f510b80
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652274"
---
# <a name="what-is-the-master-instance-in-a-sql-server-big-data-cluster"></a>SQL Server ビッグ データ クラスターのマスター インスタンスとは

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

この記事では、SQL Server 2019 ビッグ データ クラスターでの *SQL Server マスター インスタンス*の役割について説明します。 マスター インスタンスとは、ビッグ データ クラスターで実行される、接続、スケールアウト クエリ、メタデータとユーザー データベース、機械学習サービスを管理する SQL Server のインスタンスです。

SQL Server マスター インスタンスには、次の機能があります。

## <a name="connectivity"></a>接続

SQL Server マスター インスタンスにより、クラスターに対して、外部からアクセスできる TDS エンドポイントが提供されます。 他の SQL Server インスタンスと同様に、アプリケーションまたは Azure Data Studio や SQL Server Management Studio などの SQL Server ツールをこのエンドポイントに接続できます。

## <a name="scale-out-query-management"></a>クエリの管理をスケールアウトする

SQL Server マスター インスタンスには、[コンピューティング プール](concept-compute-pool.md)内のノード上の SQL Server インスタンス間でクエリを分散するために使用されるスケールアウト クエリ エンジンが含まれています。 スケールアウト クエリ エンジンでは、追加の構成を行わずに、Transact-SQL を使用してクラスター内のすべての Hive テーブルにアクセスすることもできます。

## <a name="metadata-and-user-databases"></a>メタデータとユーザー データベース

SQL マスター インスタンスには、標準の SQL Server システム データベースに加えて、次のものも含まれます。

- HDFS テーブルのメタデータを格納するメタデータ データベース
- データ プレーンのシャード マップ
- クラスター データ プレーンへのアクセスを提供する外部テーブルの詳細情報
- ユーザー データベースで定義されている PolyBase 外部データ ソースと外部テーブル

また、独自のユーザー データベースを SQL Server マスター インスタンスに追加することもできます。

## <a name="machine-learning-services"></a>Machine Learning Services

SQL Server Machine Learning Services は、SQL Server で Java、R、および Python コードを実行するために使用される、データベース エンジンのアドオン機能です。 この機能は SQL Server 機能拡張フレームワークに基づいています。これにより、外部プロセスがコア エンジン プロセスから分離されますが、ストアド プロシージャとして、R または Python ステートメントを含む T-SQL スクリプトとして、あるいは、T-SQL を含む Java、R、または Python コードとして、リレーショナル データと完全に統合されます。

Machine Learning Services は、SQL Server ビッグ データ クラスターの一部として既定により SQL Server マスター インスタンス上で使用できるようになります。 つまり、SQL Server マスター インスタンス上で外部スクリプトの実行が有効になると、sp_execute_external_script を使用して Java、R、Python スクリプトを実行できるようになります。

### <a name="advantages-of-machine-learning-services-in-a-big-data-cluster"></a>ビッグ データ クラスターでの Machine Learning Services の利点

SQL Server 2019 を使用すると、通常はエンタープライズ データベースに格納されているディメンション データにビッグ データを簡単に結合できます。 ビッグ データの価値は、組織の一部で管理されているだけでなく、レポート、ダッシュボード、アプリケーションに取り込むことも行われた場合に、大幅に増加します。 同時に、データ科学者は引き続き Spark/HDFS エコシステム ツールを使用して、SQL Server マスター インスタンス内のデータと、SQL Server マスター インスタンスを "_経由して_" アクセス可能な外部データ ソースに、リアルタイムで簡単にアクセスできます。

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]を使用すると、エンタープライズ データ レイクでさらに多くのことを行うことができます。 SQL Server 開発者とアナリストは次のことができます。

* エンタープライズ データ レイクにあるデータを消費するアプリケーションを構築する。
* Transact-SQL クエリを使用して、すべてのデータについて推論する。
* SQL Server のツールとアプリケーションからなる既存のエコシステムを使用して、エンタープライズ データにアクセスして分析する。
* データの仮想化とデータ マートにより、データ移動の必要性を削減する。
* ビッグ データのシナリオ用に引き続き Spark を使用する。
* Spark または SQL Server を使用してインテリジェントなエンタープライズ アプリケーションを構築し、データ レイクでモデルをトレーニングする。
* 最適なパフォーマンスを得るために、実稼働データベースでモデルを運用化する。
* リアルタイム分析のために、エンタープライズ データ マートにデータを直接ストリーミングする。
* 対話型分析と BI ツールを使用して、データを視覚的に探索する。

## <a name="next-steps"></a>次の手順

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] の詳細については、次のリソースを参照してください。

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)
- [ワークショップ: Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] アーキテクチャ](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
