---
title: CREATE GLOBAL CUBE ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d678622c67a83c279cce094b849829e668af30cb
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892148"
---
# <a name="mdx-data-definition---create-global-cube"></a>MDX データ操作 - CREATE GLOBAL CUBE


  サーバー上のキューブのサブキューブに基づいて、ローカルに保存されたキューブを作成して設定します。 ローカルに保存されたキューブに接続するために、サーバーへの接続は必要ありません。 ローカルキューブの詳細については、「[ローカルキューブ&#40;Analysis Services-&#41;多次元データ](https://docs.microsoft.com/analysis-services/multidimensional-models/olap-physical/local-cubes-analysis-services-multidimensional-data)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE GLOBAL CUBE local_cube_name STORAGE 'Cube_Location'   
FROM source_cube_name (<param list>)  
  
<param list>::= <param> ,<param list> | <param>  
  
<param>::= <dims list> | <measures list>  
  
<measures list>::= <measure>[, <measures list>]   
  
<dims list>::= <dim def> [, <dims list>]  
  
<measure>::= MEASURE source_cube_name.measure_name [<visibility qualifier>] [AS measure_name]   
  
<dim def>::= <source dim def> | <derived dim def>  
  
<source dim def>::= DIMENSION source_cube_name.dimension_name [<dim flags>] [<visibility qualifier>] [AS dimension_name>] [FROM <dim from clause> ] [<dim content def>]  
  
<dim flags>::= NOT_RELATED_TO_FACTS   
  
<dim from clause>::= < dim DM from clause> | <reg dim from clause>   
  
<dim DM from clause>::= dm_model_name> COLUMN column_name   
  
<dim reg from clause>::= dimension_name  
  
<dim content def>::= ( <level list> [,<grouping list>] [,<member slice list>] [,<default member>] )  
  
<level list>::= <level def> [, <level list>]  
  
<level def>::= LEVEL level_name [<level type> ] [AS level_name] [<level content def>]  
  
<level content def>::= ( <property list> ) | NO_PROPERTIES  
  
<level type>::= GROUPING  
  
<property list>::= <property def> [, <property list>]  
  
<property def>::= PROPERTY property_name   
  
<grouping list>::= <grouping entity> [,<grouping list>]  
  
<grouping entity>::= GROUP group_level_name.group_name (<mixed list>)  
  
<grp mixed list>::= <grp mixed element> [,<grp mixed list>]  
  
<grp mixed element>::= <grouping entity> | <member def>  
  
<member slice list>::= <member list>  
  
<member list>::= <member def> [, <member list>]  
  
<member def>::= MEMBER member_name  
  
<default member>::= DEFAULT_MEMBER AS MDX_expression  
  
<visibility qualifier>::= HIDDEN   
```  
  
## <a name="syntax-elements"></a>構文要素  
 local_cube_name  
 ローカル キューブの名前です。  
  
 'Cube_Location'  
 ローカルに保持されるキューブの名前とパスです。  
  
 source_cube_name  
 ローカルキューブの基になるキューブの名前です。  
  
 source_cube_name.measure_name  
 ローカルキューブに含まれる、基になるメジャーの完全修飾名です。 メジャーディメンションの計算されるメンバーは使用できません。  
  
 measure_name  
 ローカルキューブ内のメジャーの名前。  
  
 source_cube_name.dimension_name  
 ローカルキューブに含まれる、基になるディメンションの完全修飾名です。  
  
 dimension_name  
 ローカル キューブのディメンションの名前です。  
  
 From \<dim from 句 >  
 派生ディメンションの定義のみの有効な仕様です。  
  
 NOT_RELATED_TO_FACTS  
 派生ディメンションの定義のみの有効な仕様です。  
  
 \<レベルの種類 >  
 派生ディメンションの定義のみの有効な仕様です。  
  
## <a name="remarks"></a>コメント  
 ローカルキューブは、メジャーとそれを定義する定義の definedin 用語です。 ディメンションには、次の2種類があります。  
  
-   ソースディメンション-これは、ソースキューブの1つに含まれていたディメンションです。  
  
-   派生ディメンション-新しい分析機能を提供するディメンションです。 派生ディメンションは、垂直方向または水平方向にスライスされるか、ディメンションメンバーのカスタムグループが含まれている、ソースディメンションに基づいて定義された標準のディメンションにすることができます。 また、派生ディメンションは、データ マイニング モデルに基づくデータ マイニング ディメンションである場合もあります。  
  
> [!NOTE]  
>  Dimension キーワードは、ディメンションまたは階層を参照できます。  
  
 ローカル キューブでは次のタスクを実行できます。  
  
-   ソースキューブに存在するディメンションを削除する  
  
-   ディメンションに階層を追加する、ディメンションから階層を削除する  
  
-   メジャーグループまたは特定のメジャーを削除する  
  
 CREATE GLOBAL CUBE ステートメントは、以下の規則に従います。  
  
-   CREATE GLOBAL CUBE ステートメントは、計算されるメジャーやアクションなどのすべてのコマンドを自動的にローカル キューブにコピーします。 親キューブを明示的に参照する多次元式 (MDX) 式がコマンドに含まれている場合、ローカルキューブでそのコマンドを実行することはできません。 この問題を回避するには、コマンドの MDX 式を定義するときに、 **Currentcube**キーワードを使用します。 **Currentcube**キーワードは、MDX 式内のキューブを参照するときに現在のキューブコンテキストを使用します。  
  
-   ローカルキューブファイル内の既存のグローバルキューブから作成されたグローバルキューブを同じローカルキューブファイルに保存することはできません。 たとえば、SalesLocal1 という名前のグローバルキューブを作成し、このキューブを C:\ ファイルに保存します。 次に、SalesLocal2 という名前の2つ目のグローバルキューブを作成します。 これで、SalesLocal2 グローバルキューブを C:\ ファイルに保存しようとすると、エラーが発生します。 ただし、SalesLocal2 グローバルキューブを別のローカルキューブファイルに保存することはできます。  
  
-   グローバル キューブでは、個別のカウント メジャーがサポートされません。 個別のカウント メジャーを含むキューブは非加法であるため、CREATE GLOBAL CUBE ステートメントでは、個別のカウント メジャーの作成や使用はできません。  
  
-   ローカル キューブにメジャーを追加する場合は、追加するメジャーに関連するディメンションも最低 1 つ追加する必要があります。  
  
-   親子階層をローカルキューブに追加すると、親子階層のレベルとフィルターは無視され、親子階層全体が含まれます。  
  
-   ローカル キューブではメンバー プロパティはサポートされません。  
  
-   ローカル キューブは、パースペクティブからは作成できません。  
  
-   ローカルキューブに準加法メジャーを含めると、次のルールが適用されます。  
  
    -   追加するメジャーの AggregateFunction プロパティが ByAccount の場合、Account ディメンションを含める必要があります。  
  
    -   追加するメジャーの AggregateFunction プロパティが FirstChild、LastChild、FirstNonEmpty、LastNonEmpty、または AverageOfChildren の場合、Time ディメンション全体を含める必要があります。  
  
-   データマイニングディメンションをローカルキューブに追加することはできません。  
  
-   参照ディメンションが具体化され、標準のディメンションとして追加されます。  
  
-   多対多ディメンションを含める場合は、次の規則が適用されます。  
  
    -   多対多ディメンション全体を追加する必要があります。  
  
    -   中間メジャー グループを追加する必要があります。  
  
    -   多対多リレーションシップに含まれる2つのメジャーグループに共通するすべてのディメンションの全体を追加する必要があります。  
  
 次の例では、再販業者の Sales Amount メジャー、リセラーディメンション、および Date ディメンションのみを含む、ローカルの永続化されたバージョンの Adventure Works キューブを作成する方法を示します。  
  
```  
CREATE GLOBAL CUBE [LocalReseller]  
   Storage 'C:\LocalAWReseller1.cub'  
   FROM [Adventure Works]  
   (  
      MEASURE  [Adventure Works].[Reseller Sales Amount],  
      DIMENSION [Adventure Works].[Reseller],  
      DIMENSION [Adventure Works].[Date]  
   )  
```  
  
 次の例は、ローカルキューブを作成するときのスライスを示しています。 作成されるグローバルキューブは、Adventure Works キューブに基づいています。このキューブは、会計年度レベルの2005メンバーによって垂直方向にスライスされ、会計年度および月レベルで水平に行われます。  
  
```  
CREATE GLOBAL CUBE [LocalReseller]  
   Storage 'C:\LocalAWReseller2.cub'  
   FROM [Adventure Works]  
   (  
      MEASURE  [Adventure Works].[Reseller Sales Amount],  
      DIMENSION [Adventure Works].[Reseller],  
      DIMENSION [Adventure Works].[Date]  
      (  
LEVEL [Fiscal Year],  
LEVEL [Month],  
MEMBER [Date].[Fiscal].[Fiscal Year].&[2005]  
      )  
   )  
```  
  
## <a name="see-also"></a>関連項目  
 [Mdx データ定義ステートメント&#40;mdx&#41;](../mdx/mdx-data-definition-statements-mdx.md)   
 [CREATE SESSION CUBE ステートメント&#40;MDX&#41;](../mdx/mdx-data-definition-create-session-cube.md)  
  
  
