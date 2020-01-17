---
title: 計算されるメンバーはサブセレクトとサブキューブで |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 6e35e8f7-ae1c-4549-8432-accf036d2373
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 57a7a9597be4b7a662fddd9550fdf341be44f922
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074793"
---
# <a name="calculated-members-in-subselects-and-subcubes"></a>サブセレクトとサブキューブで計算されるメンバー
  以前のリリースでは、計算されるメンバーは、サブセレクトまたはサブキューブで許可されませんでした。 しかし、SQL Server 2008 以降では、接続プロパティによって許可され有効になりました。 さらに、サブセレクトおよびサブキューブにおける計算されるメンバーの新しい動作が、SQL Server 2008 R2 で導入されました。  
  
## <a name="calculated-members-in-subselects-and-subcubes"></a>サブセレクトとサブキューブで計算されるメンバー  
 `SubQueries`で接続文字列プロパティ<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>または`DBPROPMSMDSUBQUERIES`プロパティ[サポートされる XMLA プロパティ&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)動作または許容値計算されるメンバーの定義または計算サブセレクトまたはサブキューブで設定します。 このドキュメントのコンテキストでは、特に明記しない限り、サブセレクトはサブセレクトとサブキューブを示します。  
  
 SubQueries プロパティでは次の値を指定できます。  
  
|||  
|-|-|  
|値|Description|  
|0|計算されるメンバーは、サブセレクトまたはサブキューブで許可されません。<br /><br /> 計算されるメンバーが参照されている場合にサブセレクトまたはサブキューブを評価すると、エラーが発生します。|  
|1|計算されるメンバーはサブセレクトまたはサブキューブで許可されますが、返されるサブ空間に先祖メンバーは含まれません。|  
|2|計算されるメンバーはサブセレクトまたはサブキューブで許可され、返されるサブ空間に先祖メンバーが含まれます。 また、混合粒度は、計算されるメンバーの選択で許可されます。|  
  
 SubQueries プロパティに値 1 または 2 を使用すると、計算されるメンバーをサブセレクトから返されるサブ空間のフィルター処理に使用できます。  
  
 この概念をわかりやすくするため、例を示します。まず、計算されるメンバーを作成し、次に上記の動作を示すためにサブセレクト クエリを発行します。  
  
 次の例では、[Seattle Metro] を都市として Washington 州の [Geography].[Geography] 階層に追加する、計算されるメンバーを作成します。  
  
 この例を実行するには、値 1 を持つ SubQueries プロパティが接続文字列に含まれており、すべての MDX ステートメントを同じセッションで実行する必要があります。  
  
 最初に、次の MDX 式を発行します。  
  
```  
//Remember to set Subqueries=1 in the connection string prior  
//to issue these commands  
//--> AS2008 behavior  
CREATE MEMBER [Adventure Works].[Geography].[Geography].[State-Province].&[WA]&[US].[Seattle Metro Agg]   
   AS  AGGREGATE(   
                 {   
                   [Geography].[Geography].[City].&[Bellevue]&[WA]  
                 , [Geography].[Geography].[City].&[Issaquah]&[WA]  
                 , [Geography].[Geography].[City].&[Redmond]&[WA]  
                 , [Geography].[Geography].[City].&[Seattle]&[WA]  
                 }  
                )    
```  
  
 次の MDX クエリを発行し、サブセレクトで許可された計算されるメンバーを表示します。  
  
```  
Select [Date].[Calendar Year].members on 0,  
       [Geography].[Geography].allmembers on 1  
from (Select {[Geography].[Geography].[State-Province].&[WA]&[US].[Seattle Metro Agg]} on 0 from [Adventure Works])  
Where [Measures].[Reseller Sales Amount]  
```  
  
 次の結果が得られます。  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2001|CY 2002|CY 2003|CY 2004|  
|Seattle Metro Agg|$2,383,545.69|$291,248.93|$763,557.02|$915,832.36|$412,907.37|  
  
 前述のように、SubQueries=1 の場合は、返されるサブ空間に [Seattle Metro] の先祖が存在しないため、[Geography].[Geography].allmembers には計算されるメンバーのみが含まれます。  
  
 接続文字列で SubQueries=2 を使用して実行すると、次の結果が得られます。  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2001|CY 2002|CY 2003|CY 2004|  
|All Geographies|(null)|(null)|(null)|(null)|(null)|  
|米国|(null)|(null)|(null)|(null)|(null)|  
|Washington|(null)|(null)|(null)|(null)|(null)|  
|Seattle Metro Agg|$2,383,545.69|$291,248.93|$763,557.02|$915,832.36|$412,907.37|  
  
 前述のように、SubQueries=2 の場合は、返されるサブ空間に [Seattle Metro] の先祖が存在しますが、集計に使用する標準メンバーが存在しないため、これらのメンバーに対する値はありません。 したがって、この例では、計算されるメンバーのすべての先祖メンバーに対して NULL 値が返されます。  
  
 上記の動作を理解するには、計算されるメンバーは標準メンバーのように親の集計に影響を与えないということを知っておくと役に立ちます。前者は、計算されるメンバーのみでフィルター処理を行うと、作成されたサブ空間の集計値に影響を与える標準メンバーが存在しないため、先祖が空になることを意味します。 標準メンバーをフィルター式に追加すると、これらの標準メンバーから集計値が得られます。 上記の例を引き続き使用すると、Oregon の都市 Portland と Washington の都市 Spokane は、次の MDX 式に示すように、計算されるメンバーが表示される同じ軸に追加されます。  
  
```  
Select [Date].[Calendar Year].members on 0,  
       [Geography].[Geography].allmembers on 1  
from (Select {  
               [Seattle Metro Agg]  
             , [Geography].[Geography].[City].&[Portland]&[OR]  
             , [Geography].[Geography].[City].&[Spokane]&[WA]  
             } on 0 from [Adventure Works]  
     )  
Where [Measures].[Reseller Sales Amount]  
```  
  
 結果は、次のようになります。  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2001|CY 2002|CY 2003|CY 2004|  
|All Geographies|$235,171.62|$419.46|$4,996.25|$131,788.82|$97,967.09|  
|米国|$235,171.62|$419.46|$4,996.25|$131,788.82|$97,967.09|  
|Oregon|$30,968.25|$419.46|$4,996.25|$17,442.97|$8,109.56|  
|Portland|$30,968.25|$419.46|$4,996.25|$17,442.97|$8,109.56|  
|97205|$30,968.25|$419.46|$4,996.25|$17,442.97|$8,109.56|  
|Washington|$204,203.37|(null)|(null)|$114,345.85|$89,857.52|  
|Spokane|$204,203.37|(null)|(null)|$114,345.85|$89,857.52|  
|99202|$204,203.37|(null)|(null)|$114,345.85|$89,857.52|  
|Seattle Metro Agg|$2,383,545.69|$291,248.93|$763,557.02|$915,832.36|$412,907.37|  
  
 上記の結果では、[All Geographies]、[United States]、[Oregon]、および [Washington] の集計値は、&[Portland]&[OR] および &[Spokane]&[WA] の子孫の集計から取得されます。 計算されるメンバーから取得されるものはありません。  
  
### <a name="remarks"></a>コメント  
 サブセレクトまたはサブキューブ式で許可されるのは、グローバルまたはセッションで計算されるメンバーのみです。 MDX 式にクエリで計算されるメンバーが含まれている場合に、サブセレクトまたはサブキューブ式を評価すると、エラーが発生します。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>   
 [クエリのサブセレクト](subselects-in-queries.md)   
 [サポートされる XMLA プロパティ (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)  
  
  
