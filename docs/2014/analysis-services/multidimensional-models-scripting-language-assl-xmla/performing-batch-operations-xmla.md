---
title: バッチ操作 (XMLA) の実行 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- multiple projects
- XML for Analysis, batches
- parallel batch execution [XMLA]
- transactional batches
- serial batch execution [XMLA]
- XMLA, batches
- batches [XML for Analysis]
- nontransactional batches
ms.assetid: 731c70e5-ed51-46de-bb69-cbf5aea18dda
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2bd661506dbb792eb55194c61d7284d619e63a5f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62702062"
---
# <a name="performing-batch-operations-xmla"></a>バッチ操作の実行 (XMLA)
  使用することができます、[バッチ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)XML for Analysis (XMLA) 単一の XMLA を使用して複数の XMLA コマンドを実行するコマンド[Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)メソッド。 `Batch` コマンドに含まれる複数のコマンドは、単一のトランザクションとして実行することも、あるいはコマンドごとに別個のトランザクションとして直列または並列で実行することもできます。 アウトオブ ライン バインドおよびその他のプロパティを指定することも、`Batch`の複数の処理コマンド[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]オブジェクト。  
  
## <a name="running-transactional-and-nontransactional-batch-commands"></a>トランザクションおよび非トランザクション バッチ コマンドの実行  
 `Batch` コマンドは、コマンドを以下の 2 つのいずれかの方法で実行します。  
  
 **トランザクション**  
 場合、`Transaction`の属性、`Batch`コマンドの設定を true に、`Batch`コマンド実行コマンドのすべてのコマンドに含まれる、`Batch`トランザクションを 1 つのコマンド*トランザクション*バッチ。  
  
 トランザクション バッチで任意のコマンドが失敗した場合[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のいずれかのコマンドはロールバック、`Batch`失敗したコマンドの前に実行されたコマンドに対して、`Batch`コマンドを直ちに終了します。 `Batch` コマンド内でまだ実行されていないコマンドはいずれも実行されません。 `Batch` コマンドが終了した後、`Batch` コマンドは失敗したコマンドについて発生したすべてのエラーを報告します。  
  
 **非トランザクション**  
 場合、`Transaction`属性が false に設定、`Batch`コマンドに含まれる各コマンドを実行、`Batch`コマンドを個別のトランザクションを*非トランザクション*バッチ。 非トランザクション バッチ内のいずれかのコマンドが失敗した場合、`Batch` コマンドは、失敗したコマンドの後にあるコマンドの実行を続行します。 `Batch` コマンドが、`Batch` コマンドに含まれるすべてのコマンドの実行を試みた後、`Batch` コマンドは発生したすべてのエラーを報告します。  
  
 `Batch` コマンドに含まれるコマンドが返す結果はすべて、それらのコマンドが `Batch` コマンド内に含まれている順序と同じ順序で返されます。 `Batch` コマンドによって返される結果は、`Batch` コマンドがトランザクション バッチまたは非トランザクション バッチのいずれであるかによって異なります。  
  
> [!NOTE]  
>  場合、`Batch`コマンドにはなどの出力を返さないコマンドが含まれています、[ロック](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)コマンドと、コマンドが正常に実行を`Batch`コマンドは、空白を返します[ルート](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla)要素内の結果の要素。 空の `root` 要素があることにより、`Batch` コマンドに含まれるそれぞれのコマンドが、そのコマンドの結果の適切な `root` 要素と確実に対応します。  
  
### <a name="returning-results-from-transactional-batch-results"></a>トランザクション バッチの結果から結果を返す処理  
 トランザクション バッチ内で実行されたコマンドの結果は、`Batch` コマンド全体が完了するまで返されません。 それぞれのコマンドが実行された後に結果が返されないのは、トランザクション バッチ内のいずれかのコマンドが失敗すれば、`Batch` コマンド全体、および含まれるすべてのコマンドがロールバックされるためです。 すべてのコマンドを開始して正常に実行すると、[を返す](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/return-element-xmla)の要素、 [ExecuteResponse](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects-executeresponse)によって返される要素、`Execute`のメソッド、`Batch`コマンドには 1 つ[結果](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/results-element-xmla)要素、1 つを格納する`root`要素に含まれている正常に実行コマンドごとに、`Batch`コマンド。 `Batch` コマンド内のいずれかのコマンドが起動できない場合、または完了に失敗した場合、`Execute` メソッドは、失敗したコマンドのエラーを含む SOAP エラーを `Batch` コマンドについて返します。  
  
### <a name="returning-results-from-nontransactional-batch-results"></a>非トランザクション バッチの結果から結果を返す処理  
 非トランザクション バッチ内のコマンドによる結果は、それらのコマンドが `Batch` コマンド内に含まれている順序で、各コマンドごとに返されます。 `Batch` コマンド内のいずれのコマンドも正常に起動できなかった場合、`Execute` メソッドは、その `Batch` コマンドについてのエラーを含む SOAP エラーを返します。 少なくとも 1 つのコマンドが正常に起動された場合、その `return` コマンドに対する `ExecuteResponse` メソッドによって返される `Execute` 要素の `Batch` 要素には、1 つの `results` 要素が含まれます。この要素には、`root` コマンドに含まれる各コマンドに対して 1 つの `Batch` 要素が含まれています。 非トランザクション バッチ内の 1 つまたは複数のコマンドが開始することはできませんまたは完了するには失敗した場合、`root`その失敗したコマンドの要素が含まれています、[エラー](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla)エラーを説明する要素。  
  
> [!NOTE]  
>  非トランザクション バッチ内の少なくとも 1 つのコマンドが起動できれば、その非トランザクション バッチに含まれるすべてのコマンドが `Batch` コマンドの結果にエラーを返した場合であっても、その非トランザクション バッチは正常に実行されたものと見なされます。  
  
## <a name="using-serial-and-parallel-execution"></a>直列および並列実行の使用  
 `Batch` コマンドでは、含まれるコマンドを直列または並列で実行することができます。 コマンドが直列に実行される場合、`Batch` コマンド内に含まれる次のコマンドは、`Batch` コマンド内で現在実行中のコマンドが完了するまで起動できません。 コマンドが並列で実行される場合、`Batch` によって複数のコマンドを同時に実行することができます。  
  
 並行して実行するコマンドを追加するコマンドを並列で実行する、[並列](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/parallel-element-xmla)のプロパティ、`Batch`コマンド。 現時点では、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]だけなは、シーケンシャルに実行できる[プロセス](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)コマンドを並列でします。 などの他の任意の XMLA コマンド[作成](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)または[Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)に含まれる、`Parallel`プロパティが連続して実行します。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、`Process` プロパティに含まれるすべての `Parallel` コマンドの並列実行を試みますが、すべての `Process` コマンドが並列で実行されるとは限りません。 各 `Process` コマンドはインスタンスによって分析され、並列で実行できないとインスタンスが判断した `Process` コマンドは直列に実行されます。  
  
> [!NOTE]  
>  コマンドを並行で実行する場合は、`Transaction` コマンドの `Batch` 属性を true に設定する必要があります。これは、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によってサポートされるアクティブなトランザクションは接続ごとに 1 つだけであるのに対し、非トランザクション バッチは各コマンドを個別のトランザクションで実行するためです。 非トランザクション バッチに `Parallel` プロパティを含めると、エラーが発生します。  
  
### <a name="limiting-parallel-execution"></a>並列実行の制限  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスは、インスタンスが実行されているコンピューターの制限範囲で、可能な限り多くの `Process` コマンドを並列で実行しようとします。 同時に実行する `Process` コマンドの数は、`maxParallel` プロパティの `Parallel` 属性を、並列で実行できる `Process` コマンドの最大数を示す値に設定することにより制限できます。  
  
 たとえば、`Parallel` プロパティに以下の順序でコマンドが含まれているとします。  
  
1.  `Create`  
  
2.  `Process`  
  
3.  `Alter`  
  
4.  `Process`  
  
5.  `Process`  
  
6.  `Process`  
  
7.  `Delete`  
  
8.  `Process`  
  
9. `Process`  
  
 この `maxParalle` プロパティの `Parallel` 属性は 2 に設定されています。 そのため、インスタンスは上のコマンドの一覧を以下の説明のとおりに実行します。  
  
-   コマンド 1 は直列に実行されます。コマンド 1 は `Create` コマンドであり、並列で実行できるのは `Process` コマンドだけであるためです。  
  
-   コマンド 1 が完了した後、コマンド 2 は直列に実行されます。  
  
-   コマンド 2 が完了した後、コマンド 3 は直列に実行されます。  
  
-   3 のコマンドが完了した後、コマンド 4 と 5 は並列で実行します。 コマンド 6 も `Process` コマンドですが、`maxParallel` プロパティが 2 に設定されているため、コマンド 6 がコマンド 4 と 5 と共に並行で実行されることはありません。  
  
-   コマンド 6 は、コマンド 4 とコマンド 5 の両方が完了した後に直列に実行されます。  
  
-   コマンド 7 はコマンド 6 の完了後に直列に実行されます。  
  
-   コマンド 8 と 9 はコマンド 7 の完了後に並列で実行されます。  
  
## <a name="using-the-batch-command-to-process-objects"></a>バッチ コマンドを使用したオブジェクトの処理  
 `Batch` コマンドには、複数の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトの処理をサポートするために特に用意された、以下の省略可能なプロパティおよび属性が含まれています。  
  
-   `ProcessAffectedObjects` コマンドの `Batch` 属性は、指定したオブジェクトを処理する `Process` コマンドに含まれる `Batch` コマンドの結果、再処理が必要になったオブジェクトがある場合に、インスタンスがそれらのオブジェクトも処理するかどうかを示します。  
  
-   [バインド](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/bindings-element-xmla)プロパティにはにより、すべての使用の不一致バインドのコレクションが含まれています、`Process`コマンド、`Batch`コマンド。  
  
-   [DataSource](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)プロパティには、すべてのによって使用されるデータ ソースのアウトオブ ライン バインドにはが含まれています、`Process`コマンド、`Batch`コマンド。  
  
-   [DataSourceView](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceview-element-xmla)プロパティにはすべてで使用されるデータ ソース ビューのアウトオブ ライン バインドが含まれています、`Process`コマンド、`Batch`コマンド。  
  
-   [ErrorConfiguration](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/errorconfiguration-element-xmla)プロパティでは、方法を指定する、`Batch`コマンドがすべてで発生したエラーを処理`Process`に含まれるコマンド、`Batch`コマンド。  
  
    > [!IMPORTANT]  
    >  `Process` コマンドが `Bindings` コマンドに含まれている場合、その `DataSource` コマンドには `DataSourceView`、`ErrorConfiguration`、`Process`、および `Batch` プロパティを含めることができません。 `Process` コマンドにこれらのプロパティを含める必要がある場合、その `Batch` コマンドを含む `Process` の対応するプロパティに、必要な情報を指定してください。  
  
## <a name="see-also"></a>参照  
 [要素をバッチ&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)   
 [要素を処理&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)   
 [多次元モデル オブジェクトの処理](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Analysis Services での XMLA による開発](developing-with-xmla-in-analysis-services.md)  
  
  
