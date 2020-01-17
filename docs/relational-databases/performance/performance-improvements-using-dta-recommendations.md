---
title: DTA で推奨されるパフォーマンスの強化
ms.custom: seo-dt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine Tuning Advisor, performance improvements
ms.assetid: 2e51ea06-81cb-4454-b111-da02808468e6
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 48614ea63ab56974e3eafb55b0f43dd83436ec85
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74164923"
---
# <a name="performance-improvements-using-database-engine-tuning-advisor-dta-recommendations"></a>データベース エンジン チューニング アドバイザー (DTA) の推奨事項を使用したパフォーマンスの強化
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]


---
データ ウェアハウスと分析ワークロードのパフォーマンスは**列ストア** インデックスで大幅に上がります。特に、大きなテーブルをスキャンするクエリで効果を発揮します。 **行ストア** (B+-tree) インデックスは、比較的少量のデータにアクセスし、特定の値または値範囲を検索するクエリで最も効果を発揮します。 行ストア インデックスは行を並べ替えた上で提示するので、クエリ実行プランの並べ替えコストの削減にもなります。 そのため、行ストア インデックスと列ストア インデックスをどのように組み合わせるかという選択はアプリケーションのワークロードに依存します。

データベース エンジン チューニング アドバイザー (DTA) は、SQL Server 2016 以降、所与のデータベース ワークロードを分析することで**行ストア インデックスと列ストア インデックスの最適な組み合わせ**を推奨できるようになりました。 

ワークロード パフォーマンスに関する DTA 推奨の長所を示すために、実際のお客様のワークロードで実験しました。 お客様のワークロードごとに、DTA に個々のクエリとクエリの完全ワークロードを分析させました。 3 つの選択肢を考慮します。
  
  1. **列ストアのみ**:DTA を使用せず、すべてのテーブルに関して列ストア インデックスのみを作成します。 
  2. **DTA (行ストアのみ)** :行ストア インデックスのみを推奨するオプションを指定して DTA を実行します。
  3. **DTA (行ストア + 列ストア)** :行ストア インデックスと列ストア インデックスの両方を推奨するオプションを指定して DTA を実行します。  
   
この場合、推奨されたインデックスを実装しました。 クエリまたはワークロードを複数回実行し、その平均 CPU 時間をミリ秒単位で報告します。 次の図は、2 つの異なる顧客データベースを対象にワークロードの CPU 時間をミリ秒単位で描画したものです。 y 軸 (CPU 時間) では対数スケールが使用されています。   


![DTA-columnstore-rowstore-performance](../../relational-databases/performance/media/dta-columnstore-rowstore-performance.gif)



**物理的設計の混在が必要**:Customer 1 Query 1 に相当する最初のバー セットの DTA (行ストア + 列ストア) から、 4 つの列ストア インデックスと 6 つの行ストア インデックスのセットが推奨されます。結果的に、列ストア インデックスのみや DTA (行ストアのみ) と比較し、CPU 時間が 2.5 ～ 4 分の 1 に短縮されます。 これは、*クエリが 1 つの場合でも*、行ストア インデックスと列ストア インデックスが混在する物理的設計の長所を示しています。 

**行ストア インデックス推奨の効果**:2 つ目と 3 つ目のバー セット (Customer 1 Query 2 と Customer 2 Query 1 に相当) では、適切な行ストア インデックスから効果を得られる選択的フィルター述語がクエリに与えられるケースです。 いずれのクエリでも、DTA (行ストアのみ) と DTA (行ストア + 列ストア) から、行ストア インデックスのみが推奨されることがわかります。 以上の例からは、列ストア インデックスを推奨するオプションで DTA を呼び出すときであっても、そのコストに基づく手法により、ワークロードに対して実際に効果がある場合にのみ、列ストア インデックスが推奨されることもわかります。

**列ストア インデックス推奨の効果**:Customer 2 Query 2 に対応する 4 つ目のバー セットでは、列ストア インデックスの効果がありえる大きなテーブルがスキャンされます。 DTA (行ストアのみ) が生成する推奨では、列ストア インデックスが存在するときと比較し、CPU 時間が増えます。 DTA (行ストア + 列ストア) は、列ストアのみのオプションのクエリ実行パフォーマンスに匹敵する列ストア インデックスを推奨します。

**複数のクエリによるワークロードの推奨の効果**:Customer 2 の完全なワークロードに相当する最後のバー セットは、ワークロードの複数のクエリを分析し、ワークロード全体の実行コストを改善できる行ストアと列ストアの適切なセットを推奨する DTA の能力を例示するものです。 DTA (行ストア + columnstore) から、4 つの列ストア インデックスと数十の行ストア インデックスが推奨されます。結果的に、列ストア インデックスのみを作成するオプションと比較し、ワークロードを 1 桁以上改善します。DTA (行ストアのみ) と比較した場合、4 ～ 5 倍の改善になります。

まとめると、上の例により、SQL Server Database Engine でサポートされる行ストアと列ストアの両方を適宜活用し、ワークロードの CPU 時間を大幅に短縮できるインデックスの組み合わせを推奨する DTA の能力が実証されることになります。 

<a name="see-also"></a>参照
---
[Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)

[データベース エンジン チューニング アドバイザー (DTA) での列ストア インデックスの推奨事項](../../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md)

[列ストア インデックスの説明](~/relational-databases/indexes/columnstore-indexes-overview.md)

[データ ウェアハウスの列ストア インデックス](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)

[CREATE COLUMNSTORE INDEX (Transact-SQL)](../../t-sql/statements/create-columnstore-index-transact-sql.md)

[CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)



