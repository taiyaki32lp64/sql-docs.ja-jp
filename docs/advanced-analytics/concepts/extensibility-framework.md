---
title: 機能拡張アーキテクチャ
description: この記事では、SQL Server で R や Python などの外部スクリプトを実行するための機能拡張フレームワークのアーキテクチャについて説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fcdb92f92ffb8239a6cf20b0f39dfb8f546b521a
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727691"
---
# <a name="extensibility-architecture-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services の機能拡張アーキテクチャ 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server は、サーバーで R や Python などの外部スクリプトを実行するための機能拡張フレームワークのアーキテクチャを備えています。 このスクリプトは、言語ランタイム環境でコア データベース エンジンの拡張機能として実行されます。

## <a name="background"></a>背景情報

この機能拡張フレームワークは、R ランタイムをサポートするために SQL Server 2016 で導入されました。 SQL Server 2017 以降では、Python がサポートされています。

機能拡張フレームワークの目的は、SQL Server と、R や Python などのデータ サイエンス言語の間のインターフェイスを提供することです。 データ サイエンス ソリューションを運用環境に移行し、開発プロセス中に無防備になるデータを保護する際に、摩擦を軽減することを目標としています。 SQL Server によって管理される安全なフレームワーク内で信頼できるスクリプト言語を実行することで、データベース管理者は、データ科学者による企業データへのアクセスを許可しながら、セキュリティを維持することができます。

次の図は、拡張可能なアーキテクチャの機会と利点を視覚的に示しています。

  ![SQL Server との統合の目標](../media/ml-service-value-add.png "Machine Learning Services の価値の追加")

外部スクリプトは、ストアド プロシージャを呼び出すことで実行でき、その結果は、表形式の結果として SQL Server に直接返されます。 これにより、SQL クエリを送信して結果を処理できる任意のアプリケーションから、機械学習を簡単に生成または使用できます。

+ 外部スクリプトの実行は、SQL Server のデータ セキュリティの影響を受けます。 外部スクリプトを実行するユーザーは、SQL クエリでも同等に使用できるデータにのみアクセスできます。 権限が不十分であるためにクエリが失敗した場合、同じユーザーが実行するスクリプトも同じ理由で失敗します。 SQL Server セキュリティは、テーブル、データベース、およびインスタンス レベルで適用されます。 データベース管理者は、ユーザー アクセス、外部スクリプトによって使用されるリソース、およびサーバーに追加された外部コード ライブラリを管理できます。  

+ スケールと最適化の機会は、データベース プラットフォームによる利点 (列ストア インデックス、[リソース ガバナンス](../../advanced-analytics/r/resource-governance-for-r-services.md)) と、拡張機能固有の利点 (たとえば、データ サイエンス モデルに R および Python 用の Microsoft ライブラリが使用されている場合) という、2 つの利点を基盤としています。 R はシングルスレッドであるのに対し、RevoScaleR 関数はマルチスレッドであり、ワークロードを複数のコアに分散することができます。

+ 展開では SQL Server 手法が使用されます。 これらには、外部スクリプトをラップしているストアド プロシージャ、埋め込み SQL、または T-SQL クエリ (PREDICT などの関数を呼び出して、サーバーに保持されている予測モデルから結果を返す) が考えられます。

+ 特定のツールや IDE に関するスキルを身に付けている開発者は、これらのツールでコードを記述し、SQL Server にコードを移植することができます。

## <a name="architecture-diagram"></a>アーキテクチャの図

このアーキテクチャは、外部スクリプトが SQL Server とは別のプロセスで実行されるが、コンポーネントによって SQL Server のデータと操作に対する要求のチェーンが内部で管理されるように設計されています。 SQL Server のバージョンに応じて、サポートされている言語拡張機能には、[R](extension-r.md)、[Python](extension-python.md)、および Java や .NET などのサードパーティ言語が含まれます。

  ***Windows のコンポーネント アーキテクチャ:***
  
  ![Windows のコンポーネント アーキテクチャ](../media/generic-architecture-windows.png "コンポーネント アーキテクチャ")
  
  ***Linux のコンポーネント アーキテクチャ:***

  ![Linux のコンポーネント アーキテクチャ](../media/generic-architecture-linux.png "コンポーネント アーキテクチャ")
  
コンポーネントには**スタート パッド** サービスが含まれています。これは、インタープリターとライブラリを読み込むための外部ランタイムおよびライブラリ固有のロジックを呼び出すために使用されます。 ランチャーにより、言語ランタイムと独自のモジュールが読み込まれます。 たとえば、コードに RevoScaleR 関数が含まれている場合、RevoScaleR インタープリターが読み込まれます。 **BxlServer** および **SQL サテライト**により、SQL Server との通信とデータ転送が管理されます。 

Linux の場合、SQL では**スタート パッド** サービスを使用して、ユーザーごとに個別のスタート パッド プロセスとの通信が行われます。

<a name="launchpad"></a>

## <a name="launchpad"></a>スタート パッド

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] は、外部スクリプトを管理および実行するサービスです。これは、フルテキスト インデックス作成とクエリ サービスにより、フルテキスト クエリを処理するための個別のホストを起動するのに似た手法です。 スタート パッド サービスでは、Microsoft によって公開された信頼できるランチャーか、パフォーマンスとリソース管理の要件を満たしているものとして Microsoft に認定されたランチャーのみを起動できます。

| 信頼できるランチャー | 拡張子 | SQL Server のバージョン |
|-------------------|-----------|---------------------|
| Windows 用 R 言語の RLauncher.dll | [R の拡張機能](extension-r.md) | SQL Server 2016 以降 |
| Windows 用 Python 3.5 の Pythonlauncher.dll | [Python の拡張機能](extension-python.md) | SQL Server 2017 以降 |
| Linux 用 R 言語の RLauncher.so | [R の拡張機能](extension-r.md) | SQL Server 2019 以降 |
| Linux 用 Python 3.5 の Pythonlauncher.so | [Python の拡張機能](extension-python.md) | SQL Server 2019 以降 |

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] サービスは、独自のユーザー アカウント下で実行されます。 スタート パッドを実行するアカウントを変更する場合は、必ず SQL Server 構成マネージャーを使用して行い、関連ファイルに変更内容が書き込まれるようにしてください。

Windows では、SQL Server Machine Learning Services を追加したデータベース エンジン インスタンスごとに個別の [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] サービスが作成されます。 データベース エンジン インスタンスごとに 1 つのスタート パッド サービスが存在するため、外部スクリプトをサポートするインスタンスが複数ある場合は、インスタンスごとに 1 つずつスタート パッド サービスが存在します。 データベース エンジン インスタンスは、それに対して作成されたスタート パッド サービスにバインドされます。 ストアド プロシージャまたは T-SQL で外部スクリプトが呼び出されるたびに、SQL Server サービスにより、同じインスタンスに対して作成されたスタート パッド サービスが呼び出されます。

サポートされている特定の言語でタスクを実行するために、スタート パッドにより、セキュリティで保護されたワーカー アカウントがプールから取得され、外部ランタイムを管理するサテライト プロセスが開始されます。 各サテライト プロセスにより、スタート パッドのユーザー アカウントが継承され、スクリプトの実行中にそのワーカー アカウントが使用されます。 スクリプトで並列プロセスが使用される場合、これらのプロセスは 1 つの同じワーカー アカウントで作成されます。

Linux では、1 つのデータベース エンジン インスタンスのみがサポートされ、そのインスタンスにバインドされた launchpadd サービスが 1 つ存在します。 スクリプトが実行されると、launchpadd サービスにより、権限の低いユーザー アカウント **mssql_satellite** を使用して別のスタート パッド プロセスが開始されます。 各サテライト プロセスにより、スタート パッドの mssql_satellite ユーザー アカウントが継承され、スクリプトの実行中にこのアカウントが使用されます。

## <a name="bxlserver-and-sql-satellite"></a>BxlServer と SQL サテライト

**BxlServer** は、SQL Server と言語ランタイムの間の通信を管理する、Microsoft によって提供されている実行可能ファイルです。 これにより、外部スクリプト セッションの格納に使用される Windows ジョブ オブジェクト (Windows の場合) また名前空間 (Linux の場合) が作成されます。 また、外部スクリプト ジョブごとにセキュリティで保護された作業フォルダーが準備され、SQL サテライトを使用して外部ランタイムと SQL Server の間のデータ転送が管理されます。 ジョブの実行中に[プロセス エクスプローラー](https://technet.microsoft.com/sysinternals/processexplorer.aspx)を実行すると、BxlServer の 1 つまたは複数のインスタンスが表示される場合があります。

実際には BxlServer は、SQL Server と連携してデータの転送とタスクの管理を行う言語ランタイム環境に付随するものです。 BXL とは、バイナリ交換言語の略で、SQL Server と外部プロセスの間でデータを効率的に移動するために使用されるデータ形式を指します。 BxlServer は、Microsoft R Client や Microsoft R Server などの関連製品の重要な部分でもあります。

**SQL サテライト**は、データベース エンジンに含まれる機能拡張 API で、C または C++ を使用して実装された外部コードまたは外部ランタイムをサポートしています。

BxlServer は、次のタスクに SQL サテライトを使用します。

+ 入力データの読み取り
+ 出力データの書き込み
+ 入力引数の取得
+ 出力引数の書き込み
+ エラー処理
+ STDOUT と STDERR のクライアントへの書き戻し

SQL サテライトでは、SQL Server と外部スクリプト言語の間の高速データ転送用に最適化されたカスタム データ形式が使用されます。 SQL サテライトによって型変換が実行され、SQL Server と外部スクリプト ランタイムの間の通信時に入力と出力のデータセットのスキーマが定義されます。

SQL サテライトは、Windows 拡張イベント (xEvent) を使用して監視できます。 詳細については、[R の拡張イベント](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)および [Python の拡張イベント](../../advanced-analytics/python/extended-events-for-python.md)に関するページを参照してください。

## <a name="communication-channels-between-components"></a>コンポーネント間の通信チャネル

このセクションでは、コンポーネント間およびデータ プラットフォーム間の通信プロトコルについて説明します。

+ **TCP/IP**

  既定では、SQL Server と SQL サテライトの間の内部通信には TCP/IP が使用されます。

+ **名前付きパイプ**

  SQL サテライトを介した BxlServer と SQL Server の間の内部データ転送では、パフォーマンスを強化するために、専用の圧縮データ形式が使用されます。 データは、名前付きパイプを使用して、言語のランタイムと BxlServer の間で BXL 形式で交換されます。

+ **ODBC**

  外部データ サイエンス クライアントとリモート SQL Server インスタンス間の通信には、ODBC が使用されます。 SQL Server にスクリプト ジョブを送信するアカウントには、インスタンスへの接続権限と、外部スクリプトの実行権限の両方が付与されている必要があります。

  また、タスクによっては、アカウントに次の権限が必要になる場合があります。

  + ジョブによって使用されるデータを読み取る
  + テーブルへのデータの書き込み (たとえば、テーブルに結果を保存する場合)
  + データベース オブジェクトの作成 (たとえば、外部スクリプトを新しいストアド プロシージャの一部として保存する場合)

  SQL Server が、リモート クライアントから実行されるスクリプトの計算コンテキストとして使用され、実行可能ファイルによって外部ソースからデータを取得する必要がある場合は、ODBC が書き戻しに使用されます。 SQL Server により、リモート コマンドを発行しているユーザーの ID が、現在のインスタンス上のユーザーの ID にマップされ、そのユーザーの資格情報を使用して ODBC コマンドが実行されます。 この ODBC 呼び出しを実行するために必要な接続文字列は、クライアント コードから取得されます。

+ **RODBC (R のみ)** 

  追加の ODBC 呼び出しは、**RODBC** を使用してスクリプト内で実行できます。 RODBC は、リレーショナル データベースのデータにアクセスするために使用される、一般的な R パッケージです。ただし、パフォーマンスは SQL Server によって使用される同等のプロバイダーよりも一般的に低速です。 多くの R スクリプトでは、分析に使用する "セカンダリ" データセットを取得するために、RODBC への埋め込み呼び出しが使用されます。 たとえば、モデルをトレーニングするストアド プロシージャでは、モデル トレーニング用のデータを取得するために SQL クエリが定義される場合もありますが、追加要素を取得したり、検索を実行したり、テキスト ファイルや Excel などの外部ソースから新しいデータを取得する場合には、埋め込みの RODBC 呼び出しが使用されます。

  次のコードは、R スクリプトに埋め込まれた RODBC 呼び出しを示したものです。

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **その他のプロトコル**

  "チャンク" で動作するか、またはリモート クライアントにデータを転送する必要のあるプロセスでは、[XDF ファイル形式](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf)も使用できます。 実際のデータ転送は、エンコードされた BLOB を使用して行われます。

## <a name="see-also"></a>参照

+ [SQL Server の R 拡張機能](extension-r.md)
+ [SQL Server の Python 拡張機能](extension-python.md)