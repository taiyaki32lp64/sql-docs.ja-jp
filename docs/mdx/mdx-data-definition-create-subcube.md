---
title: CREATE サブキューブステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f137e8c377c94a60fdcfd8f1534069cef4b28f66
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887438"
---
# <a name="mdx-data-definition---create-subcube"></a>MDX データ操作 - CREATE SUBCUBE


  指定したキューブまたはサブキューブのキューブ空間を、指定したサブキューブに再定義します。 このステートメントは、後続の操作のために、見かけ上のキューブ空間を変更します。  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE SUBCUBE Cube_Name AS Select_Statement  
                                                  | NON VISUAL ( Select_Statement )  
```  
  
## <a name="arguments"></a>引数  
 *Cube_Name*  
 制限されているキューブまたはパースペクティブの名前を指定する有効な文字列式です。これは、サブキューブの名前になります。  
  
 *Select_Statement*  
 WITH 句、NON EMPTY 句、または HAVING 句が含まれておらず、ディメンションまたはセルのプロパティを要求しない有効な多次元式 (MDX) の SELECT 式です。  
  
 Select ステートメントと**NON VISUAL**句の構文の詳細については、「 [select ステートメント&#40;&#41; MDX](../mdx/mdx-data-manipulation-select.md) 」を参照してください。  
  
## <a name="remarks"></a>コメント  
 既定のメンバーがサブキューブの定義で除外されると、それに応じて座標が変わります。 集計できる属性の場合、既定のメンバーは [All] メンバーに移動されます。 集計が不可能な属性の場合、既定のメンバーはサブキューブ内に存在するメンバーに移動します。 次の表には、サブキューブと既定のメンバーの組み合わせの例が含まれています。  
  
|元の既定のメンバー|集計可能/不可能|サブセレクト|変更後の既定のメンバー|  
|-----------------------------|-----------------------|---------------|----------------------------|  
|時間. すべて|はい|{Time. Year. 2003}|変更なし|  
|Time. Year.[1997]|はい|{Time. Year. 2003}|時間. すべて|  
|Time. Year.[1997]|いいえ|{Time. Year. 2003}|Time. Year.[2003]|  
|Time. Year.[1997]|はい|{Time. Year. 2003, Time. 2004}|時間. すべて|  
|Time. Year.[1997]|いいえ|{Time. Year. 2003, Time. 2004}|Time. Year.[2003] または<br /><br /> Time.Year.[2004]|  
  
 [All] のメンバーは、常にサブキューブ内に存在します。  
  
 サブキューブのコンテキストで作成されたセッションオブジェクトは、サブキューブが削除されると削除されます。  
  
 サブキューブの詳細については、「 [mdx &#40;mdx&#41;でのサブキューブの作成](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/building-subcubes-in-mdx-mdx)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、サブキューブを作成し、そのサブキューブ空間をカナダの国に存在するメンバーに制限します。 次に、 **MEMBERS**関数を使用して、Geography ユーザー定義階層の国レベルのすべてのメンバーを返します。カナダの国のみが返されます。  
  
```  
CREATE SUBCUBE [Adventure Works] AS  
   SELECT [Geography].[Country].&[Canada] ON 0  
   FROM [Adventure Works]  
  
SELECT [Geography].[Country].[Country].MEMBERS ON 0  
   FROM [Adventure Works]  
  
```  
  
 次の例では、サブキューブを作成します。これは、販売店のカテゴリと {[付加価値再販業者]、[Warehouse]} の {アクセサリー, 衣料} メンバーに対して、見かけ上のキューブ空間を制限します。[ビジネスタイプ]。  
  
 `CREATE SUBCUBE [Adventure Works] AS`  
  
 `Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works]`  
  
 次の MDX を使用して、Products.Category および Resellers.[Business Type] 内のすべてのメンバーのサブキューブを照会します。  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 では、次の結果が生成されます。  
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$2031079.39|$506,172.45|$1,524,906.93|  
|Value Added Reseller|$767388.52|$175,002.81|$592,385.71|  
|Warehouse|$1263690.86|$331,169.64|$932,521.23|  
  
 NON VISUAL 句を使用してサブキューブを削除し、再作成すると、製品のすべてのメンバーに対して真の合計を保持するサブキューブが作成されます。カテゴリおよび再販業者。[Business Type] は、サブキューブに表示されるかどうかにかかわらず、表示されます。  
  
 `CREATE SUBCUBE [Adventure Works] AS`  
  
 `NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works])`  
  
 上記と同じ MDX クエリを発行する:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 では、次のような結果が生成されます。  
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$80,450,596.98|$571,297.93|$1,777,840.84|  
|Value Added Reseller|$34,967,517.33|$175,002.81|$592,385.71|  
|Warehouse|$38,726,913.48|$331,169.64|$932,521.23|  
  
 [All Products] および [All Resellers] の列と行それぞれに、表示されているメンバーだけでなく、すべてのメンバーの合計が含まれます。  
  
## <a name="see-also"></a>関連項目  
 [MDX の主な概念 (Analysis Services)](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)   
 [Mdx スクリプトステートメント&#40;mdx&#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [DROP サブキューブ&#40;ステートメント MDX&#41;](../mdx/mdx-data-definition-drop-subcube.md)   
 [SELECT ステートメント (MDX)](../mdx/mdx-data-manipulation-select.md)  
  
  
