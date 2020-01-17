---
title: キューブの書き戻し (MDX) を使用して |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- writeback [Analysis Services], cubes
- cubes [Analysis Services], modifying
- modifying cubes
- UPDATE CUBE statement
- cubes [Analysis Services], writeback
ms.assetid: ae2385fc-7fa0-4f8e-98d7-dcb0a5f0eeea
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a79e98375c27c6a3570b2fafcf424965d7a97c8d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074216"
---
# <a name="using-cube-writebacks-mdx"></a>キューブの書き戻しの使用 (MDX)
  キューブを更新するには、[UPDATE CUBE](/sql/mdx/mdx-data-manipulation-update-cube) ステートメントを使用します。 このステートメントを使用すると、特定の値で組を更新できます。 UPDATE CUBE ステートメントを使って効果的にキューブを更新するには、ステートメントの構文、発生し得るエラー条件、および更新操作がキューブに与える影響を理解しておく必要があります。  
  
## <a name="update-cube-statement-syntax"></a>UPDATE CUBE ステートメントの構文  
 UPDATE CUBE ステートメントの構文は、以下のとおりです。  
  
```  
UPDATE [CUBE] <Cube_Name> SET <tuple>.VALUE = <value> [,<tuple>.VALUE = <value>...]  
 [ USE_EQUAL_ALLOCATION | USE_EQUAL_INCREMENT |  
  USE_WEIGHTED_ALLOCATION [BY <weight value_expression>] |  
  USE_WEIGHTED_INCREMENT [BY <weight value_expression>] ]   
```  
  
 組の座標の完全なセットが指定されていない場合、未指定の座標には階層の既定のメンバーが使用されます。 指定される組では、 [Sum](/sql/mdx/sum-mdx) 関数を使って集計されるセルを参照する必要があり、計算されるメンバーをいずれかのセルの座標として使用することはできません。  
  
 UPDATE CUBE ステートメントは、アトミック セルに対する個々のセルの一連の書き戻し操作を生成するサブルーチンのようなものと考えることができます。 その後、これらすべての個々の書き戻し操作は、指定された合計にロール アップします。  
  
> [!NOTE]  
>  更新されるセルが重ならない場合は、`Update Isolation Level` 接続文字列プロパティを使用して、UPDATE CUBE のパフォーマンスを向上させることができます。 詳細については、「 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> 」を参照してください。  
  
## <a name="example"></a>例  
 Adventure Works キューブの Sales Targets メジャー グループを使って UPDATE CUBE をテストできます。 このメジャー グループは、UPDATE CUBE の要件である SUM によって集計されたメジャーで構成されます。  
  
1.  Adventure Works データベースの Sales Targets メジャー グループに対して書き戻しを有効にします。 Management Studio で、メジャー グループを右クリックし、 **[書き戻しオプション]** をポイントして、 **[書き戻しの有効化]** をクリックします。  
  
     Writeback フォルダーに新しい書き戻しテーブルが示されます。 テーブル名は WriteTable_Fact Sales Quota です。  
  
2.  MDX クエリ ウィンドウを開きます。 元の値を表示するために次の SELECT ステートメントを実行します。  
  
    ```  
    SELECT [Measures].[Sales Amount Quota] on 0 ,  
    [Employee].[Employee Department].[Title].&[Sales Representative].children on 1  
    FROM [Adventure Works]  
  
    ```  
  
     各代表者の販売ノルマを表示する必要があります。  
  
3.  新しい値を書き戻すために Update Cube ステートメントを実行します。 この例では、販売量ノルマを 0 に設定しています。 新しい値は 0 であるため、割り当て方法は指定しません。  
  
    ```  
    UPDATE CUBE [Adventure Works]   
    SET ([Measures].[Sales Amount Quota], [Employee].[Employee Department].[Department].&[Sales]) = 0  
  
    ```  
  
4.  SELECT ステートメントを再実行します。 これで、ノルマに 0 が表示されます。  
  
 書き戻し値は、現在のセッションに制限されます。 ユーザーおよびセッション間で値を永続化するために、書き戻しテーブルを処理します。 Management Studio で、[WriteTable_Fact Sales Quota] を右クリックし、 **[処理]** をクリックします。  
  
 割り当て方法を指定するには、新しい値が 0 より大きいことが必要です。 この例では、Sales Amount Quota の新しい値は 200 万であり、この割り当て方法ではこの金額がすべての販売員に配分されます。  
  
```  
UPDATE CUBE [Adventure Works]   
SET ([Measures].[Sales Amount Quota], [Employee].[Employee Department].[Department].&[Sales]) = 2000000   
USE_EQUAL_ALLOCATION  
```  
  
## <a name="error-conditions"></a>エラー条件  
 次の表は、書き戻しが失敗する原因と、エラーの結果を示しています。  
  
|エラー条件|結果|  
|---------------------|------------|  
|同じディメンションにあるが、互いに対して存在しないメンバーが更新に含まれる場合。|更新は失敗します。 参照されるセルはキューブ空間に格納されません。|  
|符号なしの型のメジャーに由来するメジャーが更新に含まれる場合。|更新は失敗します。 増分変更を行うには、メジャーが負の値をとることができなければなりません。|  
|合計以外の集計が行われるメジャーが更新に含まれる場合。|エラーが発生します。|  
|サブキューブに対する更新が試行された場合。|エラーが発生します。|  
  
## <a name="affect-of-cube-changes"></a>キューブの変更の影響  
 次のような変更は、書き戻しに影響を与えません。  
  
-   キューブ、キューブのメジャー グループ、またはキューブのディメンションの処理。  
  
-   いずれかのディメンションへの属性の追加。  
  
-   新しいディメンションの追加。  
  
-   書き戻しを含まないディメンションの削除。  
  
-   階層の追加、変更、または削除。  
  
-   新しいメジャーの追加。  
  
 次のような変更は、書き戻しデータを削除しない限り行うことはできません。  
  
-   書き戻しに含まれる属性や、その属性階層の削除。 これには、属性または属性階層を明示的に削除することや、属性の親ディメンションを削除することが含まれます。  
  
-   書き戻しに含まれるメジャーの削除。  
  
-   書き戻しに含まれるディメンションに、`(All)` レベルを使用せずに属性を追加すること。  
  
-   書き戻しに含まれるディメンションの粒度の変更。  
  
## <a name="see-also"></a>参照  
 [データの変更 &#40;MDX&#41;](mdx-data-modification-modifying-data.md)  
  
  
