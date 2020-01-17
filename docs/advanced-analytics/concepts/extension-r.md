---
title: R 言語拡張機能
description: SQL Server R Services または SQL Server Machine Learning Services での R コードの実行と組み込み R ライブラリについて学習します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 98ef57702b01a3f32babd6b0ac9b64fb3c22e9ea
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727661"
---
# <a name="r-language-extension-in-sql-server"></a>SQL Server の R 言語拡張機能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

R 拡張機能は、リレーショナル データベース エンジンに対する SQL Server Machine Learning Services アドオンの一部です。 これにより、R 実行環境、標準ライブラリとツールを使用した基本の R ディストリビューション、Microsoft R ライブラリ (大規模な分析用の [RevoScaleR](../r/ref-r-revoscaler.md)、機械学習アルゴリズム用の [MicrosoftML](../r/ref-r-microsoftml.md)、SQL Server のデータまたは R コードにアクセスするためのその他のライブラリ) が追加されます。

R 統合は、[SQL Server R Services](../r/sql-server-r-services.md) と [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) で使用できます。

## <a name="r-components"></a>R コンポーネント

SQL Server には、オープンソース パッケージと専用パッケージの両方が含まれています。 基本の R ライブラリは、Microsoft のオープンソース R のディストリビューションによってインストールされます (Microsoft R Open (MRO))。 R の現在のユーザーは、R コードを移植し、ほとんどまたはまったく変更することなく、SQL Server 上の外部プロセスとしてそれを実行できます。 MRO は、SQL ツールとは別にインストールされ、機能拡張フレームワークのコア エンジン プロセスの外部で実行されます。 インストール中に、オープンソース ライセンスの条項に同意する必要があります。 その後、R の他のオープンソース ディストリビューションと同じように、標準 R パッケージを変更することなく実行できます。 

SQL Server では、基本の R 実行可能ファイルは変更されませんが、セットアップによってインストールされたバージョンの R を使用する必要があります。これは、専用パッケージがビルドおよびテストされているバージョンであるためです。 CRAN から取得する可能性のある R の基本ディストリビューションと MRO の違いについては、[R 言語との相互運用性と Microsoft R 製品と機能](https://docs.microsoft.com/r-server/what-is-r-server-interoperability)に関するページを参照してください。

セットアップでインストールされた R 基本パッケージのディストリビューションは、インスタンスに関連付けられているフォルダーで見つけることができます。 たとえば、既定の SQL Server インスタンスに R Services をインストールした場合、R ライブラリは既定のこのフォルダー `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library` に配置されます。 同様に、既定のインスタンスに関連付けられている R ツールは、既定でこのフォルダー `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin` に配置されます。

Microsoft によって並列ワークロードと分散ワークロードに追加される R パッケージには、次のライブラリが含まれます。

| ライブラリ | [説明] |
|---------|-------------|
| [**RevoScaleR**](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | データ ソース オブジェクトとデータの探索、操作、変換、視覚化をサポートします。 リモート コンピューティング コンテキスト、およびさまざまなスケーラブルな機械学習モデル (**rxLinMod** など) の作成をサポートします。 これらの API は、大きすぎてメモリに収まらないデータ セットの分析と複数のコアまたはプロセッサでの分散計算を実行するように最適化されています。 RevoScaleR パッケージでは、分析のために使用されるデータの高速移動と格納用の XDF ファイル形式もサポートします。 XDF 形式は、カラム型ストレージを使用する移植可能な形式であり、テキスト、SPSS、ODBC 接続などのさまざまなソースからデータを読み込んで操作するために使用できます。 |
| [**MicrosoftML**](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package) | 速度と精度のために最適化された機械学習アルゴリズムに加え、テキストとイメージを操作するためのインライン変換も含まれています。 詳細については、[SQL Server の MicrosoftML](../r/ref-r-microsoftml.md) に関するページを参照してください。 | 

## <a name="using-r-in-sql-server"></a>SQL Server での R の使用

基本関数を使用して R のスクリプトを作成できますが、マルチプロセッシングを利用するには、**RevoScaleR** モジュールと **MicrosoftML** モジュールを R コードにインポートしてから、その関数を呼び出して並列に実行されるモデルを作成する必要があります。 
 
サポートされているデータ ソースには、ODBC データベース、SQL Server、他のソースまたは R ソリューションとデータを交換するための XDF ファイル形式があります。 入力データは、表形式である必要があります。 R 結果はすべて、データ フレームの形式で返される必要があります。

サポートされているコンピューティング コンテキストには、ローカルまたはリモートの SQL Server コンピューティング コンテキストが含まれます。 リモート コンピューティング コンテキストとは、ワークステーションなどの 1 台のコンピューターで起動するコード実行を指しますが、その後、スクリプトの実行はリモート コンピューターに切り替えられます。 コンピューティング コンテキストを切り替えるには、両方のシステムに同じ RevoScaleR ライブラリが用意されている必要があります。

ご想像のとおり、ローカルのコンピューティング コンテキストには、データベース エンジン インスタンスと同じサーバー上での R コードの実行に加え、T-SQL 内のコードまたはストアド プロシージャに埋め込まれたコードの実行も含まれます。 また、リモートのコンピューティング コンテキストを定義することにより、ローカルの R IDE からコードを実行し、SQL Server コンピューター上でスクリプトを実行することもできます。

## <a name="execution-architecture"></a>アーキテクチャの実行

以下の図は、サポートされている各シナリオでの SQL Server コンポーネントと R ランタイムとのやりとりを示しています。そのシナリオとは、SQL Server コンピューティング コンテキストを使用したデータベース内のスクリプトの実行と R コマンド ラインからのリモート実行です。

### <a name="r-scripts-executed-from-sql-server-in-database"></a>SQL Server (データベース内) から実行された R スクリプト

"内部" SQL Server から実行される R コードは、ストアド プロシージャを呼び出して実行されます。 したがって、R コードの実行は、ストアド プロシージャを呼び出す任意のアプリケーションによって開始できます。  その後は、SQL Server により、次の図にまとめたように、R コードの実行が管理されます。

![rsql_indb780-01](../r/media/script_in-db-r.png)

1. ストアド プロシージャ ([sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)) に渡されたパラメーター _@language='R'_ によって、R ランタイムに対する要求が示されます。 この要求は SQL Server からスタート パッド サービスに送信されます。
Linux の場合、SQL では**スタート パッド** サービスを使用して、ユーザーごとに個別のスタート パッド プロセスとの通信が行われます。 詳細については、[機能拡張アーキテクチャの図](extensibility-framework.md#architecture-diagram)を参照してください。
2. スタート パッド サービスによって、適切なランチャーが起動されます (この場合は RLauncher)。
3. RLauncher が外部の R プロセスを起動します。
4. BxlServer と R ランタイムとの連携により、SQL Server とのデータ交換や、作業結果の保存が管理されます。
5. SQL サテライトでは、関連するタスクやプロセスについての SQL Server との通信が管理されます。
6. BxlServer では、SQL サテライトを使用して、状態と結果が SQL Server に通知されます。
7. SQL Server では、結果が取得され、関連するタスクとプロセスが終了されます。

### <a name="r-scripts-executed-from-a-remote-client"></a>リモート クライアントから実行された R スクリプト

Microsoft R をサポートするリモート データ サイエンス クライアントから接続している場合には、RevoScaleR 関数を使用して、R 関数を SQL Server のコンテキストで実行できます。 これは、上記のワークフローとは異なるものです。次の図に概要を示します。

![rsql_fromR2db-01](../r/media/remote-sqlcc-from-r2.png)

1. RevoScaleR 関数の場合、R ランタイムでリンク関数を呼び出し、それによって BxlServer を呼び出します。
2. BxlServer は Microsoft R と共に提供されているもので、R ランタイムとは別個のプロセスで実行されます。
3. BxlServer は接続のターゲットを決定し、ODBC を使用して接続を開始して、R データ ソース オブジェクト内の接続文字列の一部として提供された資格情報を渡します。
4. BxlServer によって、SQL Server インスタンスへの接続が開かれます。
5. R 呼び出しの場合は、スタート パッド サービスが起動され、それによって適切なランチャー (RLauncher) が起動されます。 その後の R コードの処理は、T-SQL から R コードを実行する場合のプロセスと同様です。
6. RLauncher により、SQL Server コンピューターにインストールされている R ランタイムのインスタンスへの呼び出しを行います。
7. 結果が BxlServer に返されます。
8. SQL サテライトでは、SQL Server との通信と、関連するジョブ オブジェクトのクリーンアップが管理されます。
9. SQL Server からクライアントに結果が返されます。

## <a name="see-also"></a>参照

+ [SQL Server の機能拡張フレームワーク](extensibility-framework.md)
+ [SQL Server の Python および機械学習拡張機能](extension-python.md)