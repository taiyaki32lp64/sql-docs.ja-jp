---
title: INSERT INTO (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 210ab8c5750fdcb38bcbca324d77eecd926042d1
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892720"
---
# <a name="insert-into-dmx"></a>INSERT INTO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指定されたデータ マイニング オブジェクトを処理します。 マイニングモデルとマイニング構造の処理の詳細については、「[処理&#40;の要件&#41;と考慮事項のデータマイニング](https://docs.microsoft.com/analysis-services/data-mining/processing-requirements-and-considerations-data-mining)」を参照してください。  
  
 マイニング構造が指定された場合、ステートメントはマイニング構造とすべての関連するマイニング モデルを処理します。 マイニング モデルが指定された場合、ステートメントはマイニング モデルだけを処理します。  
  
## <a name="syntax"></a>構文  
  
```  
  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure> (<mapped model columns>) <source data query>  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure>.COLUMN_VALUES (<mapped model columns>) <source data query>  
```  
  
## <a name="arguments"></a>引数  
 *model*  
 モデル識別子です。  
  
 *データ*  
 構造識別子です。  
  
 *マップされたモデル列*  
 列の識別子と入れ子になった識別子のコンマ区切りのリストです。  
  
 *ソースデータクエリ*  
 プロバイダー定義形式のソース クエリです。  
  
## <a name="remarks"></a>コメント  
 **マイニングモデル**または**マイニング構造**を指定しない場合[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 、は名前に基づいてオブジェクトの種類を検索し、正しいオブジェクトを処理します。 サーバーが同じ名前のマイニング構造とマイニング モデルを持つ場合、エラーが返されます。  
  
 2番目の構文形式を使用して、INSERT INTO *\<object >* します。COLUMN_VALUES を使用すると、モデルをトレーニングしなくても、モデル列にデータを直接挿入できます。 この方法によって、階層あるいは順序付けられた列を含むデータセットを使用する場合に便利な順序で、簡単に列データがモデルに提供されます。  
  
 マイニングモデルまたはマイニング構造と共に**INSERT INTO**を使用して、マップさ\<れたモデル列 > \<とソースデータクエリ > を省略した場合、ステートメントは**processdefault**のように動作し、バインドを使用します。は既に存在します。 バインドが存在しない場合、ステートメントはエラーを返します。 **Processdefault**の詳細については、「[処理オプション&#40;と&#41;設定 Analysis Services](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-options-and-settings-analysis-services)」を参照してください。 次の例に構文を示します。  
  
```  
INSERT INTO [MINING MODEL] <model>  
```  
  
 **マイニングモデル**を指定し、マップされた列とソースデータクエリを指定すると、モデルと関連する構造が処理されます。  
  
 次の表は、オブジェクトの状態に依存する、異なる形式のステートメントの結果について示しています。  
  
|ステートメントから削除してください。|オブジェクトの状態|結果|  
|---------------|----------------------|------------|  
|マイニングモデル *\<モデル > への挿入*|マイニング構造は処理されます。|マイニング モデルは処理されます。|  
||マイニング構造は処理されません。|マイニング モデルとマイニング構造は処理されます。|  
||マイニング構造に追加のマイニング モデルが含まれます。|処理は失敗します。 構造と関連するマイニング モデルを再処理する必要があります。|  
|マイニング構造 *\<構造 > への挿入*|マイニング構造は処理されるか処理に失敗します。|マイニング構造と関連するマイニング モデルは処理されます。|  
|ソースクエリを含む *\<> マイニングモデルモデルモデル*への挿入<br /><br /> または<br /><br /> ソースクエリを含む *\<>* マイニング構造構造を挿入する|構造またはモデルのどちらかが既に内容に含まれます。|処理は失敗します。 この操作を実行する前に、[ [DMX &#40;&#41;の削除](../dmx/delete-dmx.md)] を使用してオブジェクトをクリアする必要があります。|  
  
## <a name="mapped-model-columns"></a>モデル列のマップ  
 \<マップされたモデル列 > 要素を使用して、データソースの列をマイニングモデルの列にマップできます。 マップ\<されたモデル列 > 要素には、次の形式があります。  
  
```  
<column identifier> | SKIP | <table identifier> (<column identifier> | SKIP), ...  
```  
  
 **SKIP**を使用すると、ソースクエリに存在する必要があるが、マイニングモデルに存在しない特定の列を除外できます。 SKIP は、入力行セットに含まれる列を制御できない場合に役立ちます。 独自の OPENQUERY を記述する場合は、SKIP を使用するのではなく SELECT 列リストから列を除外することをお勧めします。  
  
 SKIP は、結合を実行するために入力行セットの列が必要だが、その列がマイニング構造では使用されない場合にも役立ちます。 この典型的な例が、入れ子になったテーブルを含むマイニング構造とマイニング モデルです。 この構造の入力行セットには、SHAPE 句を使用して階層的な行セットを作成するために使用される外部キー列が含まれますが、外部キー列がモデルで使用されることはほとんどありません。  
  
 SKIP の構文では、対応するマイニング構造列がない入力行セットの個々の列の位置に SKIP を挿入する必要があります。 たとえば、後述の入れ子になったテーブルの例では、APPEND 句で OrderNumber のクエリを実行して、結合を指定するために RELATE 句で使用できるようにする必要があります。ただし、マイニング構造では、入れ子になったテーブルに OrderNumber データを挿入しないようにする必要があります。 したがって、この例では、INSERT INTO 引数で OrderNumber ではなく SKIP キーワードを使用します。  
  
## <a name="source-data-query"></a>ソース データ クエリ  
 Source \<data query > 要素には、次のデータソースの種類を含めることができます。  
  
-   **OPENQUERY**  
  
-   **OPENROWSET**  
  
-   **オート**  
  
-   行セットを返すクエリ[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
 データソースの種類の詳細については、「 [ &#60;ソースデータのクエリ&#62;](../dmx/source-data-query.md)」を参照してください。  
  
## <a name="basic-example"></a>基本の例  
 次の例では、 **OPENQUERY**を使用して、 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]データベース内の対象メーリングデータに基づいて Naive Bayes モデルをトレーニングします。  
  
```  
INSERT INTO NBSample (CustomerKey, Gender, [Number Cars Owned],  
    [Bike Buyer])  
OPENQUERY([AdventureWorksDW2012],'Select CustomerKey, Gender, [NumberCarsOwned], [BikeBuyer]   
FROM [vTargetMail]')  
```  
  
## <a name="nested-table-example"></a>入れ子になったテーブルの例  
 次の例では、**図形**を使用して、入れ子になったテーブルを含むアソシエーションマイニングモデルをトレーニングします。 最初の行には、 **SHAPE_APPEND**ステートメントでは必須であり、マイニングモデルでは使用されない、 **SKIP**の代わりに ordernumber が含まれていることに注意してください。  
  
```  
INSERT INTO MyAssociationModel  
    ([OrderNumber],[Models] (SKIP, [Model])  
    )  
SHAPE {  
    OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
AS [Models]  
```  
  
## <a name="see-also"></a>参照  
 [データマイニング拡張&#40;機能&#41; DMX データ定義ステートメント](../dmx/dmx-statements-data-definition.md)   
 [データマイニング拡張&#40;機能&#41; DMX データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
