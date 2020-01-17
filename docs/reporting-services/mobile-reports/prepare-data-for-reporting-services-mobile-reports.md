---
title: Reporting Services モバイル レポート用にデータを準備する | Microsoft Docs
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 8adce9ad-6a08-4d20-b1cf-d3c45544d8de
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9ded496c3509420d54325dc054e018048ede0732
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62499933"
---
# <a name="prepare-data-for-reporting-services-mobile-reports"></a>Reporting Services モバイル レポート用にデータを準備する
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)] は、フィルター処理、集計、タイムスライスを含む、多くの複雑なデータ操作をサポートしています。 この記事では、データを準備するときに考慮する必要があるいくつかの点について説明します。 あらかじめデータを集計することで、モバイル レポートの作成と使用の両方を最適化できます。一部のモバイル レポートのデザインではこれが必要です。   
  
## <a name="date-and-time-formats"></a>日付および時刻の形式 
モバイル レポートで使用する日付と時間の間隔を扱うときには (特に TimeNavigator を使用する場合)、 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] が識別できるように日付/時刻列の書式を正しく設定することが重要です。 次に、有効な日付/時刻形式の例を示します。  
  
    05/01/2009    
    2009-05-01    
    05/01/2009 14:57:32.8    
    2009-05-01 14:57:32.8    
    2009-05-01T14:57:32.8375298-04:00    
    5/01/2008 14:57:32.80 -07:00    
    1 May 2008 2:57:32.8 PM    
    Fri, 15 May 2009 20:10:57 GMT    
  
日付と時刻に基づくデータセットは、ほとんどの場合、1 つまたは複数の日付/時間間隔 (時間単位、日単位、月単位、四半期単位、年単位など) によって記述できます。 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] では、異なる粒度の複数のテーブルを結合し、それらを 1 つのモバイル レポートに表示できます。 ただし、元のデータセットと関連する間隔を覚えておいてください。これらは、どのような日付/時刻フィルター オプションで最終的なモバイル レポートでユーザーに提示するかを決定するときに役立ちます。  

[!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] の多次元モデルと表形式モデルの日付フィールドでは、共有データセットで日付の書式設定が失われる可能性があります。 書式設定を維持するための方法については、「 [Retain date formatting for Analysis Services in mobile reports](../../reporting-services/mobile-reports/retain-date-formatting-for-analysis-services-in-mobile-reports.md) 」(モバイル レポートで Analysis Services の日付の書式設定を保持する) を参照してください。
  
## <a name="preparing-filter-data"></a>フィルター データを準備する ##  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] は、日付/時刻フィールドとキー フィールドの両方に基づいてデータをフィルター処理できます。 キー フィールドの値は数値にすることもできますが、ほとんどの場合、ID または文字列値のいずれかです。 選択リストなどのナビゲーター要素で使用するためにフィルター フィールドを準備するには、フィルター キーがデータ テーブル内の 1 つの列である必要があります。 このようにすることで、フィルター列の値に基づいてテーブル行をグループ化できます。 複数の列が存在し、各列に異なるフィルター キー、つまりフィルタ条件が含まれている場合は、複数のフィルター ナビゲーターを同時に階層的に、または個別に使用してモバイル レポートを作成できます。  
  
| Industry  | Country   | Region    |  
| ------------- | ------------- | ------------- |  
| 銀行     | アフガニスタン   | アジア      |  
| 商用およびプロフェッショナル サービス | アフガニスタン | アジア |  
| 料理、飲料、タバコ | アフガニスタン | アジア |  
| [メディア] | アフガニスタン | アジア |  
| 製薬 | アフガニスタン | アジア |  
| 食品および日用品小売 | アルバニア | ヨーロッパ |  
  
  
キー ベースのフィルターは、ツリー構造の選択リストで使用するために階層構造にすることもできます。 このようなシナリオで使用するためにデータを準備するには、階層構造を記述するルックアップ テーブルを作成します。 キー列と親キー列を含むテーブル構造を使用して、ノードが階層全体のどこに所属するかを示します。  
  
次のテーブルには、ParentKey 項目が最初に [ItemKey] 列に表示され、次にその子アイテムの隣の [ParentItemKey] 列に表示されます。   
  
|ItemKey    | ParentItemKey |  
| ------------- | ------------- |  
| 金融    |   |  
| 工業   |   |  
| 日用品 |    |  
| 一般消費財 |  |     
| 医療   |   |  
| 情報技術 |  |  
| 銀行 | 金融 |  
| 不動産 | 金融 |  
| 総合金融 |  金融 |   
| 保険 |   金融 |  
| 商用およびプロフェッショナル サービス |  工業 |  
| 資本財 |   工業 |  
| 輸送 |  工業 |  
| 料理、飲料、タバコ |    日用品 |  
| 食品および日用品小売 |    日用品 |  
| 家庭用および個人用製品 | 日用品 |  
| [メディア] | 一般消費財 |  
| 自動車および部品 |  一般消費財 |  
| 一般耐久消費財および衣料品 |一般消費財 |  
| コンシューマー サービス |   一般消費財 |  
| 小売 | 一般消費財 |  
| 製薬   | 医療 |  
| 医療機器およびサービス |    医療 |  
| ソフトウェアおよびサービス | 情報技術 |  
| テクノロジ ハードウェアおよび機器   | 情報技術 |  
| 電気通信サービス |情報技術 |  
  
### <a name="see-also"></a>参照  
- [Reporting Services モバイル レポート用に Excel データを準備する](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md)  
- [Retain date formatting for Analysis Services in mobile reports](../../reporting-services/mobile-reports/retain-date-formatting-for-analysis-services-in-mobile-reports.md)
- [SQL Server Mobile Report Publisher を使用してモバイル レポートを作成する](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)
  
  
  

