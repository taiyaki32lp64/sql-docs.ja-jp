---
title: 集計変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.aggregatetrans.f1
helpviewer_keywords:
- IsBig property
- aggregate functions [Integration Services]
- Aggregate transformation [Integration Services]
- large data, SSIS transformations
ms.assetid: 2871cf2a-fbd3-41ba-807d-26ffff960e81
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4759050a9453e1925ea47bc3dbf66d13aa821feb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770638"
---
# <a name="aggregate-transformation"></a>集計変換
  集計変換は Average などの集計関数を列の値に適用し、その結果を変換出力にコピーします。 集計変換では、集計関数の他に GROUP BY 句を使用して集計範囲のグループを指定できます。  
  
## <a name="operations"></a>操作  
 集計変換では、次の操作がサポートされています。  
  
|操作|説明|  
|---------------|-----------------|  
|グループ化|データセットをグループに分割します。 グループ化には、任意のデータ型の列を使用できます。 詳細については、「[GROUP BY (Transact-SQL)](/sql/t-sql/queries/select-group-by-transact-sql)」を参照してください。|  
|Sum|列内の値を合計します。 numeric データ型を持つ列のみ、合計することができます。 詳細については、「[SUM (Transact-SQL)](/sql/t-sql/functions/sum-transact-sql)」を参照してください。|  
|平均|列内の列値の平均を返します。 numeric データ型を持つ列のみ、平均値を計算することができます。 詳細については、「[AVG (Transact-SQL)](/sql/t-sql/functions/avg-transact-sql)」を参照してください。|  
|Count|グループ内のアイテムの数を返します。 詳細については、「[COUNT (Transact-SQL)](/sql/t-sql/functions/count-transact-sql)」を参照してください。|  
|個別のカウント|グループ内の NULL でない一意の値の数を返します。|  
|最小|グループ内の最小値を返します。 詳細については、「[MIN (Transact-SQL)](/sql/t-sql/functions/min-transact-sql)」を参照してください。 Transact-SQL MIN 関数とは異なり、この操作は数値、日付、および時間データ型に対してのみ使用できます。|  
|[最大]|グループ内の最大値を返します。 詳細については、「[MAX (Transact-SQL)](/sql/t-sql/functions/max-transact-sql)」を参照してください。 Transact-SQL MAX 関数とは異なり、この操作は数値、日付、および時間データ型に対してのみ使用できます。|  
  
 集計変換では、NULL 値を、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リレーショナル データベース エンジンと同じ方法で処理します。 この動作は SQL-92 標準で定義されています。 この場合に当てはまる規則を以下に示します。  
  
-   GROUP BY 句では、他の列の値と同様に NULL が処理されます。 グループ化に使われる列に複数の NULL 値が含まれる場合は、それらの NULL 値が 1 つのグループになります。  
  
-   COUNT (列名) および COUNT (DISTINCT 列名) 関数では、NULL は無視され、名前付き列内の NULL 値を含む行が結果から除外されます。  
  
-   COUNT (*) 関数では、NULL 値の行を含め、すべての行がカウントされます。  
  
## <a name="big-numbers-in-aggregates"></a>集計における大きな数値  
 大きな数値または大きな有効桁数が必要な列がある場合は、特別な注意が必要です。 集計変換には、IsBig プロパティが含まれています。このプロパティを使用すると、出力列で、大きな数値または大きな有効桁数の数値に対し、特別な処理を実行するように設定できます。 列の値が 40 億を超える場合、または float データ型よりも大きな有効桁数が必要な場合は、IsBig を 1 に設定する必要があります。  
  
 IsBig プロパティを 1 に設定すると、集計変換の出力は、次のような影響を受けます。  
  
-   DT_R4 データ型の代わりに DT_R8 データ型が使用されます。  
  
-   カウントの結果は、DT_UI8 データ型として格納されます。  
  
-   個別のカウントの結果は、DT_UI4 データ型として格納されます。  
  
> [!NOTE]  
>  グループ化、最大、または最小操作で使用される列では、IsBig を 1 に設定することはできません。  
  
## <a name="performance-considerations"></a>パフォーマンスに関する考慮事項  
 集計変換には、変換のパフォーマンスが向上するように設定できる、プロパティのセットが含まれています。  
  
-   **グループ化** 操作を実行する場合は、コンポーネントとコンポーネント出力の Keys プロパティまたは KeysScale プロパティを設定します。 Keys を使用すると、変換で処理されるキーの正確な数を指定できます (ここでは、Keys は、**グループ化**操作の結果として予想されるグループの数を示します)。KeysScale を使用すると、キーの概数を指定できます。 Keys または KeysScale に適切な値を指定すると、変換時にキャッシュされるデータ用に十分なメモリが割り当てられるようになるため、パフォーマンスが向上します。  
  
-   **個別のカウント** 操作を実行するときは、コンポーネントの CountDistinctKeys プロパティまたは CountDistinctScale プロパティを設定します。 CountDistinctKeys を使用すると、変換時に個別のカウント操作で処理されるキーの正確な数を指定できます (ここでは、CountDistinctKeys は、**個別のカウント**操作の結果として予想される個別の値の数を示します)。CountDistinctScale を使用すると、個別のカウントの操作で処理するキーの概数を指定できます。 CountDistinctKeys または CountDistinctScale に適切な値を指定すると、変換時にキャッシュされるデータ用に十分なメモリが割り当てられるようになるため、パフォーマンスが向上します。  
  
## <a name="aggregate-transformation-configuration"></a>集計変換の構成  
 集計変換は、変換、出力、および列の各レベルで構成します。  
  
-   変換レベルでは、次の値を指定することにより、集計変換を構成してパフォーマンスを高めることができます。  
  
    -   **グループ化** 操作の結果として予想されるグループの数。  
  
    -   **個別のカウント** 操作の結果として予想される個別の値の数。  
  
    -   集計の際にメモリを拡張できる割合。  
  
     また、除数の値が 0 のときに失敗せずに警告を生成するように、集計変換を構成することもできます。  
  
-   出力レベルでは、 **グループ化** 操作の結果として予想されるグループの数を指定することにより、集計変換を構成してパフォーマンスを高めることができます。 集計変換では複数の出力を設定して、各列を個別に構成できます。  
  
-   列レベルでは、次の値を指定します。  
  
    -   列が実行する集計。  
  
    -   集計の比較オプション。  
  
 また、次の値を指定することにより、集計変換を構成してパフォーマンスを高めることもできます。  
  
-   列に対する **グループ化** 操作の結果として予想されるグループの数。  
  
-   列に対する **個別のカウント** 操作の結果として予想される個別の値の数。  
  
 列に含まれる数値が大きい場合、または数値の有効桁数が大きい場合には、その列を IsBig として識別することもできます。  
  
 集計変換は非同期です。つまり、行ごとにデータを使用またはパブリッシュしません。 集計変換は行セット全体を使用してグループ化と集計を実行し、その結果をパブリッシュします。  
  
 この変換では列をパススルーすることはなく、変換によりパブリッシュされるデータ用に、新しい列がデータ フロー内に作成されます。 集計関数が適用される入力列、または変換がグループ化用に使用する入力列のみが、変換出力にコピーされます。 たとえば、集計変換入力に次の 3 つの列があるものとします: **CountryRegion**、**City**、**Population**。 集計変換は、 **CountryRegion** 列によりグループ化を行い、 関数を **Population** 列に適用します。 したがって、出力には **City** 列は含まれません。  
  
 また、複数の出力を集計変換に追加し、各集計を別々の出力に送ることもできます。 たとえば、集計変換が Sum および Average 関数を適用する場合に、各集計をそれぞれ別の出力に送ることができます。  
  
 1 つの入力列に複数の集計を適用できます。 たとえば、 **Sales**という名前の入力列の合計値と平均値を計算する場合に、Sum および Average 関数の両方を **Sales** 列に適用するように、集計変換を構成できます。  
  
 集計変換は、1 つの入力と 1 つ以上の出力をとります。 エラー出力はサポートされていません。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[集計変換エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[集計変換エディター] ([集計] タブ)](../../aggregate-transformation-editor-aggregations-tab.md)  
  
-   [[集計変換エディター] ([詳細設定] タブ)](../../aggregate-transformation-editor-advanced-tab.md)  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../../common-properties.md)  
  
-   [変換のカスタム プロパティ](transformation-custom-properties.md)  
  
 プロパティの設定方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   [集計変換を使用してデータセットの値を集計する](aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
-   [データ フロー コンポーネントのプロパティを設定する](../set-the-properties-of-a-data-flow-component.md)  
  
-   [マージ変換およびマージ結合変換用にデータを並べ替える](sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [集計変換を使用してデータセットの値を集計する](aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
## <a name="see-also"></a>参照  
 [データ フロー](../data-flow.md)   
 [Integration Services の変換](integration-services-transformations.md)  
  
  
