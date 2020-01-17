---
title: ドリルスルーステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ee90d2c367fa289e8255a84e4eb6da19b37933e0
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68891203"
---
# <a name="mdx-data-manipulation---drillthrough"></a>MDX データ操作 - DRILLTHROUGH


  キューブ内の指定されたセルの作成に使用されたテーブル行を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DRILLTHROUGH[MAXROWSUnsigned_Integer]   
      <MDX SELECT statement>   
      [RETURNSet_of_Attributes_and_Measures   
            [,Set_of_Attributes_and_Measures ...]  
      ]  
```  
  
## <a name="arguments"></a>引数  
 *Unsigned_Integer*  
 正の整数値です。  
  
 *MDX SELECT statement*  
 任意の有効な多次元式 (MDX) 式の SELECT ステートメントです。  
  
 *Set_of_Attributes_and_Measures*  
 ディメンションの属性とメジャーのコンマ区切りの一覧です。  
  
## <a name="remarks"></a>コメント  
 ドリルスルーとは、エンドユーザーがキューブから1つのセルを選択し、より詳細な情報を取得するためにそのセルのソースデータから結果セットを取得する操作です。 既定では、ドリルスルーの結果セットは、選択したキューブ セルの値を計算するために評価されたテーブル行から導き出されます。 エンドユーザーがドリルスルーを行うには、クライアントアプリケーションがこの機能をサポートしている必要があります。 で[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]は、ROLAP パーティションまたはディメンションに対してクエリを実行しない限り、結果は MOLAP ストレージから直接取得されます。  
  
> [!IMPORTANT]  
>  ドリルスルーのセキュリティは、キューブで定義された全般的なセキュリティ オプションに基づいています。 ユーザーが MDX を使用して一部のデータを取得できない場合、ドリルスルーでも同じ方法でユーザーが制限されます。  
  
 対象のセルは、MDX ステートメントによって指定します。 **MAXROWS**引数で指定された値は、結果の行セットによって返される行の最大数を示します。  
  
 既定では、返される行の最大数は1万行です。 つまり、 **MAXROWS**を指定しないままにした場合、1万行以下になります。 この値がシナリオに対して小さすぎる場合は、 **MAXROWS**をなどのより大きい数値`MAXROWS 20000`に設定できます。 全体が少なすぎる場合は、 **OLAP\Query\DefaultDrillthroughMaxRows**サーバーのプロパティを変更することで、既定値を増やすことができます。 このプロパティの変更の詳細については、「 [Analysis Services のサーバープロパティ](https://docs.microsoft.com/analysis-services/server-properties/server-properties-in-analysis-services)」を参照してください。  
  
 特に指定しない限り、返される列には、多対多ディメンション以外の、指定したメジャーのメジャーグループに関連付けられているすべてのディメンションのすべての粒度属性が含まれます。 ディメンションとメジャーグループを区別するために、キューブディメンションの前に $ が付きます。 **RETURN**句を使用して、ドリルスルー クエリで返される列を指定します。 次の関数が 1 つの属性に適用できるまたはによってメジャー、**RETURN**句。  
  
 Name(attribute_name)  
 指定された属性メンバーの名前を返します。  
  
 UniqueName (attribute_name)  
 指定された属性メンバーの一意の名前を返します。  
  
 キー (attribute_name [, N])  
 指定された属性メンバーのキーを返します。N は、複合キーの列 (存在する場合) を指定します。 N の既定値は1です。  
  
 Caption(attribute_name)  
 指定された属性メンバーのキャプションを返します。  
  
 MemberValue(attribute_name)  
 指定された属性メンバーのメンバー値を返します。  
  
 CustomRollup (attribute_name)  
 指定された属性メンバーのカスタム ロールアップ式を返します。  
  
 CustomRollupProperties (attribute_name)  
 指定された属性メンバーのカスタム ロールアップ プロパティを返します。  
  
 UnaryOperator(attribute_name)  
 指定された属性メンバーの単項演算子を返します。  
  
## <a name="example"></a>例  
 次の例では、オーストラリアの国の再販業者 sales amount メジャー (既定のメジャー) に2007年7月のセルを指定しています。 RETURN 句では、このセルの基になる各販売日、製品モデル名、従業員名、販売金額、税金額、および製品コストの値を指定します。  
  
```  
DRILLTHROUGH  
SELECT  
   ([Date].[Calendar].[Month].[July 2007])  
ON 0   
FROM [Adventure Works]  
WHERE [Geography].[Country].[Australia]  
RETURN   
  [$Date].[Date]  
  ,KEY([$Product].[Model Name])  
  ,NAME([$Employee].[Employee])  
  ,[Reseller Sales].[Reseller Sales Amount]  
  ,[Reseller Sales].[Reseller Tax Amount]  
  ,[Reseller Sales].[Reseller Standard Product Cost]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX データ操作ステートメント&#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
