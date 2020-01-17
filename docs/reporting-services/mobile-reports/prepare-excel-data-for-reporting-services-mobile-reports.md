---
title: Reporting Services モバイル レポート用に Excel データを準備する | Microsoft Docs
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 16698f8d-bfc7-4eca-9e97-82c99d8bc08e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9285b9b89930fe540f9b5493f1730184cf4e9526
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62499953"
---
# <a name="prepare-excel-data-for-reporting-services-mobile-reports"></a>Reporting Services モバイル レポート用に Excel データを準備する
  
ここでは、Excel ファイルおよびワークシートをモバイル レポートで使用できるように準備する際に留意すべき点をいくつか説明します。  
  
## <a name="do"></a>次のことを行います  
  
- データセットごとにワークシートを 1 つ用意する。  
- 先頭行に列ヘッダーを設定する。  
- 各列内でデータ型の一貫性を維持する。  
- Excel のセルを適切な型で書式設定する。  
- Excel ではデータ モデルではなくワークシートにデータを含める。  
- 数式を使用する場合は、必ず同じ数式を使用して列全体の計算を行う。  
- Excel 2007 以降を使用する。  
- Excel ファイルは XLSX 拡張子で保存する。  
          
## <a name="dont"></a>次のことは行わないでください  
  
- データセットのワークシートに、画像、グラフ、ピボット テーブル、またはその他の埋め込みオブジェクトを含める。  
- 合計行または集計行を含める。  
- インポート時にファイルを Excel で開いたままにする。  
- 通貨またはその他の記号を追加することで、数値を手動で書式設定する。  
- データ モデルに格納されたデータを含むブックを使用する。  
  
## <a name="worksheets"></a>ワークシート  
          
Excel ファイルをモバイル レポート用のデータセットとして準備する際は、ワークシートごとにデータセットが 1 ずつしかないことを確認してください。 個々のワークシートはそれぞれ独立したテーブルとして [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] にインポートされます。 複数の Excel ソースからの同じ名前のワークシートについては、インポート時に、インクリメンタル数を追加することで名前が変更されます。 たとえば、ブックに "MyWorksheet" というタイトルの付いたワークシートが 3 つ含まれている場合、2 番目と 3 番目のワークシートはそれぞれ、"MyWorksheet0" および "MyWorksheet1" という名前に変更されます。 次のスクリーン ショットは、インポートの準備が整った理想的な Excel ワークシートの先頭部分の行を示しています。  
  
![SS_MRP_ExcelDataSheet](../../reporting-services/mobile-reports/media/ss-mrp-exceldatasheet.png)  
          
## <a name="column-headers"></a>列ヘッダー  
  
上記の例の最初の行には、列のメトリックの名前が含まれているのがわかります。 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] では、これらの列ヘッダーを、ギャラリー要素設定で簡単に参照できるように保持します。 ただし、列ヘッダーは必須ではありません。 列ヘッダーがない場合、 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] は Excel の生成規則 ( A、B、C、…、AA、BB、...) に従ってヘッダーを生成します。  
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] は、Excel ワークシートをインポートするとき、各列の最初の 2 つのセルのデータ型を比較することで、先頭行のヘッダーを自動的に検出します。 任意の列の最初の 2 つのセルのデータ型が一致しない場合、最初の行は列ヘッダーを含んでいると見なされます。 したがって、テーブルに数値列ヘッダーが含まれている場合は、それらがインポート処理時にヘッダーとして検出されるようにヘッダー名の頭に文字列が付けられます。  
  
## <a name="cells"></a>[セル]  
  
ワークシートの各列のセル データは、一貫性が保たれている必要があります。 各列にはインポート時にデータ型が割り当てられます。 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] では、データ型を自動的に検出し、文字列、double (数値)、ブール値 (true/false)、または datetime (日付時間) と判定します。 同じ列にデータ型が混在している場合、データ型の検出が正しく行われなかったり、完全に失敗したりすることがあります。 この検出では、string 型の列ヘッダーが存在する可能性があることを考慮に入れます。 必要な型が [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] によって確実に検出されるように、Excel ではセルを適切な型で書式設定する必要があります。 上記の例では、6 つの列の型が次のように設定されています。  
*  datetime 型の列が 1 つ  
*  string 型の列が 1 つ  
*  double 型の列が 4 つ  
  
ワークシートに集計セルまたは数式が含まれている場合、結果として生成された表示値のみが [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]にインポートされます。  
  
## <a name="file-location-and-refreshing-excel-data"></a>ファイルの場所と Excel データの更新  
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]にインポートする Excel ファイルの格納場所について、制限はありません。 ただし、インポート後にファイルの移動または名前の変更を行った場合、データ ビューにある **[すべてのデータの更新]** コマンドでそのデータを更新することができなくなります。   
  
>**注**: [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] は Excel のデータを自動更新しません。 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] **[更新]** コマンドを使用してファイルを更新することができますが、それはファイルが移動されていない場合に限られます。  
  
## <a name="dates"></a>日付  
  
日付フィールドは多くのモバイル レポートで不可欠です。このため、Excel ではセルが日付として適切に書式設定されている必要があります。 場合によっては、変換が必要です。 Excel でセルをテキストから日付に変換するための式の例を次に示します。  
  
    Week 24-2013=DATE(MID(A2,9,4),1,-2)-WEEKDAY(DATE(MID(A2,9,4),1,3))+MID(A2,6,2)*7  
  
    2013/03/21=DATEVALUE(A1)  
  
    2013-mar-12=DATEVALUE(RIGHT(A1,2)&"-"&MID(A1,6,3)&"-"&LEFT(A1,4))  
  
セルを変換したら、セルを日付として書式設定する必要があります。そのためには、該当するセルを選択するか、列全体を選択し、 **[コンテキスト]** メニュー  >  **[セルの書式設定]** の順に選択し、 **[カテゴリ]** の一覧から **[日付]** を選択します。 また、Excel の区切り位置ウィザードを使用して、テキスト セルを適切に書式設定された日付に変換することができます。  
  
## <a name="unsupported"></a>サポートされていない  
  
ワークシート データの形式が上記で説明した形式とは異なる場合、インポート時に予期しない結果が発生する可能性があります。 Excel ファイル内のワークシートを、モバイル レポートで使用するのに適した形式のワークシートのみに制限することをお勧めします。  
  
Excel ワークシート内のカスタム オブジェクト (ピボット テーブル、視覚化エフェクト、画像など) は、 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]にインポートされません。  
  
### <a name="see-also"></a>参照  
- [Reporting Services モバイル レポート用にデータを準備する](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)  
- [Create and publish mobile reports with SQL Server Mobile Report Publisher (SQL Server Mobile Report Publisher でモバイル レポートを作成し発行する)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  [iPad アプリ (Power BI for iOS) で SQL Server モバイル レポートと KPI を表示する](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  
-  [iPhone アプリ (Power BI for iOS) で SQL Server モバイル レポートと KPI を表示する](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-iphone-kpis-mobile-reports)  
  
  
  
  
  
  
  

