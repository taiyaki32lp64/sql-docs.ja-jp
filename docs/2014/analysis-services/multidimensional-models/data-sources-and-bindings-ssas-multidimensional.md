---
title: データ ソースとバインド (SSAS 多次元) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data source views [Analysis Services], bindings
- DSO, bindings
- Analysis Services Scripting Language, data sources
- cubes [Analysis Services], bindings
- OLAP mining models [Analysis Services Scripting Language]
- bindings [Analysis Services Scripting Language]
- rebindings [Analysis Services Scripting Language]
- ASSL, bindings
- relational mining models [ASSL]
- data sources [Analysis Services Scripting Language]
- ASSL, data sources
- dimensions [Analysis Services], bindings
- measures [Analysis Services], bindings
- relational data sources [Analysis Services Scripting Language]
- Analysis Services Scripting Language, bindings
- chaptered rowsets
- granularity
- mining models [Analysis Services], data sources
- inline bindings [ASSL]
- out-of-line bindings
- measure groups [Analysis Services], bindings
- partitions [Analysis Services], bindings
ms.assetid: bc028030-dda2-4660-b818-c3160d79fd6d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b909423c431507d7709d814bfa4061eaf0a0e342
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076078"
---
# <a name="data-sources-and-bindings-ssas-multidimensional"></a>データ ソースとバインド (SSAS 多次元)
  キューブ、ディメンション、その他の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトはデータ ソースにバインドできます。 データ ソースとは次のいずれかのオブジェクトです。  
  
-   リレーショナル データ ソース  
  
-   行セット (またはチャプター行セット) を出力する [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] パイプライン  
  
 データ ソースを表す方法は、データ ソースの種類によって異なります。 たとえば、リレーショナル データ ソースは接続文字列によって区別されます。 使用できるデータ ソースの詳細については、「 [多次元モデルのデータ ソース](data-sources-in-multidimensional-models.md)」を参照してください。  
  
 使用しているデータ ソースにかかわらず、データ ソース ビュー (DSV) にはデータ ソースのメタデータが含まれています。 したがって、キューブまたは他の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトのバインドは DSV へのバインドとして表されます。 これらのバインドは、ビュー、計算列、およびデータ ソースに物理的に存在しないリレーションシップなどの論理オブジェクトのオブジェクトへのバインドを含めることができます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、式をカプセル化する計算列を DSV に追加し、対応する OLAP メジャーを DSV のその列にバインドします。 DSV の詳細については、「 [多次元モデルのデータ ソース ビュー](data-source-views-in-multidimensional-models.md)」を参照してください。  
  
 データ ソースへのバインド方法は各 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトによって異なります。 また、これらのオブジェクトのデータ バインドとデータ ソースの定義は、データバインド オブジェクト (ディメンションなど) の定義と共にインラインで提供することも、個別の定義セットとして不一致で提供することも可能です。  
  
## <a name="analysis-services-data-types"></a>Analysis Services のデータ型  
 バインドで使用されるデータ型は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]でサポートされているデータ型と一致する必要があります。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]では次のデータ型が定義されています。  
  
|Analysis Services のデータ型|説明|  
|---------------------------------|-----------------|  
|BigInt|64 ビットの符号付き整数です。 このデータ型は、Microsoft [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の Int64 データ型と、OLE DB の DBTYPE_I8 データ型にマップされます。|  
|Bool|ブール値です。 このデータ型は、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の Boolean データ型と、OLE DB の DBTYPE_BOOL データ型にマップされます。|  
|通貨|通貨単位の 1 万分の 1 までの精度を持つ -263 (-922,337,203,685,477.5808) ～ 263-1 (+922,337,203,685,477.5807) の通貨の値です。 このデータ型は、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の Decimal データ型と、OLE DB の DBTYPE_CY データ型にマップされます。|  
|date|倍精度浮動小数点数として保存される日付データです。 整数部分は 1899 年 12 月 30 日からの日数で、小数部分は日の端数です。 このデータ型は、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の DateTime データ型と、OLE DB の DBTYPE_DATE データ型にマップされます。|  
|Double|-1.79E +308 ～ 1.79E +308 の範囲の倍精度浮動小数点数です。 このデータ型は、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の Double データ型と、OLE DB の DBTYPE_R8 データ型にマップされます。|  
|Integer|32 ビットの符号付き整数です。 このデータ型は、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の Int32 データ型と、OLE DB の DBTYPE_I4 データ型にマップされます。|  
|単一|-3.40E +38 ～ 3.40E +38 の範囲の単精度浮動小数点数です。 このデータ型は、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の Single データ型と、OLE DB の DBTYPE_R4 データ型にマップされます。|  
|SmallInt|16 ビットの符号付き整数です。 このデータ型は、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の Int16 データ型と、OLE DB の DBTYPE_I2 データ型にマップされます。|  
|TinyInt|8 ビットの符号付き整数です。 このデータ型は、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の SByte データ型と、OLE DB の DBTYPE_I1 データ型にマップされます。<br /><br /> 注:データ ソースに tinyint データ型と、AutoIncrement プロパティのフィールドが含まれている場合は、データ ソース ビューで整数に変換されますし、True に設定されます。|  
|UnsignedBigInt|64 ビットの符号なし整数です。 このデータ型は、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の UInt64 データ型と、OLE DB の DBTYPE_UI8 データ型にマップされます。|  
|UnsignedInt|32 ビットの符号なし整数です。 このデータ型は、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の UInt32 データ型と、OLE DB の DBTYPE_UI4 データ型にマップされます。|  
|UnsignedSmallInt|16 ビットの符号なし整数です。 このデータ型は、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の UInt16 データ型と、OLE DB の DBTYPE_UI2 データ型にマップされます。|  
|WChar|Unicode 文字の NULL 終了ストリームです。 このデータ型は、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の String データ型と、OLE DB の DBTYPE_WSTR データ型にマップされます。|  
  
 データ ソースから受け取るデータはすべて、(通常は処理中に) バインドで指定された [!INCLUDE[ssAS](../../includes/ssas-md.md)] の型に変換されます。 変換を実行できない場合 (たとえば、String から Int への変換など) はエラーが発生します。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] では、バインドのデータ型は、通常、データ ソース内の変換元の型に最も適しているデータ型に設定されます。 たとえば、SQL 型の DateTime、SmallDateTime、DateTime2、DateTimeOffset は [!INCLUDE[ssAS](../../includes/ssas-md.md)] 型の Date にマップされ、SQL 型の Time は String にマップされます。  
  
## <a name="bindings-for-dimensions"></a>ディメンションのバインド  
 ディメンションの各属性は DSV の列にバインドされます。 ディメンションの属性はすべて 1 つのデータ ソースに基づいている必要がありますが、 バインドできるテーブルの列はさまざまです。 テーブル間のリレーションシップは DSV で定義されます。 リレーションシップの 1 つ以上のセットが同じテーブルに存在する場合は、'別名' テーブルとして機能する、DSV で名前付きクエリを紹介するために必要な場合があります。 式とフィルターは、DSV で名前付き計算と名前付きクエリを使用して定義されます。  
  
## <a name="bindings-for-measuregroups-measures-and-partitions"></a>メジャー グループ、メジャー、およびパーティションのバインド  
 各メジャー グループには次の既定のバインドがあります。  
  
-   メジャー グループは DSV のテーブルにバインドされます (たとえば `MeasureGroup.Source`)。  
  
-   各メジャーはそのテーブルの列にバインドされます (たとえば `Measure.ValueColumn.Source`)。  
  
-   各メジャー グループのディメンションには、メジャー グループの粒度を定義する *粒度属性* のセットがあります。 これらの各属性を、属性キーが含まれているファクト テーブルの列にバインドする必要があります (粒度属性の詳細については、このトピックの後半の「MeasureGroup 粒度属性」を参照してください)。  
  
 これら既定のバインドは、パーティションごとに選択的にオーバーライドできます。 各パーティションは異なるデータ ソース、テーブル名、クエリ名、またはフィルター式を指定できます。 最も一般的なパーティション分割方法では、同じデータ ソースを使用して、パーティションごとにテーブルをオーバーライドします。 その他、パーティションごとに異なるフィルターを適用する方法や、データ ソースを変更する方法もあります。  
  
 既定のデータ ソースを DSV で定義して、リレーションシップの詳細などのスキーマ情報を提供する必要があります。 パーティション レベルで指定するその他のテーブルやクエリは、DSV に一覧表示する必要はありませんが、メジャー グループに定義されている既定のテーブルと同じスキーマを含めるか、少なくともメジャーまたは粒度属性で使用される列をすべて含める必要があります。 メジャーと粒度属性ごとの詳細なバインドはパーティション レベルではオーバーライドできません。これらは、メジャー グループに定義されている列と同じ列であると想定されます。 したがって、実際にはパーティションでスキーマの異なるデータ ソースを使用している場合、そのパーティションに定義されている `TableDefinition` クエリが、メジャー グループで使用しているスキーマと同じスキーマになる必要があります。  
  
### <a name="measuregroup-granularity-attributes"></a>MeasureGroup 粒度属性  
 メジャー グループの粒度がデータベースの既知の粒度と一致し、ファクト テーブルからディメンション テーブルへの直接的なリレーションシップがある場合は、ファクト テーブルの適切な外部キー列に粒度属性をバインドするだけです。 たとえば、次のファクト テーブルとディメンション テーブルについて検討します。  
  
 `Sales(RequestedDate, OrderedProductID, ReplacementProductID, Qty)`  
  
 `Product(ProductID, ProductName,Category)`  
  
 ``  
  
 `Relation: Sales.OrderedProductID -> Product.ProductID`  
  
 `Relation: Sales.ReplacementProductID -> Product.ProductID`  
  
 ``  
  
 注文製品別に分析する場合、Sales ディメンション ロールの Ordered Product において、Product 粒度属性は Sales.OrderedProductID にバインドされます。  
  
 ただし、`GranularityAttributes` がファクト テーブルの列として存在しない場合もあります。 たとえば、次のような状況では `GranularityAttributes` が列として存在しない可能性があります。  
  
-   OLAP の粒度がソースの粒度よりも粗い。  
  
-   ファクト テーブルとディメンション テーブルの間に中間テーブルが介在する。  
  
-   ディメンション キーがディメンション テーブルの主キーと異なる。  
  
 このような場合には、ファクト テーブルに GranularityAttributes が存在するように、DSV を定義する必要があります。 たとえば、名前付きクエリや計算列を使用します。  
  
 上記と同じサンプル テーブルで、粒度がカテゴリ別であれば、Sales のビューを使用できます。  
  
 `SalesWithCategory(RequestedDate, OrderedProductID, ReplacementProductID, Qty, OrderedProductCategory)`  
  
 `SELECT Sales.*, Product.Category AS OrderedProductCategory`  
  
 `FROM Sales INNER JOIN Product`  
  
 `ON Sales.OrderedProductID = Product.ProductID`  
  
 ``  
  
 この場合は、GranularityAttribute カテゴリが SalesWithCategory.OrderedProductCategory にバインドされます。  
  
### <a name="migrating-from-decision-support-objects"></a>Decision Support オブジェクトからの移行  
 Decision Support オブジェクト (DSO) 8.0 では、`PartitionMeasures` を再バインドできます。 したがって、このような場合の移行方法として、適切なクエリを作成します。  
  
 同様に、パーティション内でディメンション属性を再バインドすることはできませんが、DSO 8.0 ではこの再バインドも可能です。 このような場合の移行方法として、ディメンションで使用されているテーブルや列と同じものがパーティションの DSV に存在するように、DSV で必要な名前付きクエリを定義します。 場合によっては、構造化された関連テーブル セットではなく、1 つの名前付きクエリに From/Join/Filter 句をマップするという単純な移行方法を採用する必要があります。 DSO 8.0 では、パーティションが同じデータ ソースを使用していても PartitionDimensions を再バインドできるので、移行には同じデータ ソースの複数の DSV が必要になる場合もあります。  
  
 DSO 8.0 では、対応するバインドを 2 とおりの方法で表すことができます。つまり、最適化されたスキーマを使用しているかどうかによって、ディメンション テーブルの主キーにバインドするか、ファクト テーブルの外部キーにバインドします。 ASSL では、これらの方法が区別されません。  
  
 ディメンション テーブルが含まれていないデータ ソースを使用しているパーティションでも、同じバインド方法が適用されます。これは、ディメンション テーブルの主キー列ではなく、ファクト テーブルの外部キー列にバインドされるためです。  
  
## <a name="bindings-for-mining-models"></a>マイニング モデルのバインド  
 マイニング モデルはリレーショナルまたは OLAP です。 リレーショナル マイニング モデルのデータ バインドは、OLAP マイニング モデルのバインドとは大きく異なります。  
  
### <a name="bindings-for-a-relational-mining-model"></a>リレーショナル マイニング モデルのバインド  
 リレーショナル マイニング モデルは、DSV で定義されているリレーションシップを利用して、どの列をどのデータ ソースにバインドするかに関するあいまいさを解決します。 リレーショナル マイニング モデルのデータ バインドは、次のルールに従います。  
  
-   入れ子になっていないテーブルの各列は、多対一または一対一のリレーションシップに従って、ケース テーブルまたはケース テーブルに関連するテーブルの列にバインドされます。 DSV はテーブル間のリレーションシップを定義します。  
  
-   入れ子になったテーブルの各列はソース テーブルにバインドされます。 入れ子になったテーブルの列が所有している列は、そのソース テーブルまたはソース テーブルに関連するテーブルの列にバインドされます (この場合もバインドは多対一または一対一のリレーションシップに従います)。マイニング モデルのバインドは、入れ子になったテーブルの結合パスを提供しません。 この情報は、DSV で定義されているリレーションシップによって提供されます。  
  
### <a name="bindings-for-an-olap-mining-model"></a>OLAP マイニング モデルのバインド  
 OLAP マイニング モデルには DSV に相当するものがありません。 したがって、データ バインドによって、列とデータ ソースの間のあいまいさを排除する必要があります。 たとえば、マイニング モデルが Sales キューブに基づき、列が Qty、Amount、および Product Name に基づくことが可能です。 または、マイニング モデルが Product に基づき、列が Product Name、Product Color、および Sales Qty の入れ子になったテーブルに基づくことも可能です。  
  
 OLAP マイニング モデルのデータ バインドは、次のルールに従います。  
  
-   入れ子になっていないテーブルの各列はキューブ上のメジャー、そのキューブのディメンション上の属性 (ディメンション ロールの場合は、あいまいさを排除するために `CubeDimension` を指定)、またはディメンション上の属性にバインドされます。  
  
-   入れ子になったテーブルの各列は `CubeDimension` にバインドされます。 つまり、ディメンションから関連キューブまで、またはキューブからそのディメンションの 1 つまで (入れ子になったテーブルでは一般的ではありません)、移動する方法を定義します。  
  
## <a name="out-of-line-bindings"></a>不一致バインド  
 不一致バインドを使用すると、コマンドが実行されている間、既存のデータ バインドを一時的に変更することができます。 不一致バインドとは、コマンドに含まれ、持続しないバインドのことです。 不一致バインドは、特定のコマンドの実行中にのみ適用されます。 一方、インライン バインドは ASSL のオブジェクト定義に含まれ、サーバー メタデータ内のオブジェクト定義を持続します。  
  
 ASSL では、不一致バインドを `Process` コマンド (バッチに含まれていない場合) または `Batch` コマンドで指定できます。 不一致バインドを `Batch` コマンドで指定すると、`Batch` コマンドで指定したすべてのバインドによって新しいバインド コンテキストが作成され、バッチのすべての `Process` コマンドがそのコンテキストで実行されます。 この新しいバインド コンテキストには、`Process` コマンドによって間接的に処理されるオブジェクトが含まれています。  
  
 不一致バインドをコマンドで指定すると、指定したオブジェクトの持続 DDL に含まれているインライン バインドがオーバーライドされます。 これらの処理されたオブジェクトには、`Process` コマンドで直接指定されたオブジェクトや、処理の一部として自動的に処理が開始される他のオブジェクトが含まれている場合があります。  
  
 不一致バインドは、処理コマンドと共にオプションの `Bindings` コレクション オブジェクトを含めることで指定します。 オプションの `Bindings` コレクションには次の要素が含まれています。  
  
|プロパティ|Cardinality|型|説明|  
|--------------|-----------------|----------|-----------------|  
|`Binding`|0-n|`Binding`|新しいバインドのコレクションを提供します。|  
|`DataSource`|0-1|`DataSource`|サーバーの使用された `DataSource` を置き換えます。|  
|`DataSourceView`|0-1|`DataSourceView`|サーバーの使用された `DataSourceView`<br /><br /> を置き換えます。|  
  
 不一致バインドに関連する要素はすべてオプションです。 指定されていない要素については、ASSL では持続オブジェクトの DDL に含まれている指定が使用されます。 `DataSource` コマンドの `DataSourceView` または `Process` の指定はオプションです。 `DataSource` または `DataSourceView` が指定されている場合は、インスタンス化されず、`Process` コマンドの完了後は持続しません。  
  
### <a name="definition-of-the-out-of-line-binding-type"></a>不一致バインド型の定義  
 ASSL では、不一致 `Bindings` コレクション内で、複数のオブジェクトのバインドのコレクションである、各 `Binding` を使用できます。 各 `Binding` には拡張オブジェクト参照があります。これはオブジェクト参照に似ていますが、マイナー オブジェクト (たとえばディメンション属性やメジャー グループ属性) の参照も可能です。 このオブジェクトは特有のフラット形式、`Object`要素`Process`いる点を除き、コマンド、 \<*オブジェクト*>\< */オブジェクト*>タグはありません。  
  
 バインドが指定されている各オブジェクトが、フォームの XML 要素によって識別される\<*オブジェクト*> ID (たとえば、 `DimensionID`)。 オブジェクトを識別したら、フォームで具体的にできるだけ\<*オブジェクト*> ID は、通常、バインドされているが指定されている、要素を識別する`Source`。 一般に、属性の列バインドの場合のように、`Source` は `DataItem` のプロパティです。 この場合は、`DataItem` タグを指定しないで、バインドする列に直接存在するかのように `Source` プロパティを指定するだけです。  
  
 `KeyColumns` は、`KeyColumns` コレクション内の順序によって識別されます。 たとえば、属性の最初と 3 番目のキー列のみを指定することはできません。2 番目のキー列がスキップされることを示す方法がないからです。 不一致バインドでは、ディメンション属性のキー列のすべてが存在する必要があります。  
  
 `Translations` には ID がありませんが、その言語によって意味が識別されます。 したがって、`Translations` 内の `Binding` にその言語識別子を含める必要があります。  
  
 DDL に直接存在しない `Binding` 内で許容されるもう 1 つの要素は、`ParentColumnID` です。これはデータ マイニングの入れ子になったテーブルに使用されます。 この場合は、バインドを提供する入れ子になったテーブルの親列を指定する必要があります。  
  
  
