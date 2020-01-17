---
title: パーティション ストレージ モードおよび処理 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- storage [Analysis Services], partitions
- hybrid OLAP
- data storage [Analysis Services]
- relational OLAP
- multidimensional OLAP
- partitions [Analysis Services], storage
- storing data [Analysis Services], partitions
- HOLAP
- MOLAP
- ROLAP
ms.assetid: 86d17547-a0b6-47ac-876c-d7a5b15ac327
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 74f53ddb6e7e3fc6b9d14ddcc726c2766a598860
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62727578"
---
# <a name="partition-storage-modes-and-processing"></a>パーティションのストレージ モードおよび処理
  パーティションのストレージ モードは、クエリと処理のパフォーマンス、ストレージの要件、パーティションおよびその親メジャー グループと親キューブのストレージ場所に影響します。 また、ストレージ モードの選択内容は、処理の選択内容にも影響します。  
  
 パーティションでは、次の 3 つの基本的なストレージ モードのうちいずれかを使用できます。  
  
-   多次元 OLAP (MOLAP)  
  
-   リレーショナル OLAP (ROLAP)  
  
-   ハイブリッド OLAP (HOLAP)  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] すべての 3 つの基本的なストレージ モードをサポートしています。 また、ROLAP ストレージと MOLAP ストレージの特性を組み合わせてデータの即時性とクエリのパフォーマンスを向上させることができるプロアクティブ キャッシュもサポートされています。 詳細については、「[プロアクティブ キャッシュ (パーティション)](partitions-proactive-caching.md)」をご覧ください。  
  
## <a name="molap"></a>[MOLAP]  
 MOLAP ストレージ モードを使用した場合は、パーティションの処理時、パーティションの集計とそのソース データのコピーが [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の多次元構造に格納されます。 この MOLAP 構造は、クエリのパフォーマンスを最大限に高めるために高度に最適化されています。 ストレージの場所は、パーティションが定義されているコンピューター上、または [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] を実行している別のコンピューター上に配置できます。 ソース データのコピーは多次元構造に存在するため、パーティションのソース データにアクセスしないでクエリを解決できます。 集計を使用すればクエリの応答時間を大幅に削減できます。 パーティションの MOLAP 構造の現在のデータは、最新のパーティションの処理によって決まります。  
  
 ソース データの変更に伴い、MOLAP ストレージ内のオブジェクトを定期的に処理して、その変更内容を組み込み、ユーザーが使用できるようにする必要があります。 処理することで、MOLAP 構造のデータは完全または段階的に更新されます。 ある処理から次の処理までの間に待機時間が発生し、その間は OLAP オブジェクトのデータがソース データと一致しない場合があります。 MOLAP ストレージのオブジェクトは、パーティションまたはキューブをオフラインにすることなく、段階的または完全に更新できます。 ただし、キューブをオフラインにして、OLAP オブジェクトへの特定の構造の変更を処理する必要がある場合があります。 MOLAP ストレージの更新に必要なダウンタイムを最小限に抑えるには、ステージング サーバーでキューブの更新と処理を行い、データベースの同期化を使用して、処理したオブジェクトを実稼働サーバーにコピーします。 また、プロアクティブ キャッシュを使用して、MOLAP ストレージのパフォーマンス面の利点を維持しながら、待機時間を最小限に抑えて可用性を最大限に高めることもできます。 詳細については、次を参照してください[プロアクティブ キャッシュ&#40;パーティション&#41;](partitions-proactive-caching.md)、 [Analysis Services データベースの同期](../multidimensional-models/synchronize-analysis-services-databases.md)、および[多次元モデル オブジェクト処理](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
## <a name="rolap"></a>[ROLAP]  
 ROLAP ストレージ モードでは、パーティションの集計はパーティションのデータ ソース内で指定されたリレーショナル データベースのインデックス付きビューに格納されます。 MOLAP ストレージ モードとは異なり、ROLAP ではソース データのコピーが [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のデータ フォルダーに格納されません。 代わりに、クエリ キャッシュから結果を取得できない場合は、クエリに応答するためにデータ ソースのインデックス付きビューへのアクセスが行われます。 通常、ROLAP ストレージ モードでは、MOLAP または HOLAP ストレージ モードよりもクエリ応答が遅くなります。 一般的に処理時間も遅くなります。 しかし、ROLAP によってユーザーはリアルタイムでデータを表示し、履歴だけのデータなど、クエリの頻度が低い大きなデータセットを使用して作業するときにストレージ領域を節約することができます。  
  
> [!NOTE]  
>  ROLAP を使用すると、結合と GROUP BY 句を組み合わせた場合に、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] から不明なメンバーに関する誤った情報が返される可能性があります。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  により、不明なメンバーの値が返されるのではなく、リレーショナル整合性エラーがなくなります。  
  
 パーティションで ROLAP ストレージ モードを使用し、そのソース データを [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]に格納している場合は、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によってパーティションの集計を格納するためのインデックス付きビューが作成されます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によってインデックス付きビューを作成できない場合、集計テーブルは作成されません。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]でインデックス付きビューを作成するためのセッション要件を処理しますが、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] で集計用にインデックス付きビューを作成するには、ROLAP パーティションとそのスキーマ内のテーブルが次の条件を満たしている必要があります。  
  
-   パーティションには、`Min` または `Max` 集計関数を使用するメジャーを含めることはできません。  
  
-   ROLAP パーティションのスキーマ内の各テーブルは、一度しか使用できません。 たとえば、スキーマに [dbo].[address] AS "Customer Address" と [dbo].[address] AS "SalesRep Address" を含めることはできません。  
  
-   各テーブルは、ビューではなく、テーブルでなければなりません。  
  
-   パーティションのスキーマ内のすべてのテーブル名は、[dbo].[customer] のように、所有者名で修飾する必要があります。  
  
-   パーティションのスキーマ内のすべてのテーブルの所有者が同じである必要があります。たとえば、テーブル [tk].[customer]、[john].[store]、および [dave].[sales_fact_2004] を参照する FROM 句は指定できません。  
  
-   パーティションのメジャーのソース列に NULL 値は許可できません。  
  
-   ビューに使用されるすべてのテーブルは、次のオプションを ON に設定して作成する必要があります。  
  
    -   ANSI_NULLS  
  
    -   QUOTED_IDENTIFIER  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] で使用できるインデックス キーの合計サイズは最大 900 バイトです [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] CREATE INDEX ステートメントが処理されるときに、固定長キー列に基づいてこの条件をアサートします。 ただし、インデックス キーに可変長列がある場合は、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ベース テーブルに対するすべての更新のこの条件をアサートすることもできます。 ビュー定義は集計ごとに異なるため、インデックス付きビューを使用する ROLAP 処理の成否は、集計デザインによって決まります。  
  
-   インデックス付きビューを作成するセッションで、次のオプションが ON に設定が必要です。ARITHABORT、CONCAT_NULL_YEILDS_NULL、QUOTED_IDENTIFIER、ANSI_NULLS、ANSI_PADDING、および ANSI_WARNING します。 これは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で設定できます。  
  
-   インデックス付きビューを作成するセッションで次のオプションを OFF に設定が必要です。NUMERIC_ROUNDABORT します。 これは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で設定できます。  
  
## <a name="holap"></a>HOLAP  
 HOLAP ストレージ モードは、MOLAP と ROLAP の属性を組み合わせたものです。 HOLAP、MOLAP と同様に、多次元構造に格納されるパーティションの集計が原因、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]インスタンス。 ソース データのコピーは格納されません。 パーティションの集計に含まれる要約データにのみアクセスするクエリの場合、HOLAP の応答時間は MOLAP と同程度です。 ソース データにアクセスするクエリ-などアトミック キューブ セルにドリルダウンする場合が存在しない集計データにする必要がありますには、リレーショナル データベースからデータを取得し、ソース データが MOLAP structur に格納されていたかどうかになる同じ速度はできません電子メール。 HOLAP ストレージ モードでは通常、クエリがキャッシュまたは集計から解決されたか、またはソース データ自体から解決されたかに応じてクエリ時間に大きな差が生じます。  
  
 HOLAP として格納されたパーティションのサイズは、ソース データを含まないため、同程度の MOLAP パーティションより小さく、要約データにアクセスするクエリの応答時間は ROLAP パーティションより高速です。 一般的に、要約データが大量のソース データで構成され、クエリに高速な応答が要求されるキューブのパーティションには、HOLAP ストレージ モードが適しています。 ただし、中央値の計算のようにリーフ レベル データを処理する必要のあるクエリをユーザーが生成する場合は、MOLAP の方が適しています。  
  
## <a name="see-also"></a>参照  
 [プロアクティブ キャッシュ&#40;パーティション&#41;](partitions-proactive-caching.md)   
 [Analysis Services データベースの同期](../multidimensional-models/synchronize-analysis-services-databases.md)   
 [パーティション (Analysis Services - 多次元データ)](partitions-analysis-services-multidimensional-data.md)  
  
  
