---
title: レッスン 1:SSIS によるプロジェクトと基本パッケージの作成 | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 84d0b877-603f-4f8e-bb6b-671558ade5c2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ff31579a425f9e86fed11811c9d0a42c3113ee15
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257073"
---
# <a name="lesson-1-create-a-project-and-basic-package-with-ssis"></a>レッスン 1:SSIS によるプロジェクトと基本パッケージの作成

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



この実習では、シンプルな ETL パッケージを作成します。このパッケージは、1 つのフラット ファイル ソースからデータを抽出し、2 つの参照変換を使用してそのデータを変換します。さらに、変換したデータを **AdventureWorksDW2012** サンプル データベースの **FactCurrencyRate** ファクト テーブルのコピーに書き込みます。 ここでは、新しいパッケージを作成する方法、データの変換元と変換先の接続を追加、構成する方法、新しい制御フロー コンポーネントとデータ フロー コンポーネントを操作する方法を学習します。  
  
パッケージを作成する前に、ソース データの形式と変換先データの形式を理解する必要があります。 理解することで、ソース データを変換先にマップするための変換を定義できます。  

## <a name="prerequisites"></a>前提条件

このチュートリアルでは、Microsoft SQL Server Data Tools、一連のサンプル パッケージ、サンプル データベースを使用します。

* SQL Server Data Tools をインストールするには、「[SQL Server Data Tools のダウンロード](../ssdt/download-sql-server-data-tools-ssdt.md)」を参照してください。  
  
* このチュートリアルのレッスン パッケージをすべてダウンロードするには:

    1.  [Integration Services チュートリアル ファイル](https://www.microsoft.com/download/details.aspx?id=56827)のページに移動します。

    2.  **[ダウンロード]** ボタンを選択します。

    3.  **Creating a Simple ETL Package.zip** ファイルを選択し、 **[次へ]** を選択します。

    4.  ファイルのダウンロード後、そのコンテンツを解凍し、ローカル ディレクトリに置きます。  

* **AdventureWorksDW2012** サンプル データベースをインストールし、[AdventureWorks サンプル データベースのインストールと構成 (SQL)](../samples/adventureworks-install-configure.md) に関するページを参照してください。
  
## <a name="look-at-the-source-data"></a>ソース データを表示する
このチュートリアルで使用するソース データは、**SampleCurrencyData.txt** という名前のフラット ファイルに含まれている一連の通貨履歴データです。 ソース データには、通貨の平均相場、通貨キー、日付キー、1 日の最終相場の 4 つの列があります。  
  
SampleCurrencyData.txt ファイルのソース データの例:  
  
<pre>1.00070049USD9/3/05 0:001.001201442  
1.00020004USD9/4/05 0:001  
1.00020004USD9/5/05 0:001.001201442  
1.00020004USD9/6/05 0:001  
1.00020004USD9/7/05 0:001.00070049  
1.00070049USD9/8/05 0:000.99980004  
1.00070049USD9/9/05 0:001.001502253  
1.00070049USD9/10/05 0:000.99990001  
1.00020004USD9/11/05 0:001.001101211  
1.00020004USD9/12/05 0:000.99970009</pre>  
  
フラット ファイル ソース データを操作する前に、フラット ファイル接続マネージャーがフラット ファイル データをどのように解釈するのかを理解しておく必要があります。 フラット ファイル ソースが Unicode の場合、すべての列が [DT_WSTR] として定義され、既定の列幅 50 が設定されます。 フラット ファイル ソースが ANSI エンコードの場合は、列が [DT_STR] として定義され、列幅が既定の 50 になります。 これらの既定値を変更し、自分のデータにより適した文字列型にしなければならない場合があります。 変換先のデータ型を見て、フラット ファイル接続マネージャー内でその型を選択する必要があります。  
  
## <a name="look-at-the-destination-data"></a>変換先データを見る
ソース データの変換先は、**AdventureWorksDW** の **FactCurrencyRate** ファクト テーブルのコピーです。 次の表に示すように、**FactCurrencyRate** ファクト テーブルには 4 つの列があり、さらに 2 つのディメンション テーブルへのリレーションシップがあります。  
  
|列名|データ型|参照テーブル|参照列|  
|---------------|-------------|----------------|-----------------|  
|AverageRate|float|なし|なし|  
|CurrencyKey|int (FK)|DimCurrency|CurrencyKey (PK)|  
|DateKey|int (FK)|DimDate|DateKey (PK)|  
|EndOfDayRate|float|なし|なし|  
  
## <a name="map-the-source-data-to-the-destination"></a>変換先にソース データをマップする  
変換元と変換先のデータ形式を調べてみると、**CurrencyKey** と **DateKey** の値については参照が必要であることがわかります。 これらの参照を実行する変換では、**DimCurrency** ディメンション テーブルと **DimDate** ディメンション テーブルの代替キーを使用することにより、それらの値を取得します。  
  
|フラット ファイルの列|テーブル名|列名|データ型|  
|--------------------|--------------|---------------|-------------|  
|0|FactCurrencyRate|AverageRate|float|  
|1|DimCurrency|CurrencyAlternateKey|nchar (3)|  
|2|DimDate|FullDateAlternateKey|date|  
|3|FactCurrencyRate|EndOfDayRate|float|  
  
## <a name="lesson-tasks"></a>このレッスンの作業  
このレッスンの内容は次のとおりです。  
  
-   [ステップ 1:新しい Integration Services プロジェクトを作成する](../integration-services/lesson-1-1-creating-a-new-integration-services-project.md)  
  
-   [手順 2:フラット ファイル接続マネージャーの追加と構成](../integration-services/lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
-   [ステップ 3:OLE DB 接続マネージャーを追加し、構成する](../integration-services/lesson-1-3-adding-and-configuring-an-ole-db-connection-manager.md)  
  
-   [手順 4:データ フロー タスクをパッケージに追加する](../integration-services/lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
-   [手順 5:フラット ファイルの変換元を追加し、構成する](../integration-services/lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
-   [手順 6:参照変換を追加し、構成する](../integration-services/lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
-   [手順 7:OLE DB 変換先を追加し、構成する](../integration-services/lesson-1-7-adding-and-configuring-the-ole-db-destination.md)  
  
-   [手順 8: レッスン 1 パッケージに注釈を付け、書式を設定する](../integration-services/lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
-   [手順 9:レッスン 1 パッケージをテストする](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>レッスンの開始  
[ステップ 1:新しい Integration Services プロジェクトを作成する](../integration-services/lesson-1-1-creating-a-new-integration-services-project.md)  
  
