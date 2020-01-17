---
title: 集計のデザイン (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- statistical information [XML for Analysis]
- batches [XML for Analysis]
- aggregations [Analysis Services], XML for Analysis
- XMLA, aggregations
- queries [XMLA]
- XML for Analysis, aggregations
- iterative aggregation process [XMLA]
ms.assetid: 4dd27afa-10c7-408d-bc24-ca74217ddbcb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 81450789395dfef84f81896990fa251514d3489e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62702123"
---
# <a name="designing-aggregations-xmla"></a>集計のデザイン (XMLA)
  集計デザインは、集計の格納時に複数のパーティションで同じ構造を確実に使用するようにするため、特定のメジャー グループのパーティションに関連付けられるものです。 使用して後でマージできるパーティションを簡単に定義することができるパーティションに対して同じストレージ構造を使用して、 [MergePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla)コマンド。 集計デザインの詳細については、次を参照してください。[集計と集計デザイン](../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)します。  
  
 使用することができます、集計デザインの集計を定義する、 [DesignAggregations](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/designaggregations-element-xmla) XML for Analysis (XMLA) コマンド。 `DesignAggregations` コマンドには、参照として使用する集計デザインを識別し、その参照に基づいたデザイン プロセスを制御するためのプロパティがあります。 `DesignAggregations` コマンドとそのプロパティを使用すると、集計を反復処理またはバッチ処理でデザインし、その結果のデザイン統計を表示してデザイン プロセスを評価することができます。  
  
## <a name="specifying-an-aggregation-design"></a>集計デザインの指定  
 [オブジェクト](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)のプロパティ、`DesignAggregations`コマンドは、既存の集計デザインへのオブジェクト参照を含める必要があります。 オブジェクト参照には、データベース識別子、キューブ識別子、メジャー グループ識別子、および集計デザイン識別子が含まれます。 既存の集計デザインがない場合、エラーが発生します。  
  
## <a name="controlling-the-design-process"></a>デザイン プロセスの制御  
 `DesignAggregations` コマンドの以下のプロパティを使用して、集計デザインに対応した集計を定義するために使用するアルゴリズムを制御できます。  
  
-   [手順](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/steps-element-xmla)プロパティは、反復回数を指定します、`DesignAggregations`コントロールをクライアント アプリケーションに返す前にコマンドを実行する必要があります。  
  
-   [時間](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/time-element-xmla)プロパティは、ミリ秒数を決定します。、`DesignAggregations`コントロールをクライアント アプリケーションに返す前にコマンドを実行する必要があります。  
  
-   [最適化](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/optimization-element-xmla)プロパティは、パフォーマンス向上の推定割合を決定します。、`DesignAggregations`達成を図るコマンド。 集計を反復的にデザインする場合、このプロパティは最初のコマンドで送信するだけで十分です。  
  
-   [ストレージ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/storage-element-xmla)プロパティで使用されるバイト単位のディスク ストレージの推定量を決定する、`DesignAggregations`コマンド。 集計を反復的にデザインする場合、このプロパティは最初のコマンドで送信するだけで十分です。  
  
-   [具体化](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/materialize-element-xmla)プロパティを決定するかどうか、`DesignAggregations`コマンドは、デザイン プロセス中に定義されている集計を作成する必要があります。 集計を反復的にデザインする場合、デザインした集計を保存する用意ができるまで、このプロパティは false に設定しておく必要があります。 true に設定した場合、現在のデザイン プロセスが終了し、定義された集計は指定した集計デザインに追加されます。  
  
## <a name="specifying-queries"></a>クエリを指定します。  
 DesignAggregations コマンドは、1 つまたは複数を含めることによって最適化の使用量ベースのコマンドをサポートしている`Query`内の要素、[クエリ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/queries-element-xmla)プロパティ。 `Queries`プロパティは、1 つまたは複数含めることができます[クエリ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/query-element-xmla)要素。 `Queries` プロパティに `Query` 要素が含まれていない場合、`Object` 要素で指定された集計デザインでは、一般的な集計のセットを含む既定の構造が使用されます。 この一般的な集計のセットは、`Optimization` コマンドの `Storage` および `DesignAggregations` プロパティで指定される条件を満たすようにデザインされています。  
  
 各 `Query` 要素は、最もよく使用するクエリを対象とする集計を定義するためにデザイン プロセスが使用する、目標クエリを表します。 ユーザー独自のクエリを指定することもできますが、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスによってクエリ ログに格納されている情報を使用して、最もよく使用されるクエリに関する情報を取得することもできます。 使用法に基づく最適化ウィザードでは、`DesignAggregations` コマンドの送信時にクエリ ログを使用して、時間、使用法、または指定されたユーザーに基づいて目標クエリを取得します。 詳細については、次を参照してください。[使用法に基づく最適化ウィザードの F1 ヘルプ](../usage-based-optimization-wizard-f1-help.md)します。  
  
 集計を反復的にデザインする場合、目標クエリは最初の `DesignAggregations` コマンドで送信するだけで十分です。これは、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスがこれらの目標クエリを保存し、後続の `DesignAggregations` コマンドでそれらのクエリを使用するためです。 反復処理の最初の `DesignAggregations` コマンドで目標クエリを渡した場合、後続の `DesignAggregations` コマンドの `Queries` プロパティに目標クエリが含まれていると、エラーが発生します。  
  
 `Query` 要素には、以下の引数を含むコンマ区切りの値が含まれます。  
  
 *Frequency*,*Dataset*[,*Dataset*...]  
  
 *頻度*  
 クエリが以前に実行された回数に対応する重み係数です。 場合、`Query`要素、新しいクエリを表す、*頻度*値は、クエリを評価する、デザイン プロセスによって使用される重み係数を表します。 この値が大きいほど、デザイン プロセスでクエリに対して付けられる重みが増加します。  
  
 *データセット*  
 ディメンション内のどの属性をクエリに含めるかを指定する数値文字列です。 この文字列の文字数は、ディメンション内の属性の数と一致している必要があります。 0 は、その位置にある属性が、指定されたディメンションのクエリに含まれないことを示します。1 は、その位置にある属性が、指定されたディメンションのクエリに含まれることを示します。  
  
 たとえば文字列 "011" は、3 つの属性を持つディメンションを処理するクエリの中に、2 番目と 3 番目の属性が含まれることを示しています。  
  
> [!NOTE]  
>  いくつかの属性は、データセットでの考慮の対象から除外されます。 除外された属性の詳細については、次を参照してください。 [Query 要素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/query-element-xmla)します。  
  
 集計デザインを含むメジャー グループ内の各ディメンションがによって表される、*データセット*値、`Query`要素。 *Dataset* の値の順序は、メジャー グループに含まれるディメンションの順序と一致している必要があります。  
  
## <a name="designing-aggregations-using-iterative-or-batch-processes"></a>反復処理またはバッチ処理を使用した集計のデザイン  
 `DesignAggregations` コマンドは、デザイン プロセスで必要な対話性に応じて、反復処理またはバッチ処理の一部として使用することができます。  
  
### <a name="designing-aggregations-using-an-iterative-process"></a>反復処理を使用した集計のデザイン  
 集計を反復処理によってデザインするには、複数の `DesignAggregations` コマンドを送信して、デザイン プロセスを細かく制御します。 集計のデザイン ウィザードでも、同じアプローチを使用してデザイン プロセスを細かく制御します。 詳細については、次を参照してください。[集計デザイン ウィザードの F1 ヘルプ](../aggregation-design-wizard-f1-help.md)します。  
  
> [!NOTE]  
>  集計を反復処理によってデザインするには、明示的なセッションが必要です。 明示的なセッションの詳細については、次を参照してください。[接続の管理とセッション&#40;XMLA&#41;](managing-connections-and-sessions-xmla.md)します。  
  
 反復処理を開始するには、最初に以下の情報を含む `DesignAggregations` コマンドを送信します。  
  
-   `Storage` および `Optimization` プロパティの値。これが、デザイン プロセス全体での設定になります。  
  
-   `Steps` および `Time` プロパティの値。これに基づいて、デザイン プロセスの最初のステップが制限されます。  
  
-   (使用法に基づく最適化を行う場合) 目標クエリを含む `Queries` プロパティ。これが、デザイン プロセス全体での設定になります。  
  
-   `Materialize` プロパティは、false に設定します。 このプロパティを false に設定することは、コマンドの完了時に、定義された集計がデザイン プロセスによって集計デザインに保存されないことを意味します。  
  
 最初の `DesignAggregations` コマンドが終了すると、コマンドはデザインの統計を含む行セットを返します。 これらのデザインの統計を評価して、デザイン プロセスを継続するか、あるいは終了するかを判断することができます。 プロセスを継続する場合は、次の `DesignAggregations` コマンドを送信します。そのコマンドには、デザイン プロセスのこのステップを制限するための `Steps` および `Time` の値を含めます。 そして結果の統計を評価し、デザイン プロセスを継続すべきかどうかを判断します。 このように、`DesignAggregations` コマンドを送信してその結果を評価するプロセスを、目標に到達して集計の適切なセットが定義されるまで繰り返します。  
  
 目標の集計のセットに到達したら、最後の `DesignAggregations` コマンドを送信します。 この最後の `DesignAggregations` コマンドでは、`Steps` プロパティを 1 に設定し、`Materialize` プロパティを true に設定します。 これらの設定により、この最後の `DesignAggregations` コマンドはデザイン プロセスを終了し、定義された集計を集計デザインに保存します。  
  
### <a name="designing-aggregations-using-a-batch-process"></a>バッチ処理を使用した集計のデザイン  
 集計のデザインは、単一の `DesignAggregations` コマンドを送信することにより、バッチ処理を使用して行うこともできます。そのコマンドには、デザイン プロセス全体の設定となり制限する `Steps`、`Time`、`Storage`、および `Optimization` プロパティの値を含めます。 使用法に基づく最適化を行う場合は、`Queries` プロパティに、デザイン プロセスの対象となる目標クエリを含める必要があります。 また、コマンドの終了時に、定義された集計がデザイン プロセスによって集計デザインに保存されるように、`Materialize` を true に設定します。  
  
 バッチ処理による集計のデザインは、暗黙のセッションまたは明示的なセッションのいずれでも行うことができます。 暗黙的および明示的なセッションの詳細については、次を参照してください。[接続の管理とセッション&#40;XMLA&#41;](managing-connections-and-sessions-xmla.md)します。  
  
## <a name="returning-design-statistics"></a>デザインの統計を返す処理  
 `DesignAggregations` コマンドは、クライアント アプリケーションに制御を返すときに、そのコマンドに関するデザインの統計を表す 1 つの行を含む行セットを返します。 行セットに含まれる列は、次の表のとおりです。  
  
|[列]|データ型|説明|  
|------------|---------------|-----------------|  
|手順|Integer|クライアント アプリケーションに制御を返すまでに、コマンドによって行われたステップの数です。|  
|Time|Long integer|クライアント アプリケーションに制御を返すまでに、コマンドで経過したミリ秒単位の時間です。|  
|Optimization|Double|クライアント アプリケーションに制御を返すまでに、コマンドによって達成されたパフォーマンス向上率の予測値です。|  
|ストレージ|Long integer|クライアント アプリケーションに制御を返すまでに、コマンドによって使用されたバイト数の予測値です。|  
|集計|Long integer|クライアント アプリケーションに制御を返すまでに、コマンドによって定義された集計の数です。|  
|LastStep|ブール値|行セット内のデータがデザイン プロセス内の最後のステップを表しているかどうかを示します。 コマンドの `Materialize` プロパティが true に設定されている場合、この列の値が true に設定されます。|  
  
 各 `DesignAggregations` コマンドの後に返される行セットに含まれるデザインの統計は、反復処理によるデザインとバッチ処理によるデザインの両方で使用できます。 反復処理によるデザインの場合、進行状況の判別と表示を行うために、デザインの統計を使用できます。 集計をバッチ処理によってデザインする場合は、コマンドによって作成された集計の数を判断するために、デザインの統計を使用できます。  
  
## <a name="see-also"></a>参照  
 [Analysis Services での XMLA による開発](developing-with-xmla-in-analysis-services.md)  
  
  
