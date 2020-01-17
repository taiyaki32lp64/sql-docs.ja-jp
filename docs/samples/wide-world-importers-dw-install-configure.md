---
title: DW WideWorldImporters サンプルデータベースのインストール & 構成
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: d8768fec2f96c725a9ba4bbf91996e95de4c800a
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056302"
---
# <a name="wideworldimportersdw-installation-and-configuration"></a>WideWorldImportersDW のインストールと構成
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
WideWorldImportersDW データベースのインストールと構成の手順。

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) (またはそれ以降) または[Azure SQL Database](https://azure.microsoft.com/services/sql-database/)。 このサンプルの完全バージョンを使用するには、SQL Server Evaluation/Developer/Enterprise Edition を使用します。
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。 最善の結果を得るには、2016 年 6 月リリース以降を使用してください。

## <a name="download"></a>ダウンロード

サンプルの最新リリース:

[wide-world-importers-release](https://go.microsoft.com/fwlink/?LinkID=800630)

SQL Server または Azure SQL データベースのエディションに対応するサンプル WideWorldImportersDW データベースのバックアップ/bacpac をダウンロードしてください。

サンプル データベースを再作成するソース コードは、以下の場所から使用可能です。 データ カタログの作成は、OLTP データベース (WideWorldImporters) から ETL に基づいていることに注意してください。

[wide-world-importers-source](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-dw-database-scripts)

## <a name="install"></a>インストール


### <a name="sql-server"></a>SQL Server

バックアップを SQL Server インスタンスに復元するには、Management Studio を使用できます。

1. SQL Server Management Studio を開き、ターゲットの SQL Server インスタンスに接続します。
2. **データベース**ノードを右クリックし、**Restore Database** を選択します。
3. 選択**デバイス** ボタンをクリックします **。**
4. ダイアログで **[バックアップデバイスの選択]** をクリックし、 **[追加]** をクリックして、サーバーのファイルシステム内のデータベースバックアップに移動し、バックアップを選択します。 クリックして **OK**です。
5. 必要に応じて、 **[ファイル]** ウィンドウでデータファイルとログファイルのターゲットの場所を変更します。 データファイルとログファイルは別のドライブに配置することをお勧めします。
6. クリックして **OK**です。 これにより、データベースの復元が開始されます。 完了すると、SQL Server インスタンスにデータベース WideWorldImporters がインストールされます。

### <a name="azure-sql-database"></a>Azure SQL Database

Bacpac を新しい SQL Database にインポートするには、Management Studio を使用できます。

1. optionalまだ Azure に SQL Server がない場合は、 [Azure portal](https://portal.azure.com/)に移動し、新しい SQL Database を作成します。 データベースを作成するプロセスでは、サーバーを作成します。 サーバーをメモしておきます。
   - [このチュートリアル](https://azure.microsoft.com/documentation/articles/sql-database-get-started/)を参照して、データベースを数分で作成してください
2. SQL Server Management Studio を開き、Azure のサーバーに接続します。
3. **[データベース]** ノードを右クリックし、 **[データ層アプリケーションのインポート]** をクリックします。
4. **[インポートの設定]** で、 **[ローカルディスクからインポート]** する を選択し、ファイルシステムからサンプルデータベースの bacpac を選択します。
5. **[データベースの設定]** で、データベース名を*WideWorldImportersDW*に変更し、使用するターゲットエディションとサービス目標を選択します。
6. [**次へ** **] をクリックして、** 展開を開始します。 完了するまで数分かかります。 S2 より低いサービス目標を指定すると、時間がかかることがあります。

## <a name="configuration"></a>Configuration

[SQL Server 2016 (およびそれ以降) の Developer/評価版に適用されます/Enterprise Edition]

サンプルデータベースでは、PolyBase を使用して、Hadoop または Azure blob storage 内のファイルに対してクエリを実行できます。 ただし、この機能は既定では SQL Server と共にインストールされません。 SQL Server セットアップ中に選択する必要があります。 そのため、インストール後の手順が必要です。

1. SQL Server Management Studio で、WideWorldImportersDW データベースに接続し、新しいクエリウィンドウを開きます。
2. 次の T-sql コマンドを実行して、データベースで PolyBase を使用できるようにします。

   [アプリケーション] を実行します。[Configuration_ApplyPolyBase]
