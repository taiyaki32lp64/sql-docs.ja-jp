---
title: あいまいグループ化変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzygroupingtrans.f1
helpviewer_keywords:
- cleaning data
- comparing data
- token delimiters [Integration Services]
- temporary indexes [Integration Services]
- Fuzzy Grouping transformation
- temporary tables [Integration Services]
- grouping data
- standardizing data [Integration Services]
- columns [Integration Services], standardizing
- similarity thresholds [Integration Services]
- data cleaning [Integration Services]
- duplicate data [Integration Services]
ms.assetid: e43f17bd-9d13-4a8f-9f29-cce44cac1025
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 41ac7c11824457bd6d93a062344eb3b411c95b3e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62900561"
---
# <a name="fuzzy-grouping-transformation"></a>あいまいグループ化変換
  あいまいグループ化変換は、重複部分と考えられるデータの行を識別し、データを標準化するときに使用するデータの正規行を選択することで、データ クリーニング タスクを実行します。  
  
> [!NOTE]  
>  パフォーマンスやメモリの制限など、あいまいグループ化変換に関する詳細については、ホワイト ペーパー「 [Fuzzy Lookup and Fuzzy Grouping in SQL Server Integration Services 2005](https://go.microsoft.com/fwlink/?LinkId=96604)」(SQL Server Integration Services 2005 のあいまい参照とあいまいグループ化) をご覧ください。  
  
 あいまいグループ化変換では、変換アルゴリズムの処理に必要な一時 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] テーブルを作成するために、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスへの接続が必要になります。 接続時には、データベース内にテーブルを作成する権限を持つユーザーの解決が必要です。  
  
 変換を構成する場合は、重複部分を識別するときに使用する入力列を選択し、一致の種類としてあいまい一致か完全一致かを列ごとに選択する必要があります。 完全一致の場合は、その列に同じ値を持つ行のみがグループ化されます。 完全一致は、DT_TEXT、DT_NTEXT、および DT_IMAGE を除く任意の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] データ型の列に適用できます。 あいまい一致の場合は、ほぼ同じ値を持つ行がグループ化されます。 データのあいまい一致は、ユーザーが指定する類似性スコアに基づいて判定されます。 あいまい一致に使用できるのは、DT_WSTR データ型および DT_STR データ型の列のみです。 詳細については、「 [Integration Services Data Types](../integration-services-data-types.md)」を参照してください。  
  
 変換出力には、すべての入力列、標準化されたデータを含む 1 つ以上の列、および類似性スコアを含む 1 つの列が含まれます。 スコアは、0 ～ 1 の 10 進値です。 正規行のスコアは 1 です。 あいまいグループ内の他の行は、その行がどれだけ正規行に一致するかを示すスコアを持ちます。 スコアが 1 に近いほど、その行と正規行との類似性が高いことを示しています。 正規行と完全に重複する行があいまいグループに含まれている場合、その行のスコアは 1 となります。 この変換では、重複行は削除されません。この変換では、正規行を類似の行に関連付けるキーを作成して、行をグループ化します。  
  
 この変換では、入力行ごとに、次の列が追加された 1 つの出力行が生成されます。  
  
-   **_key_in**。各行を一意に識別する列です。  
  
-   **_key_out**。重複行のグループを識別する列です。 **_key_out** 列は、正規データ行の **_key_in** 列の値を含みます。 **_key_out** の値が同じ行は、同じグループに属します。 グループの **_key_out**値は、正規データ行の **_key_in** の値に対応します。  
  
-   **_score**。入力行と正規行との類似性を示す、0 ～ 1 の値です。  
  
 これらは既定の列名であり、別の名前を使用するようにあいまいグループ化変換を構成することもできます。 その場合、あいまいグループ化に含まれるそれぞれの列に関する類似性スコアも出力されます。  
  
 あいまいグループ化変換には、グループ化をカスタマイズするための 2 つの機能として、トークン区切り記号と類似性しきい値があります。 この変換には、データをトークン化に使用される既定の区切り記号のセットがありますが、データのトークン化を向上する新しい区切り記号も追加できます。  
  
 類似性しきい値とは、変換で重複を識別する際の厳密さのレベルを示します。 類似性しきい値は、コンポーネント レベルおよび列レベルで設定できます。 列レベルの類似性しきい値は、あいまい一致を実行する列に対してのみ使用できます。 類似性の範囲は 0 ～ 1 です。 しきい値が 1 に近いほど、行や列が一致していると判断される場合の類似性が高くなります。 行および列の類似性しきい値を指定するには、コンポーネント レベルまたは列レベルで MinSimilarity プロパティを設定します。 コンポーネント レベルで指定された類似性を満たすためには、すべての列のすべての行において、コンポーネント レベルで指定された類似性しきい値以上の類似性が求められます。  
  
 あいまいグループ化変換では、類似性の内部メジャーが計算され、MinSimilarity に指定された値に満たない行はグループ化されません。  
  
 データに適した類似性しきい値を求めるには、最小類似性しきい値をその都度変えて何回かあいまいグループ化変換を試す必要があります。 実行時には、変換出力のスコア列に、グループの各行の類似性スコアが格納されます。 これらの値を使用すると、データに適した類似性しきい値を識別できます。 類似性を高く設定するには、スコア列の値よりも大きい値を MinSimilarity に設定します。  
  
 あいまいグループ化変換の入力の列のプロパティを設定することで、この変換で実行されるグループ化をカスタマイズできます。 たとえば、FuzzyComparisonFlags プロパティは、変換で列の文字列データを比較する方法を指定します。ExactFuzzy プロパティは、変換であいまい一致または完全一致を実行するかどうかを指定します。  
  
 あいまいグループ化変換で使用されるメモリの量は、MaxMemoryUsage カスタム プロパティを設定することによって構成できます。 メガバイト (MB) 単位の数値または 0 を指定できます。0 を指定すると、変換に必要なメモリの量と使用できる物理メモリの量に基づいて、変換に使用されるメモリの量が動的に決まります。 MaxMemoryUsage カスタム プロパティは、パッケージの読み込み時にプロパティ式で更新できます。 詳しくは、「[Integration Services &#40;SSIS&#41; の式](../../expressions/integration-services-ssis-expressions.md)」、「[パッケージでプロパティ式を使用する](../../expressions/use-property-expressions-in-packages.md)」、および「[変換のカスタム プロパティ](transformation-custom-properties.md)」をご覧ください。  
  
 この変換は 1 つの入力と 1 つの出力をとります。 エラー出力はサポートされていません。  
  
## <a name="row-comparison"></a>行の比較  
 あいまいグループ化変換を構成するときに、変換入力内の行の比較に使用する比較アルゴリズムを指定できます。 Exhaustive プロパティを設定する場合`true`、変換入力内の他のすべての行に入力されたすべての行を比較します。 この比較アルゴリズムを使用すると、より正確な結果が生成されますが、入力の行の数が少ない場合を除けば、処理により多くの時間がかかるようになります。 パフォーマンスの問題を回避するためには、Exhaustive プロパティを設定することをお勧め`true`パッケージ開発時にのみです。  
  
## <a name="temporary-tables-and-indexes"></a>一時テーブルおよびインデックス  
 実行時、あいまいグループ化変換は、テーブルやインデックスなどの一時オブジェクトを接続先の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースに作成します。この一時オブジェクトのサイズは、かなり大きくなる可能性があります。 テーブルおよびインデックスのサイズは、変換入力内の行の数およびあいまいグループ化変換によって作成されたトークンの数に比例します。  
  
 また、変換は一時テーブルに対してクエリを実行します。 このため、特に稼働サーバーのディスク容量が少ない場合は、あいまいグループ化変換を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の非稼働インスタンスに接続することを検討してください。  
  
 この変換で使用するテーブルおよびインデックスがローカル コンピューター上にあると、変換のパフォーマンスが向上する可能性があります。  
  
## <a name="configuration-of-the-fuzzy-grouping-transformation"></a>あいまいグループ化変換の構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[あいまいグループ化変換エディター]** ダイアログ ボックスを使用して設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[あいまいグループ化変換エディター] &#40;[接続マネージャー] タブ&#41;](../../fuzzy-grouping-transformation-editor-connection-manager-tab.md)  
  
-   [[あいまいグループ化変換エディター] &#40;[列] タブ&#41;](../../fuzzy-grouping-transformation-editor-columns-tab.md)  
  
-   [[あいまいグループ化変換エディター] &#40;[詳細設定] タブ&#41;](../../fuzzy-grouping-transformation-editor-advanced-tab.md)  
  
 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../../common-properties.md)  
  
-   [変換のカスタム プロパティ](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 このタスクのプロパティの設定方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   [あいまいグループ化変換を使用して類似のデータ行を識別する](fuzzy-grouping-transformation.md)  
  
-   [データ フロー コンポーネントのプロパティを設定する](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="see-also"></a>参照  
 [あいまい参照変換](lookup-transformation.md)   
 [Integration Services の変換](integration-services-transformations.md)  
  
  
