---
title: マイニング構造 (Analysis Services - データ マイニング) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [data mining]
- mining structures [Analysis Services], about mining structures
- mining structures [Analysis Services]
- data mining [Analysis Services], structure
- Analysis Services objects, data mining objects
- data mining [Analysis Services], models
- algorithms [data mining]
- data mining [Analysis Services], objects
- mining models [Analysis Services]
- mining models [Analysis Services], about data mining models
ms.assetid: 39748290-c32a-48e6-92a6-0c3a9223773a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1cfc630ffc943a989348e350c3668452a2777298
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083376"
---
# <a name="mining-structures-analysis-services---data-mining"></a>マイニング構造 (Analysis Services - データ マイニング)
  マイニング構造には、マイニング モデルの作成元となる、データ ソース ビュー、列の数と型、トレーニング セットとテスト セットに分ける省略可能なパーティションなどのデータを定義します。 1 つのマイニング構造は、同じドメインを共有する複数のマイニング モデルをサポートできます。 次の図は、データ マイニング構造とデータ ソースの関係、およびデータ マイニング構造とそれを構成するデータ マイニング モデルの関係を示しています。  
  
 ![データの処理: ソース、構造モデル、](../media/dmcon-modelarch.gif "データの処理: ソース、モデルの構造")  
  
 図内のマイニング構造は、CustomerID フィールドで結合された複数のテーブルまたはビューを含むデータ ソースを基にしています。 1 つのテーブルには顧客に関する情報 (地理的な領域、年齢、収入、性別など) が格納され、入れ子になった関連テーブルには各顧客の追加情報 (顧客が購入した製品など) を含む複数の行が格納されます。 この図は、同じマイニング構造から複数のモデルを作成し、それぞれのモデルに構造からさまざまな列を採用できることを示しています。  
  
 **モデル 1** CustomerID、Income、Age、Region を使用し、Region でデータをフィルタリングします。  
  
 **モデル 2** CustomerID、Income、Age、Region を使用し、Age でデータをフィルタリングします。  
  
 **モデル 3** CustomerID、Age、Gender と入れ子になったテーブルを使用し、フィルターは適用しません。  
  
 それぞれのモデルは入力に異なる列を使用しており、うち 2 つのモデルはフィルター適用によってモデル内で使用するデータをさらに絞り込んでいるため、同じデータに基づいていても結果は著しく異なる場合があります。 CustomerID 列は、ケース キーとして使用できる唯一の有効な列であるため、すべてのモデルに必要となります。  
  
 このセクションでは、データ マイニング構造の基本的なアーキテクチャについて説明します。マイニング構造の定義方法、その構造にデータを設定する方法、モデル作成のためにそれを使用する方法などが含まれます。 既存のデータ マイニング構造の管理方法またはエクスポート方法の詳細については、「 [データ マイニング ソリューションおよびオブジェクトの管理](management-of-data-mining-solutions-and-objects.md)」を参照してください。  
  
## <a name="defining-a-mining-structure"></a>マイニング構造の定義  
 データ マイニング構造の設定は、次の手順で行います。  
  
-   データ ソースを定義します。  
  
-   構造に含めるデータの列を選択し (モデルにはすべての列を含める必要はありません)、キーを定義します。  
  
-   必要に応じて入れ子になったテーブルのキーも含めて、構造のキーを定義します。  
  
-   ソース データをトレーニング セットとテスト セットに分割する必要があるかどうかを指定します。 このステップは省略可能です。  
  
-   構造を処理します。  
  
 これらの手順は、以下のセクションで詳しく説明します。  
  
### <a name="data-sources-for-mining-structures"></a>マイニング構造のデータ ソース  
 マイニング構造を定義する際には、既存のデータ ソース ビューで使用できる列を指定します。 データ ソース ビューは、複数のデータ ソースをまとめて 1 つのデータ ソースとして使用することができる共有オブジェクトです。 元のデータ ソースはクライアント アプリケーションでは表示されません。データ型の変更や、集計列またはエイリアス列の作成には、データ ソース ビューのプロパティを使用できます。  
  
 同じマイニング構造から複数のマイニング モデルを作成する場合、それぞれのモデルに構造からさまざまな列を採用することができます。 たとえば、1 つの構造を作成してデシジョン ツリー モデルとクラスター モデルを別々に作成し、各モデルが別々の列を使用したり、異なる属性を予測したりできます。  
  
 また、各モデルでは、構造からさまざまな方法で列を使用できます。 たとえば、データ ソース ビューに Income 列が含まれるとすると、それを異なるモデルに対して異なる方法でバインドすることができます。  
  
 データ マイニング構造には、データ ソースおよびそれに含まれる列の定義がソース データへの*バインド*という形で保存されます。 データ ソースのバインドの詳細については、「[データ ソースとバインド (SSAS 多次元)](../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)」を参照してください。 ただし、DMX の [CREATE MINING STRUCTURE (DMX)](/sql/dmx/create-mining-structure-dmx) ステートメントを使用して、特定のデータ ソースにバインドせずにデータ マイニング構造を作成することもできることに留意してください。  
  
### <a name="mining-structure-columns"></a>マイニング構造列  
 マイニング構造の構成要素は、データ ソースに格納されているデータについて記述したマイニング構造列です。 マイニング構造列には、データ型、コンテンツの種類、データの配布方法などの情報が格納されます。 マイニング構造には、特定のマイニング モデルに対する列の使用方法や、モデルを構築するために使用されるアルゴリズムの種類などの情報は含まれていません。これらの情報は、マイニング モデルの内部で定義されます。  
  
 マイニング構造には、入れ子になったテーブルを含めることもできます。 入れ子になったテーブルは、ケースのエンティティとその関連属性との間の一対多の関係を表します。 たとえば、顧客に関する情報と顧客の購入記録が別々のテーブルに格納されている場合は、入れ子になったテーブルを使用すると、これらの情報を単一のケースにまとめることができます。 この場合、顧客の識別子はエンティティで、購入記録は関連する属性となります。 入れ子になったテーブルを使用する場合詳細については、「[入れ子になったテーブル (Analysis Services - データ マイニング)](nested-tables-analysis-services-data-mining.md)」を参照してください。  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] でデータ マイニング モデルを作成するには、まずデータ マイニング構造を作成する必要があります。 データ マイニング ウィザードを使用すると、マイニング構造の作成、データの選択、およびマイニング モデルの追加の手順を段階的に実行できます。  
  
 データ マイニング拡張機能 (DMX) を使用してマイニング モデルを作成する場合は、モデルとモデル内の列を指定すると、必要なマイニング構造が DMX によって自動的に作成されます。 詳細については、「[CREATE MINING MODEL (DMX)](/sql/dmx/create-mining-model-dmx)」を参照してください。  
  
 詳細については、「[マイニング構造列](mining-structure-columns.md)」をご覧ください。  
  
### <a name="dividing-the-data-into-training-and-testing-sets"></a>トレーニング セットとテスト セットへのデータの分割  
 マイニング構造のデータを定義する際に、データの一部をトレーニング用に、一部をテスト用に指定することもできます。 そのため、データ マイニング構造を作成する前にデータを分割する必要はなくなりました。 代わりに、モデルを作成する際にデータの一定の割合をテスト用、残りをトレーニング用として指定できます。また、テスト データセットとして使用するケースの数を指定することもできます。 トレーニング データ セットとテスト データセットに関する情報は、マイニング構造と共にキャッシュも保存され、その結果、その構造に基づくすべてのモデルで同じテスト セットを使用できます。  
  
 詳しくは、「 [Training and Testing Data Sets](training-and-testing-data-sets.md)」をご覧ください。  
  
### <a name="enabling-drillthrough"></a>ドリルスルーの有効化  
 特定のマイニング モデルで使用する予定がない列でも、マイニング構造に追加することができます。 これは、分析プロセスで電子メール アドレスを使用せずに、クラスター モデルで顧客の電子メール アドレスを検索する場合などに便利です。 分析および予測のフェーズで列を無視するには、それを構造に追加しますが、使用法フラグを Ignore に設定するか、その列の使用を指定しません。 マイニング モデルでドリルスルーが有効であり、ユーザーが適切な権限を持っている場合には、この方法でフラグを設定したデータをクエリで使用できます。 たとえば、モデルの作成にそれらの列のデータが使用されなかった場合でも、すべての顧客の分析結果のクラスターを確認してから、ドリルスルー クエリを使用して特定のクラスターの顧客の名前と電子メールを取得できます。  
  
 詳細については、「[ドリルスルー クエリ (データ マイニング)](drillthrough-queries-data-mining.md)」をご覧ください。  
  
### <a name="processing-mining-structures"></a>マイニング構造の処理  
 マイニング構造は、処理されるまでは単なるメタデータ コンテナーです。 マイニング構造を処理する際、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、データに関する統計値、連続属性を分離する方法に関する情報、および後でマイニング モデルが使用するその他の情報を格納するキャッシュを作成します。 マイニング モデル自体には、このサマリー情報は保存されませんが、代わりに、マイニング構造の処理時にキャッシュに保存された情報が参照されます。 したがって、既存の構造に新しいモデルを追加するたびに構造を再処理する必要はなく、モデルのみを処理できます。  
  
 キャッシュが非常に大きい場合や詳細データを削除したい場合は、処理後にこのキャッシュを破棄することもできます。 データをキャッシュしない場合は、マイニング構造の `CacheMode` プロパティを `ClearAfterProcessing` に変更できます。 これにより、モデルを処理した後にキャッシュが破棄されます。 `CacheMode` プロパティを `ClearAfterProcessing` に設定すると、マイニング モデルからのドリルスルーが無効になります。  
  
 ただし、キャッシュを破棄した後は、マイニング構造に新しいモデルを追加することはできません。 新しいマイニング モデルを追加したり、既存のモデルのプロパティを変更した場合は、マイニング構造を最初に再処理する必要があります。 詳細については、「[処理の要件および注意事項 (データ マイニング)](processing-requirements-and-considerations-data-mining.md)」を参照してください。  
  
### <a name="viewing-mining-structures"></a>マイニング構造の表示  
 ビューアーを使用して、マイニング構造内のデータを参照することはできません。 しかし、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]では、データ マイニング デザイナーの **[マイニング構造]** タブを使用して構造列とその定義を表示できます。 詳細については、「 [データ マイニング デザイナー](data-mining-designer.md)」を参照してください。  
  
 マイニング構造のデータを確認する場合、データ マイニング拡張機能 (DMX) を使用してクエリを作成できます。 たとえば、 `SELECT * FROM <structure>.CASES` というステートメントでは、マイニング構造のすべてのデータが返されます。 この情報を取得するには、マイニング構造が既に処理されていて、処理結果がキャッシュされている必要があります。  
  
 `SELECT * FROM <model>.CASES` というステートメントでは同じ列が返されますが、特定のモデルのケースのみです。 詳細については、「[SELECT FROM &#60;structure&#62;.CASES](/sql/dmx/select-from-structure-cases)」および「[SELECT FROM &#60;model&#62;.CASES (DMX)](/sql/dmx/select-from-model-content-dmx)」を参照してください。  
  
## <a name="using-data-mining-models-with-mining-structures"></a>データ マイニング モデルとマイニング構造の使用  
 データ マイニング モデルは、マイニング構造によって表されるデータにマイニング モデル アルゴリズムを適用します。 マイニング モデルは特定のマイニング構造に属するオブジェクトで、マイニング構造によって定義されるプロパティのすべての値を継承します。 マイニング モデルは、マイニング構造に含まれているすべての列またはその一部を使用することができます。 構造列の複数のコピーを構造に追加できます。 構造列の複数のコピーをモデルに追加し、モデルの各構造列に異なる名前、つまり *別名*を割り当てることもできます。 構造列の別名定義の詳細については、「 [モデル列の別名の作成](create-an-alias-for-a-model-column.md) 」および「 [マイニング モデルのプロパティ](mining-model-properties.md)」を参照してください。  
  
 データ マイニング モデルのアーキテクチャの詳細については、「 [マイニング モデル (Analysis Services - データ マイニング)](mining-models-analysis-services-data-mining.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 マイニング構造の定義、管理、使用の詳細については、次のリンクを使用してください。  
  
|処理手順|リンク|  
|-----------|-----------|  
|リレーショナル マイニング構造の操作|[新しいリレーショナル マイニング構造の作成](create-a-new-relational-mining-structure.md)<br /><br /> [マイニング構造への入れ子になったテーブルの追加](add-a-nested-table-to-a-mining-structure.md)|  
|OLAP キューブに基づくマイニング構造の操作|[新規の OLAP マイニング構造の作成](create-a-new-olap-mining-structure.md)<br /><br /> [マイニング構造のソース キューブのフィルター選択](../filter-the-source-cube-for-a-mining-structure.md)|  
|マイニング構造内の列の操作|[マイニング構造への列の追加](add-columns-to-a-mining-structure.md)<br /><br /> [マイニング構造からの列の削除](remove-columns-from-a-mining-structure.md)|  
|マイニング構造のプロパティおよびデータの変更またはクエリ|[マイニング構造のプロパティの変更](change-the-properties-of-a-mining-structure.md)|  
|基になるデータ ソースの操作とソース データの更新|[マイニング構造に使用されるデータ ソース ビューの編集](edit-the-data-source-view-used-for-a-mining-structure.md)<br /><br /> [マイニング構造の処理](process-a-mining-structure.md)|  
  
## <a name="see-also"></a>参照  
 [データベース オブジェクト (Analysis Services - 多次元データ)](../multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [マイニング モデル (Analysis Services - データ マイニング)](mining-models-analysis-services-data-mining.md)  
  
  
