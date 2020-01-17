---
title: AdventureWorks サンプルデータベースをインストールして構成する
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 06/19/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 6a4b56a31ede0d8e011c1a2244f5d014e185e7e5
ms.sourcegitcommit: 9e026cfd9f2300f106af929d88a9b43301f5edc2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74318993"
---
# <a name="adventureworks-installation-and-configuration"></a>AdventureWorks のインストールと構成
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

AdventureWorks ダウンロードリンクとインストール手順。 

## <a name="prerequisites"></a>前提条件

- [SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)または[Azure SQL Database](https://azure.microsoft.com/services/sql-database/)。 このサンプルの完全なバージョンについては、SQL Server Evaluation/Developer/Enterprise Edition を使用してください。
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。 最良の結果を得るには、2016年6月リリース以降を使用します。
 
## <a name="oltp-downloads"></a>OLTP ダウンロード

AdventureWorks の OLTP バージョンへの直接リンクについては、以下を参照してください。

- [AdventureWorks2017](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak)
- [AdventureWorks2016](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016.bak)
- [AdventureWorks2014](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2014.bak)
- [AdventureWorks2012](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2012.bak)
- [AdventureWorks2008R2](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-oltp.bak)


## <a name="data-warehouse-downloads"></a>データウェアハウスのダウンロード

AdventureWorks のデータウェアハウスバージョンへの直接リンクについては、以下を参照してください。

- [AdventureWorksDW2017](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2017.bak)
- [AdventureWorksDW2016](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016.bak)
- [AdventureWorksDW2014](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2014.bak)
- [AdventureWorksDW2012](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2012.bak)
- [AdventureWorksDW2008R2](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008-dw.bak)

## <a name="creation-scripts"></a>作成スクリプト
次のスクリプトを使用すると、すべてのバージョンに関係なく、AdventureWorks データベース全体を作成できます。 

- [AdventureWorks OLTP スクリプト Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [AdventureWorks DW スクリプト Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

## <a name="github-links"></a>GitHub リンク

- [SQL 2014-2016 のすべての AdventureWorks ファイル](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [SQL 2012 のすべての AdventureWorks ファイル](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [SQL 2008 および2008R2 のすべての AdventureWorks ファイル](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)

## <a name="install-to-sql-server"></a>SQL Server にインストールする

### <a name="restore-backup"></a>バックアップの復元
SQL Server Management Studio を使用してデータベースのバックアップを復元するには、次の手順に従います。 

1. SQL Server Management Studio を開き、ターゲットの SQL Server インスタンスに接続します。
2. [**データベース**] ノードを右クリックし、[**データベースの復元**] を選択します。
3. [**デバイス**] を選択し、省略記号ボタン ([.**.**.]) をクリックします。
4. ダイアログで [**バックアップデバイスの選択**] をクリックし、[**追加**] をクリックして、サーバーのファイルシステム内のデータベースバックアップに移動し、バックアップを選択します。 [**OK**] をクリックすると、
5. 必要に応じて、[**ファイル**] ウィンドウでデータファイルとログファイルのターゲットの場所を変更します。 データファイルとログファイルは別のドライブに配置することをお勧めします。
6. [**OK**] をクリックすると、 これにより、データベースの復元が開始されます。 完了すると、AdventureWorks データベースが SQL Server インスタンスにインストールされます。

SQL Server データベースの復元の詳細については、「 [SSMS を使用したデータベースバックアップの復元](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)」を参照してください。


### <a name="attach-a-datafile"></a>データファイルをアタッチする
次の手順に従って、SQL Server Management Studio を使用してデータベースのデータファイルをアタッチします。

1. SQL Server Management Studio を開き、ターゲットの SQL Server インスタンスに接続します。
2. [**データベース**] ノードを右クリックし、[**アタッチ**] を選択します。
3. [**追加**] を選択し、に移動します。アタッチする MDF ファイル。 
1. ファイルを選択し、 **[OK]** をクリックします。 
    1. 選択したデータベースが下部のウィンドウに表示されます。 ファイルが "見つかりません" と表示されている場合は、ファイル名の横にある省略記号 (**..**.) を選択し、パスを正しいパスに更新します。 
    1. ログファイル (.ldf) ではなく、データファイル (.mdf) のみがある場合は、下部のウィンドウで .ldf を強調表示し、[**削除**] を選択します。 これにより、新しいログファイルが作成されます。 
1. [ **OK]** を選択してファイルをアタッチします。 ファイルがアタッチされると、AdventureWorks データベースが SQL Server インスタンスにインストールされます。  

データベースファイルのアタッチの詳細については、「[データベースのアタッチ](../relational-databases/databases/attach-a-database.md)」を参照してください。 

## <a name="install-to-azure-sql-database"></a>Azure SQL Database にインストールする


まだ Azure に SQL Server がない場合は、 [Azure portal](https://portal.azure.com/)に移動し、新しい SQL Database を作成します。 データベースを作成するプロセスでは、サーバーを作成します。 サーバーをメモしておきます。 データベースを数分で作成するには、[このチュートリアル](https://azure.microsoft.com/documentation/articles/sql-database-get-started/)を参照してください。

1. Azure portal に接続します。
1. ナビゲーションウィンドウの左上にある [**リソースの作成**] を選択します。 
1. [**データベース**] を選択し、[ **SQL Database**] を選択します。 
1. 必要な情報を入力します。
1. **[ソースの選択**] フィールドで、[ **Sample (AdventureWorksLT)** ] を選択して、最新の AdventureWorksLT バックアップのバックアップを復元します。
1. [**作成**] を選択して、AdventureWorksLT データベースの復元されたコピーである新しい SQL Database を作成します。 


## <a name="see-also"></a>参照
[SQL Server Management Studio のチュートリアル](../ssms/tutorials/tutorial-sql-server-management-studio.md)   
[SQL Server データベースエンジンのチュートリアル](../relational-databases/database-engine-tutorials.md)
