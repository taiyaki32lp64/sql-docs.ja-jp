---
title: CREATE SESSION CUBE ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ac95afcebcf07a5d691db5f2599b3290b9587d44
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038362"
---
# <a name="mdx-data-definition---create-session-cube"></a>MDX データ操作 - CREATE SESSION CUBE


  既存のサーバー キューブから、セッション キューブを作成および設定します。 セッション キューブは現在のセッション内でのみ表示できます。他のセッションから参照したり、クエリを実行することはできません。 セッション キューブは、セッションが閉じられたときに暗黙的に削除されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE SESSION CUBE session_cube_name FROM <cube list> (<param list>)  
  
<cube list>::= source_cube_name [,<cube list>]  
  
<param list>::= <param> ,<param list> | <param>  
  
<param>::= <dims list> | <measures list>  
  
<measures list>::= <measure>[, <measures list>]   
  
<dims list>::= <dim def> [, <dims list>]  
  
<measure>::= MEASURE source_cube_name.measure_name [<visibility qualifier>] [AS measure_name]   
  
<dim def>::= <source dim def> | <derived dim def>  
  
<source dim def>::= DIMENSION source_cube_name.dimension_name [<dim flags>] [<visibility qualifier>] [AS dimension_name>] [FROM <dim from clause> ] [<dim content def>]  
  
<dim flags>::= NOT_RELATED_TO_FACTS   
  
<dim from clause>::= <reg dim from clause>   
  
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
 session_cube_name  
 セッション キューブの名前です。  
  
 source_cube_name  
 作成するセッション キューブの基になるキューブの名前です。  
  
 source_cube_name.measure_name  
 セッション キューブに含まれる、基になるメジャーの完全修飾名。 メジャー ディメンションの計算されるメンバーは許可されていません。  
  
 measure_name  
 セッション キューブのメジャーの名前です。  
  
 source_cube_name.dimension_name  
 セッション キューブに含まれるソース ディメンションの完全修飾名。  
  
 dimension_name  
 セッション キューブのディメンションの名前。  
  
 \<句から dim >  
 派生ディメンションの定義のみ有効な仕様。  
  
 NOT_RELATED_TO_FACTS  
 派生ディメンションの定義のみ有効な仕様。  
  
 \<レベルの種類 >  
 派生ディメンションの定義のみ有効な仕様。  
  
## <a name="remarks"></a>コメント  
 サーバー キューブやローカル キューブと異なり、セッション キューブは、それを作成したセッションの期間を超えて保持されません。 セッション キューブはメジャーとその定義の観点から定義されます。 ディメンションの 2 種類があります。  
  
-   ソース ディメンション - これらは、1 つ以上のソース キューブの一部であったディメンションです。  
  
-   派生ディメンション - これらは、新しい分析機能を提供するディメンションです。 派生ディメンションは、通常のディメンションが定義されている基になる、ソース ディメンションを垂直方向または水平方向にスライスか、またはディメンション メンバーのカスタム グループを格納します。 また、派生ディメンションは、データ マイニング モデルに基づくデータ マイニング ディメンションである場合もあります。  
  
> [!NOTE]  
>  Dimension キーワードは、ディメンションまたは階層を参照できます。  
  
 セッション キューブは、Microsoft Excel などのクライアント アプリケーションで主にカスタム メンバー グループに属性メンバーの動的なグループ化に使用されます。 セッション キューブでは、次のタスクを実行できます。  
  
-   ソース キューブに存在するディメンションを削除する。  
  
-   追加またはディメンションから階層を削除します。  
  
-   メジャー グループまたは特定のメジャーを削除します。  
  
-   既存の属性に対してグループを作成するための属性のバインドに基づく新しい属性を追加するには.  
  
> [!IMPORTANT]  
>  セッション キューブ オブジェクトのセキュリティは、基になるソース オブジェクトのセキュリティを継承します。 アクションや計算スクリプトなどの他のオブジェクトは、セッション キューブも継承されます。  
  
 CREATE SESSION CUBE ステートメントでは、これらの規則に従います。  
  
-   親子階層ではグループ化を実行できません。  
  
-   ROLAP ディメンションでグループ化を行うことはできません。  
  
-   リンク ディメンションでグループ化を行うことはできません。  
  
-   カスタム ロールアップを持つレベルでグループ化を行うことはできません。  
  
-   分離された属性階層ではグループ化を実行できません。  
  
-   (年齢、性別) などのレベル間の多対多のリレーションシップを持つ階層には、不自然階層では、グループ化を行うことはできません。  
  
-   MDX スクリプト内でキューブ名を明示的に参照しても、セッション キューブでは名前が異なるためグループ化によって参照が無効になります。 代わりに CURRENTCUBE キーワードを使用します。  
  
-   明示的な既定メンバーを持つディメンションではグループ化を実行できません。  
  
-   グループ化を実行するときに、元のサーバー キューブのセッション スコープの計算されるメンバーは削除されます。  
  
-   サーバー キューブのキューブ ディメンションでグループ化を実行する場合、同じディメンションに基づくすべてのキューブ ディメンションに影響します。  
  
## <a name="example"></a>例  
 Reseller Sales Amount メジャー、Reseller ディメンション、Product ディメンション、Geography ディメンション、および Date ディメンションを含んでいる Adventure Works キューブのセッション スコープのバージョンを作成する次の例に示します。 このセッション キューブ内では 2 つのグループが作成されます。1 つはヨーロッパ諸国を含み、もう 1 つは北米の国々を含みます。 このサンプルは、ユーザーがメンバーのカスタム グループを作成するときに、Microsoft Excel によって発行された CREATE SESSION CUBE ステートメントの簡略化されたバージョンです。  
  
```  
CREATE SESSION CUBE [Adventure Works_XL_GROUPING1]   
   FROM [Adventure Works]   
   ( MEASURE [Adventure Works].[Internet Sales Amount]  
   ,MEASURE [Adventure Works].[Reseller Sales Amount]  
   ,DIMENSION [Adventure Works].[Date].[Calendar]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Year]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Semester]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Quarter]  
   ,DIMENSION [Adventure Works].[Date].[Month Name]  
   ,DIMENSION [Adventure Works].[Date].[Date]  
   ,DIMENSION [Adventure Works].[Geography].[Country]   
      HIDDEN AS _XL_GROUPING81  
   ,DIMENSION [Adventure Works].[Geography].[State-Province]  
   ,DIMENSION [Adventure Works].[Geography].[City]  
   ,DIMENSION [Adventure Works].[Geography].[Postal Code]  
   ,DIMENSION [Adventure Works].[Geography].[Geography]  
   ,DIMENSION [Adventure Works].[Product].[Product Categories]  
   ,DIMENSION [Adventure Works].[Product].[Category]  
   ,DIMENSION [Adventure Works].[Product].[Subcategory]  
   ,DIMENSION [Adventure Works].[Product].[Product]  
   ,DIMENSION [Adventure Works].[Product].[Product Key]  
   ,DIMENSION [Adventure Works].[Reseller].[Reseller]  
   ,DIMENSION [Adventure Works].[Reseller].[Geography Key]  
   ,DIMENSION [Geography].[Country]   
      NOT_RELATED_TO_FACTS FROM _XL_GROUPING81   
          ( LEVEL [(All)]  
         ,LEVEL [Country1] GROUPING  
         ,LEVEL [Country]  
            ,GROUP [Country1].[CountryXl_Grp_1]   
                ( MEMBER [Geography].[Country].&[Canada]  
                  ,MEMBER [Geography].[Country].&[United States] )  
            ,GROUP [Country1].[CountryXl_Grp_2]   
                ( MEMBER [Geography].[Country].&[France]  
                  ,MEMBER [Geography].[Country].&[Germany]  
                  ,MEMBER [Geography].[Country].&[United Kingdom] )   
            )   
   )  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX データ定義ステートメント&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)   
 [CREATE GLOBAL CUBE ステートメント&#40;MDX&#41;](../mdx/mdx-data-definition-create-global-cube.md)  
  
  
