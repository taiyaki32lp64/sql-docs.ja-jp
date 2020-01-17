---
title: Integration Services (SSIS) 用の Azure Feature Pack | Microsoft Docs
ms.custom: ''
ms.date: 08/17/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.SSIS.AZURE.F1
- SQL14.SSIS.AZURE.F1
ms.assetid: 31de555f-ae62-4f2f-a6a6-77fea1fa8189
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0e6531e05a3f800bbd4c1563c53c4b4d18eb0eea
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73659588"
---
# <a name="azure-feature-pack-for-integration-services-ssis"></a>Integration Services (SSIS) 用の Azure Feature Pack

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


SQL Server Integration Services (SSIS) Feature Pack for Azure は、このページにリストされている SSIS のコンポーネントを提供して、Azure サービスへの接続、Azure とオンプレミスのデータ ソース間でのデータ転送、および Azure に格納されたデータの処理を行うための拡張機能です。

[![SSIS Feature Pack for Azure のダウンロード](https://docs.microsoft.com/analysis-services/analysis-services/media/download.png)](https://www.microsoft.com/download/details.aspx?id=100430) **ダウンロード**

- SQL Server 2019 の場合 - [Microsoft SQL Server 2019 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=100430)
- SQL Server 2017 の場合 - [Microsoft SQL Server 2017 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=54798)
- SQL Server 2016 の場合 - [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=49492)
- SQL Server 2014 の場合 - [Microsoft SQL Server 2014 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=47366)
- SQL Server 2012 の場合 - [Microsoft SQL Server 2012 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=47367)

ダウンロード ページには、前提条件に関する情報も含まれます。 必ず SQL Server をインストールしてから Azure Feature Pack をサーバーにインストールします。そうしないと、サーバー上の SSIS カタログ データベース (SSISDB) にパッケージを展開するときに Feature Pack 内のコンポーネントを利用できない場合があります。

## <a name="components-in-the-feature-pack"></a>Feature Pack のコンポーネント
-   接続マネージャー

    -   [Azure Data Lake Analytics 接続マネージャー](connection-manager/azure-data-lake-analytics-connection-manager.md)

    -   [Azure Data Lake Store 接続マネージャー](../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)
    
    -   [Azure HDInsight 接続マネージャー](../integration-services/connection-manager/azure-hdinsight-connection-manager.md)

    -   [Azure Resource Manager の接続マネージャー](../integration-services/connection-manager/azure-resource-manager-connection-manager.md)
    
    -   [Azure Storage 接続マネージャー](../integration-services/connection-manager/azure-storage-connection-manager.md)

    -   [Azure サブスクリプション接続マネージャー](../integration-services/connection-manager/azure-subscription-connection-manager.md)
    
-   処理手順

    -   [Azure BLOB のダウンロード タスク](../integration-services/control-flow/azure-blob-download-task.md)

    -   [Azure BLOB のアップロード タスク](../integration-services/control-flow/azure-blob-upload-task.md)

    -   [Azure Data Lake Analytics タスク](control-flow/azure-data-lake-analytics-task.md)

    -   [Azure Data Lake Store ファイル システム タスク](../integration-services/control-flow/azure-data-lake-store-file-system-task.md)

    -   [Azure HDInsight クラスターの作成タスク](../integration-services/control-flow/azure-hdinsight-create-cluster-task.md)

    -   [Azure HDInsight クラスターの削除タスク](../integration-services/control-flow/azure-hdinsight-delete-cluster-task.md)
    
    -   [Azure HDInsight Hive タスク](../integration-services/control-flow/azure-hdinsight-hive-task.md)

    -   [Azure HDInsight Pig タスク](../integration-services/control-flow/azure-hdinsight-pig-task.md)

    -   [Azure SQL DW のアップロード タスク](../integration-services/control-flow/azure-sql-dw-upload-task.md)

    -   [柔軟なファイル タスク](../integration-services/control-flow/flexible-file-task.md)

-   データ フロー コンポーネント

    -   [Azure BLOB Source](../integration-services/data-flow/azure-blob-source.md)

    -   [Azure Blob Destination](../integration-services/data-flow/azure-blob-destination.md)
    
    -   [Azure Data Lake Store Source](../integration-services/data-flow/azure-data-lake-store-source.md)
    
    -   [Azure Data Lake Store Destination](../integration-services/data-flow/azure-data-lake-store-destination.md)

    -   [柔軟なファイル ソース](../integration-services/data-flow/flexible-file-source.md)

    -   [柔軟なファイルの変換先](../integration-services/data-flow/flexible-file-destination.md)

-   Azure BLOB、Azure Data Lake Store、および Data Lake Storage Gen2 のファイル列挙子。 「[Foreach ループ コンテナー](../integration-services/control-flow/foreach-loop-container.md)」を参照してください。

## <a name="use-tls-12"></a>TLS 1.2 を使用する

Azure Feature Pack で使用される TLS のバージョンは、システム .NET Framework 設定に準拠しています。
TLS 1.2 を使用するには、次の 2 つのレジストリキーの下に `SchUseStrongCrypto` という名前の `REG_DWORD` 値をデータ `1` と共に追加します。

1. `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319`
2. `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319`

## <a name="dependency-on-java"></a>Java への依存関係

Azure Data Lake Store/フラット ファイル コネクタで ORC/Parquet ファイル形式を使用するには、Java が必要です。  
Java ビルドのアーキテクチャ (32/64 ビット) は、SSIS ランタイムのそれと一致しなければ使用できません。
次の Java ビルドがテストされています。

- [Zulu の OpenJDK 8u192](https://www.azul.com/downloads/zulu/zulu-windows/)
- [Oracle の Java SE Runtime Environment 8u192](https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8-2177648.html)

### <a name="set-up-zulus-openjdk"></a>Zulu の OpenJDK を設定する

1. インストール zip パッケージをダウンロードし、抽出します。
2. コマンド プロンプトから `sysdm.cpl` を実行します。
3. **[詳細設定]** タブの **[環境変数]** を選択します。
4. **[システム変数]** セクションで **[新規]** を選択します。
5. **[変数名]** に「`JAVA_HOME`」と入力します。
6. **[ディレクトリの参照]** を選択し、解凍したフォルダーに移動し、`jre` サブフォルダーを選択します。
   **[OK]** を選択すると、**変数の値**が自動的に入力されます。
7. **[OK]** を選択し、 **[新しいシステム変数]** ダイアログ ボックスを閉じます。
8. **[OK]** を選択し、 **[環境変数]** ダイアログ ボックスを閉じます。
9. **[OK]** を選択して **[システム プロパティ]** ダイアログ ボックスを閉じます。

### <a name="set-up-zulus-openjdk-on-azure-ssis-integration-runtime"></a>Azure-SSIS Integration Runtime で Zulu の OpenJDK を設定する

これは、Azure-SSIS Integration Runtime の[カスタム セットアップ インターフェイス](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup)経由で行う必要があります。
`zulu8.33.0.1-jdk8.0.192-win_x64.zip` が使用されているとします。
BLOB コンテナーは次のように構成できます。

~~~
main.cmd
install_openjdk.ps1
zulu8.33.0.1-jdk8.0.192-win_x64.zip
~~~

エントリ ポイントとして、`main.cmd` により PowerShell スクリプト `install_openjdk.ps1` の実行がトリガーされます。それによって次に `zulu8.33.0.1-jdk8.0.192-win_x64.zip` が抽出され、それに応じて `JAVA_HOME` が設定されます。

**main.cmd**

~~~
powershell.exe -file install_openjdk.ps1
~~~

**install_openjdk.ps1**

~~~
Expand-Archive zulu8.33.0.1-jdk8.0.192-win_x64.zip -DestinationPath C:\
[Environment]::SetEnvironmentVariable("JAVA_HOME", "C:\zulu8.33.0.1-jdk8.0.192-win_x64\jre", "Machine")
~~~

### <a name="set-up-oracles-java-se-runtime-environment"></a>Oracle の Java SE Runtime Environment を設定する

1. exe インストーラーをダウンロードし、実行します。
2. インストーラーの指示に従い、設定を完了します。

## <a name="scenario-processing-big-data"></a>シナリオ:ビッグ データの処理
 Azure コネクタを使用して、次のビッグ データの処理を完了します。

1.  Azure Blob Upload Task を使用して、入力データを Azure Blob ストレージにアップロードします。

2.  Azure HDInsight Create Cluster Task を使用して、Azure HDInsight のクラスターを作成します。 独自のクラスターを使用する場合は、この手順は省略できます。

3.  Azure HDInsight Hive Task か Azure HDInsight Pig Task を使用して、Azure HDInsight クラスターで Pig または Hive ジョブを呼び出します。

4.  手順 2 でオンデマンドの HDInsight クラスターを作成した場合は、使用後の HDInsight クラスターを Azure HDInsight Delete Cluster Task で削除します。

5.  Azure HDInsight Blob Download Task を使用して、Azure Blob ストレージから Pig/Hive の出力データをダウンロードします。

![SSIS-AzureConnector-BigDataScenario](../integration-services/media/ssis-azureconnector-bigdatascenario.png)
 
## <a name="scenario-managing-data-in-the-cloud"></a>シナリオ:クラウド内のデータ管理
 SSIS パッケージ内の Azure Blob Destination を使用して、出力データを Azure Blob ストレージに書き込みむか、または Azure Blob Source を使用して、Azure Blob ストレージからデータを読み取ります。

![SSIS-AzureConnector-CloudArchive-1](../integration-services/media/ssis-azureconnector-cloudarchive-1.png)
 
 ![SSIS-AzureConnector-CloudArchive-2](../integration-services/media/ssis-azureconnector-cloudarchive-2.png)

 Azure Blob 列挙子とともに Foreach ループ コンテナーを使用して、複数の BLOB ファイルのデータを処理します。

![SSIS-AzureConnector-CloudArchive-3](../integration-services/media/ssis-azureconnector-cloudarchive-3.png)
  
## <a name="release-notes"></a>リリース ノート

### <a name="version-1160"></a>バージョン 1.16.0

#### <a name="bugfixes"></a>バグ修正

1. 場合によっては、パッケージの実行から "エラー:ファイルまたはアセンブリ 'Newtonsoft.Json, Version=11.0.0.0, Culture=neutral, PublicKeyToken=30ad4fe6b2a6aeed'、またはその依存関係の 1 つが読み込むことができませんでした。" が報告されます。

### <a name="version-1150"></a>バージョン 1.15.0

#### <a name="improvements"></a>機能強化

1. 柔軟なファイル タスクに、フォルダー/ファイルの削除操作が追加されます
1. 柔軟なファイル ソースに、外部/出力データ型の変換機能が追加されます

#### <a name="bugfixes"></a>バグ修正

1. 特定のケースで、"配列と互換性のない型の要素にアクセスしようとしました" というエラー メッセージと共に発生する Data Lake Storage Gen2 の接続障害がテストされます
1. Azure ストレージ エミュレーターのサポートが再開されます