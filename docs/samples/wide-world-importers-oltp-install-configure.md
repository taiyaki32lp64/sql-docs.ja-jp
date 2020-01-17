---
title: WideWorldImporters サンプルデータベースをインストールして構成する
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: e1683adfa20851d279e8b8e18a3c767db9e5810d
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056272"
---
# <a name="installation-and-configuration"></a>インストールと構成
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
大規模な環境では、OLTP データベースのインストールと構成の手順について説明します。

## <a name="prerequisites"></a>Prerequisites

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) (またはそれ以降) または[Azure SQL Database](https://azure.microsoft.com/services/sql-database/)。 このサンプルの完全なバージョンについては、SQL Server Evaluation/Developer/Enterprise Edition を使用してください。
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。 最善の結果を得るには、2016 年 6 月リリース以降を使用してください。

## <a name="download"></a>ダウンロード

サンプルの最新リリース:

[wide-world-importers-release](https://go.microsoft.com/fwlink/?LinkID=800630)

SQL Server または Azure SQL Database のエディションに対応するサンプル WideWorldImporters database backup/bacpac をダウンロードします。

サンプル データベースを再作成するソース コードは、以下の場所から使用可能です。 データ生成にはランダムな要因があるため、サンプルを再作成すると、データにわずかな違いが生じることに注意してください。

[wide-world-importers](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-database-scripts)

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
5. **[データベースの設定]** で、データベース名を*WideWorldImporters*に変更し、使用するターゲットエディションとサービス目標を選択します。
6. [**次へ** **] をクリックして、** 展開を開始します。 P1 の完了までに数分かかります。 価格レベルを低くする必要がある場合は、新しい P1 データベースにインポートし、価格レベルを目的のレベルに変更することをお勧めします。

## <a name="configuration"></a>Configuration

### <a name="full-text-indexing"></a>フルテキスト インデックス作成

サンプルデータベースでは、フルテキストインデックスを使用できます。 ただし、この機能は既定では SQL Server と共にインストールされません。 SQL Server セットアップ中に選択する必要があります (Azure SQL DB では既定で有効になっています)。 そのため、インストール後の手順が必要です。

1. SQL Server Management Studio で、WideWorldImporters データベースに接続し、新しいクエリウィンドウを開きます。
2. 次の T-sql コマンドを実行して、データベースでフルテキストインデックスの使用を有効にします。 `EXECUTE Application.Configuration_ApplyFullTextIndexing`


### <a name="sql-server-audit"></a>SQL Server Audit

適用対象: SQL Server

SQL Server で監査を有効にするには、サーバー構成が必要です。 WideWorldImporters サンプルの SQL Server 監査を有効にするには、データベースで次のステートメントを実行します。

    EXECUTE [Application].[Configuration_ApplyAuditing]

Azure SQL Database では、 [Azure portal](https://portal.azure.com/)によって監査が構成されます。

### <a name="row-level-security"></a>行レベルのセキュリティ

適用対象: Azure SQL Database

行レベルのセキュリティは、WideWorldImporters の bacpac ダウンロードでは既定で有効になっていません。 データベースで行レベルのセキュリティを有効にするには、次のストアドプロシージャを実行します。

    EXECUTE [Application].[Configuration_ApplyRowLevelSecurity]

