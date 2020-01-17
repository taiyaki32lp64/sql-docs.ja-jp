---
title: 分析情報ウィジェットを使用してサーバーとデータベースを監視する
titleSuffix: Azure Data Studio
description: Azure Data Studio の分析情報ウィジェットについて説明します
ms.custom: seodec18, sqlfreshmay19, seo-lt-2019
ms.date: 05/14/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4edf4003d40da35dcd54b3938e0f318ef8b9440a
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957056"
---
# <a name="manage-servers-and-databases-with-insight-widgets-in-includename-sosincludesname-sos-shortmd"></a>[!INCLUDE[name-sos](../includes/name-sos-short.md)] の分析情報ウィジェットを使用してサーバーとデータベースを管理する

分析情報ウィジェットでは、お客様がサーバーとデータベースを監視するために使用している Transact-SQL (T-SQL) クエリが取得され、それらが洞察に富んだ視覚エフェクトに変換されます。

分析情報とは、サーバーとデータベースの監視ダッシュボードに追加するカスタマイズ可能なチャートとグラフです。 ご利用のサーバーとデータベースに関するひとめでわかる分析情報を表示し、次に詳細にドリルダウンして、定義した管理アクションを開始します。

次の例のように、サーバーおよびデータベース用の素晴らしい管理ダッシュボードを作成することができます。

![データベース ダッシュボード](media/insight-widgets/database-dashboard.png)

さまざまな種類の分析情報ウィジェットの作成を開始するには、次のチュートリアルをご覧ください。

- [カスタム分析情報ウィジェットのビルド](tutorial-build-custom-insight-sql-server.md)
- *組み込みの分析情報ウィジェットを有効にする*
  - [パフォーマンス監視の分析情報を有効にする](tutorial-qds-sql-server.md)
  - [テーブル領域の使用状況に関する分析情報を有効にする](tutorial-table-space-sql-server.md)

## <a name="sql-queries"></a>SQL クエリ

[!INCLUDE[name-sos](../includes/name-sos-short.md)] では、可能な限り最小の JSON 構成で T-SQL を使用することが試みられているため、別の言語や高負荷のユーザー インターフェイスのさらなる導入は回避することが試みられます。 T-SQL を使用して分析情報ウィジェットを構成すると、洞察に富んだウィジェットに変換できる有用な T-SQL クエリの既存のソースが無数に活用されます。

分析情報ウィジェットは、次に示す 1 つまたは 2 つの T-SQL クエリで構成されます。
* *分析情報ウィジェット クエリ*はウィジェットに表示されるデータを返すクエリであり、これは必須となります。
* *分析情報の詳細のクエリ*は、分析情報の詳細ページを作成する場合にのみ必要です。

分析情報ウィジェット クエリでは、カウント、チャート、またはグラフをレンダリングするデータセットが定義されます。 分析情報の詳細のクエリは、関連する分析情報の詳細情報を分析情報の詳細パネルに表形式で一覧表示するために使用されます。 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] では、分析情報ウィジェット クエリが実行され、クエリ結果セットがチャートのデータセットにマップされてから、そのレンダリングが行われます。 ユーザーが分析情報の詳細を開くと、分析情報の詳細のクエリが実行され、ダイアログ内のグリッド ビューに結果が出力されます。

基本的な考え方は、T-SQL クエリをカウント、チャート、グラフ ウィジェットのデータセットとして使用できるように、T-SQL クエリを記述することです。 

## <a name="summary"></a>まとめ

T-SQL クエリとその結果セットにより、分析情報ウィジェットの動作が決まります。 グラフの種類に対するクエリを作成すること、または既存のクエリに対して適切なグラフの種類をマップすることは、効果的な分析情報ウィジェットを構築する上で重要な考慮事項です。



## <a name="additional-resources"></a>その他のリソース
- [クエリ エディター](tutorial-sql-editor.md)

