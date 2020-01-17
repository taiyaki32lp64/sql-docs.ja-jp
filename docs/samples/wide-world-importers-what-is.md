---
title: Wide World のインポーター-SQL のサンプルデータベース |Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 872892d307883bb7df31b08de701b2030d9aeb1f
ms.sourcegitcommit: bcc3b2c7474297aba17b7a63b17c103febdd0af9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2019
ms.locfileid: "68794608"
---
# <a name="wide-world-importers-sample-databases-for-microsoft-sql"></a>Microsoft SQL 用の大規模なインポーターのサンプルデータベース
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
これは、架空の会社全体のインポーターと、SQL Server および Azure SQL Database 用の WideWorldImporters サンプルデータベースで対処されているワークフローの概要です。  

Wide World のインポーター (WWI) は、サンフランシスコベイ領域からの卸売分野商品インポーターおよびディストリビューターです。

WWI の顧客は、卸売業者として、ほとんどの場合、個人を再販する企業です。 WWI は、専門ストア、supermarkets、コンピューティングストア、tourist 引力ショップ、および一部の個人を含む米国全体の小売顧客に販売します。 また、WWI は、WWI の代理で製品を宣伝するエージェントのネットワークを介して、他の卸売に販売しています。 WWI のすべての顧客は現在米国に基づいていますが、会社は他の国に拡張するためにプッシュするつもりです。

WWI は、分野、おもちゃの製造元、その他の分野卸売などのサプライヤーから商品を購入します。 顧客の注文を満たすためするために、WWI warehouse に商品を保管し、必要に応じてサプライヤーから注文を受けます。 また、大量の梱包材を購入し、お客様の利便性を高めるために、これらの製品をより小さな数量で販売します。

最近では、chilli チョコレートなどのさまざまな WWI novelties の販売を開始しました。  以前は、会社は chilled の項目を処理する必要がありませんでした。 ここで、食品取り扱いの要件を満たすために、chiller 室の気温と、chiller セクションを持つトラックを監視する必要があります。

## <a name="workflow-for-warehouse-stock-items"></a>倉庫の在庫品目のワークフロー

項目の在庫と分散の一般的なフローは次のとおりです。
- WWI は発注書を作成し、仕入先に送信します。
- サプライヤーは、項目を送信し、WWI を受け取り、倉庫で在庫します。
- 顧客が WWI から品目を注文する
- WWI は倉庫の在庫品目に顧客の注文を入力します。在庫が十分でない場合は、サプライヤーから追加の在庫を注文します。
- 在庫されていない項目を待機したくないお客様もいます。 5つの異なる在庫品目を注文し、4つの商品を使用できる場合は、4つの項目を受け取り、残りの項目を順番に受注します。 この項目は、後で別の出荷で送信されます。
- WWI は、通常、注文を請求書に変換することによって、在庫品目の顧客を請求します。
- 在庫されていない商品を注文する場合があります。 これらの項目は入荷待ちです。
- WWI は、独自の配送 van を通じて、または他の couriers または運賃方法を使用して、顧客に商品を配信します。
- お客様は請求書を WWI に支払います。
- 定期的に、WWI は注文書にあった商品の仕入先を支払います。 これは、多くの場合、商品を受け取った後に発生します。

## <a name="data-warehouse-and-analysis-workflow"></a>データウェアハウスと分析のワークフロー

WWI のチームは、WideWorldImporters データベースから運用レポートを生成するために SQL Server Reporting Services を使用しますが、データに対して分析を実行し、戦略的なレポートを生成する必要もあります。 チームは、データベース WideWorldImportersDW にディメンションデータモデルを作成しました。 このデータベースには、Integration Services パッケージが設定されます。

SQL Server Analysis Services は、ディメンションデータモデルのデータから分析データモデルを作成するために使用されます。 SQL Server Reporting Services は、ディメンションデータモデルから直接、または分析モデルから、戦略的レポートを生成するために使用されます。 Power BI は、同じデータからダッシュボードを作成するために使用されます。 ダッシュボードは、web サイト、携帯電話、タブレットで使用されます。 *注: これらのデータモデルとレポートはまだ使用できません*

## <a name="additional-workflows"></a>追加のワークフロー

これらは追加のワークフローです。
- WWI は、何らかの理由でお客様が適切な情報を得られない場合、または商品に欠陥がある場合にクレジットメモを発行します。 これらは負の請求書として扱われます。
- WWI は、在庫品目の手持ち数量を定期的にカウントし、システムで使用可能な在庫数量が正確であることを確認します。 (これを行うプロセスは、stocktake と呼ばれます)。
- コールドルーム温度。 Perishable 商品は refrigerated ルームに格納されています。 これらのルームからのセンサーデータは、監視と分析を目的としてデータベースに取り込まれたされます。
- 車両位置の追跡。 WWI の商品を輸送する車両には、場所を追跡するセンサーが含まれています。 この場所は、監視とその他の分析のためにデータベースに再び取り込まれたされます。

## <a name="fiscal-year"></a>会計年度

この会社は、11月1日に開始する財務年度を操作します。

## <a name="terms-of-use"></a>利用規約

サンプルデータベースとサンプルコードのライセンスについては、「 [license.txt](https://github.com/Microsoft/sql-server-samples/blob/master/license.txt) 」を参照してください。

サンプルデータベースには、data.gov および自然 EarthData から読み込まれたパブリックデータが含まれています。 使用条件は次のとおりです。[https://www.naturalearthdata.com/about/terms-of-use/](https://www.naturalearthdata.com/about/terms-of-use/)
