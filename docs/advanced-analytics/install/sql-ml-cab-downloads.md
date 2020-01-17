---
title: オフライン インストール用の更新プログラムをダウンロードする
description: SQL Server Machine Learning Services と SQL Server 2016 R Services 用の R および Python CAB とパッケージ ファイルをダウンロードします。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e7266d90e04071c242145fc0df2e59ce86d86a16
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727628"
---
# <a name="cab-downloads-for-cumulative-updates-of-sql-server-in-database-analytics-instances"></a>SQL Server データベース内分析インスタンスの累積的な更新プログラムの CAB ダウンロード

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

データベース内分析用に構成されている SQL Server インスタンスには、R と Python の機能があります。 これらの機能は CAB ファイルに付属し、SQL Server セットアップを通じてインストールされて提供されます。 インターネットに接続されているデバイスでは、CAB の更新プログラムは通常、Windows Update によって適用されます。 接続されていないサーバーの場合、CAB ファイルを手動でダウンロードして適用する必要があります。 

この記事では、累積的な更新プログラムごとの CAB ファイルのダウンロード リンクを示します。 オフライン インストールの詳細については、[インターネットへのアクセスなしで SQL Server 機械学習コンポーネントをインストールする](sql-ml-component-install-without-internet-access.md#apply-cu)に関するページを参照してください。

## <a name="prerequisites"></a>Prerequisites

ベースライン インストールから開始します。

+ SQL Server Machine Learning Services では、最初のリリースがベースライン インストールです。 
+ SQL Server 2016 R Services では、最初のリリース、SP1、または SP2 から始めることができます。 

また、スタンドアロン サーバーに累積的な更新プログラムを適用することもできます。

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

## <a name="sql-server-2017-cabs"></a>SQL Server 2017 CAB

CAB ファイルは、新しい順で一覧表示されます。 CAB ファイルをダウンロードしてターゲット コンピューターに転送する場合、**Downloads** フォルダーやセットアップ ユーザーの %temp% フォルダーなどの便利なフォルダーにファイルを配置します。

|リリース  |コンポーネント | ダウンロード リンク  | 対処された問題 | 
|---------|----------|----------------|------------------|
|**[SQL Server 2017 CU14](https://support.microsoft.com/help/4484710/)-[CU15](https://support.microsoft.com/help/4498951/)-[CU16](https://support.microsoft.com/help/4508218/)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073898&clcid=1033)| パッケージ内のバイナリが署名されました。 |
| | R Server      |[SRS_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2069739&clcid=1033)| パッケージ内のバイナリが署名されました。 |
| | Microsoft Python Open     | [SPO_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073897&clcid=1033)| パッケージ内のバイナリが署名されました。 |
| | Python サーバー    |[SPS_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2071421&clcid=1033)| パッケージ内のバイナリが署名されました。  |
|**[SQL Server 2017 CU13](https://support.microsoft.com/help/4466404)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 以前のバージョンからの変更はありません。 |
| | R Server      |[SRS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038263&clcid=1033)| SQL Server セットアップを使用してインストールされた、[操作に対応したスタンドアロン R Server](https://docs.microsoft.com/machine-learning-server/what-is-operationalization) をアップグレードするための修正プログラムが含まれています。 CU13 CAB を使用し、[こちらの手順](sql-machine-learning-standalone-windows-install.md#apply-cu)に従って更新プログラムを適用します。 |
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 以前のバージョンからの変更はありません。 |
| | Python サーバー    |[SPS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038197&clcid=1033)| SQL Server セットアップを使用してインストールされた、[操作に対応したスタンドアロン Python Server](https://docs.microsoft.com/machine-learning-server/what-is-operationalization) をアップグレードするための修正プログラムが含まれています。 CU13 CAB を使用し、[こちらの手順](sql-machine-learning-standalone-windows-install.md#apply-cu)に従って更新プログラムを適用します。 |
|**[SQL Server 2017 CU10](https://support.microsoft.com/help/4342123)-[CU11](https://support.microsoft.com/help/4462262)-[CU12](https://support.microsoft.com/help/4464082)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 以前のバージョンからの変更はありません。 |
| | R Server      |[SRS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006287&clcid=1033)| 小さな修正。|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 以前のバージョンからの変更はありません。 |
| | Python サーバー    |[SPS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006805&clcid=1033)| 重複が削除されると、Python rx_data_step では行の順序が失われます。 <br/>SPEE は、クラスター化列ストア インデックスでのデータ型検出に失敗します。 <br/>列にすべて null 値が含まれている場合は、空のテーブルを返します。 |
|**[SQL Server 2017 CU8](https://support.microsoft.com/help/4338363)-[CU9](https://support.microsoft.com/help/4341265)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 以前のバージョンからの変更はありません。 |
| | R Server      |[SRS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874708&clcid=1033)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 以前のバージョンからの変更はありません。 |
| | Python サーバー    |[SPS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874707&clcid=1033)|
|**[SQL Server 2017 CU6](https://support.microsoft.com/help/4101464)-[CU7](https://support.microsoft.com/help/4229789)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 以前のバージョンからの変更はありません。 |
| | R Server      |[SRS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871074&clcid=1033)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 以前のバージョンからの変更はありません。 |
| | Python サーバー    |[SPS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871073&clcid=1033)| SPEES クエリの DateTime データ型。<br/>トレーニング済みのモデルがない場合の microsoftml でのエラー メッセージが改善されました。<br/> revoscalepy 変換関数と変数が修正されました。|
|**[SQL Server 2017 CU5](https://support.microsoft.com/help/4092643)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 以前のバージョンからの変更はありません。 |
| | R Server      |[SRS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869052&clcid=1033)| rxInstallPackages の長いパスに関連するエラー。<br/>RxExec のループバックでの接続。
| | Microsoft Python Open    | 以前のバージョンからの変更はありません。 |
| | Python サーバー    |[SPS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869053&clcid=1033)| <br/>rx_exec のループバックでの接続。
|**[SQL Server 2017 CU4](https://support.microsoft.com/help/4056498)** |  |   |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 以前のバージョンからの変更はありません。 |
| | R Server      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 以前のバージョンからの変更はありません。 |
| |  Python サーバー    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|
|**[SQL Server 2017 CU3](https://support.microsoft.com/help/4052987)** |  |  |  |
| | Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
| | R Server      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 以前のバージョンからの変更はありません。 |
| | Python サーバー    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)| [rx_serialize_model 関数](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)を使用した、revoscalepy での Python モデルのシリアル化。<br/>[ネイティブのスコアリング](../sql-native-scoring.md)のサポートに加えて、[リアルタイム スコアリング](../real-time-scoring.md)の機能強化が行われました。 
|**[SQL Server 2017 CU1](https://support.microsoft.com/help/4038634)-[CU2](https://support.microsoft.com/help/4052574)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)| 以前のバージョンからの変更はありません。 |
| | R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 以前のバージョンからの変更はありません。 | 
| | Python サーバー    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) | スキーマ情報を返すための rx_create_col_info を追加します。 <br/>`RxLocalParallel` コンピューティング コンテキストを使用した並列シナリオをサポートする [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) の機能強化。|
|**最初のリリース** |  |  |
| | Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
| | R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
| | Python サーバー    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

::: moniker-end

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"

<a name="bkmk_2016Installers"></a>

## <a name="sql-server-2016-cabs"></a>SQL Server 2016 CAB

SQL Server 2016 R Services では、ベースライン リリースは RTM バージョンまたは Service Pack バージョンのいずれかになります。

|リリース  |ダウンロード リンク  |
|---------|---------------|
|**SQL Server 2016 SP2 CU6**     |
|Microsoft R Open     |[SRO_3.2.2.20100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079936&clcid=1033)|
|Microsoft R Server    |[SRS_8.0.3.20100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079933&clcid=1033)|
|**SQL Server 2016 SP2 CU1-CU5**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R Server    |[SRS_8.0.3.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866038)|
|**SQL Server 2016 SP2**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R Server    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)|
|**SQL Server 2016 SP1 CU14**     |
|Microsoft R Open     |[SRO_3.2.2.16100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2080130&clcid=1033)|
|Microsoft R Server    |[SRS_8.0.3.17200_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079935&clcid=1033)|
|**SQL Server 2016 SP1 CU1-CU13**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R Server    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
|**SQL Server 2016 SP1**     |
|Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)|
|Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)|
|**SQL Server 2016 CU4-CU9**     |
|Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
|Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
|**SQL Server 2016 CU2-CU3**     |
|Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)|
|Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)|
|**SQL Server 2016 CU1**     |
|Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)|
|Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)|
|**SQL Server 2016 RTM**     |
|Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)|
|Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)|

> [!NOTE]
> 
> SQL Server 2016 SP1 CU4 または SP1 CU5 をオフラインでインストールする場合は、SRO_3.2.2.16000_1033.cab をダウンロードします。 セットアップ ダイアログ ボックスに示されているように、FWLINK 831785 から SRO_3.2.2.13000_1033.cab をダウンロードした場合は、累積的な更新プログラムをインストールする前に、ファイルの名前を SRO_3.2.2.16000_1033.cab に変更します。

Microsoft R のソース コードを表示する場合は、次のように tar 形式のアーカイブとしてダウンロードできます。[R Server インストーラーのダウンロード](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows#download)

::: moniker-end

## <a name="next-steps"></a>次の手順

[インターネットにアクセスしないコンピューターに累積的な更新プログラムを適用する](sql-ml-component-install-without-internet-access.md#apply-cu)

[インターネットに接続できるコンピューターに累積的な更新プログラムを適用する](sql-ml-component-install-without-internet-access.md#apply-cu)

[スタンドアロン サーバーに累積的な更新プログラムを適用する](sql-machine-learning-standalone-windows-install.md#apply-cu)
