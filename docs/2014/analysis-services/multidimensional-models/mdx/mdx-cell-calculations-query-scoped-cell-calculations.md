---
title: クエリ スコープのセル計算 (MDX) を作成する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- WITH keyword
- query-scoped cell calculations [MDX]
ms.assetid: 45987daa-4400-41e9-add7-2428fd75709b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 575bac6ba111259fe20540fd0b40f193f0a54b38
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074423"
---
# <a name="creating-query-scoped-cell-calculations-mdx"></a>クエリ スコープのセル計算の作成 (MDX)
  計算されるセルをクエリのコンテキストの中で記述するには、多次元式 (MDX) の `WITH` キーワードを使用します。 `WITH` キーワードの構文は、以下のとおりです。  
  
```  
WITH CELL CALCULATION Cube_Name.CellCalc_Identifier  String_Expression  
```  
  
 `CellCalc_Identifier` の値は、計算されるセルの名前です。 `String_Expression` の値には、直交する 1 次元の MDX セット式の一覧を指定します。 それぞれの式は次の表に示されているカテゴリのいずれかに解決する必要があります。  
  
|カテゴリ|説明|  
|--------------|-----------------|  
|空セット|空セットに解決される MDX セット式。 この場合、計算されるセルのスコープはキューブ全体です。|  
|単一メンバー セット|1 つのメンバーに解決される MDX セット式。|  
|レベル メンバーのセット|単一レベルのメンバーに解決される MDX セット式。 このようなセット式の例は、 *Level_Expression*します。`Members` MDX 関数です。 計算されるメンバーを含めるには使用、 *Level_Expression*します。`AllMembers` MDX 関数です。 詳細については、「[AllMembers (MDX)](/sql/mdx/allmembers-mdx)」を参照してください。|  
|子孫のセット|指定したメンバーの子孫に解決される MDX セット式。 このようなセット式の例は、 `Descendants`(*メンバー式*、 *Level_Expresion*、 *Desc_Flag*) MDX 関数です。 詳細については、「[Descendants (MDX)](/sql/mdx/descendants-mdx)」を参照してください。|  
  
 `String_Expression` 引数でディメンションが記述されていない場合、MDX は計算サブキューブの構築のためにすべてのメンバーが含まれていると想定します。 したがって、 `String_Expression` 引数が NULL の場合、計算されるセルの定義はキューブ全体に適用されます。  
  
 `MDX_Expression` 引数には、 `String_Expression` 引数で定義したすべてのセルのセル値に評価される MDX 式を指定します。  
  
## <a name="additional-considerations"></a>その他の注意点  
 `CONDITION` プロパティによって指定された計算条件は、MDX によって一度だけ処理されます。 このように一度だけの処理を行うことにより、複数の計算されるセルの定義を評価する場合、特に計算されるセルがキューブ パス間で重複している場合のパフォーマンスが向上します。  
  
 この一度だけの処理がいつ行われるかは、計算されるセルの定義の作成スコープによって異なります。  
  
-   キューブの一部としてグローバル スコープで作成した計算条件は、MDX によってそのキューブの処理時に処理されます。 キューブ内でセルがなんらかの方法で修正され、そのセルが計算されるセルの定義の計算サブキューブに含まれている場合は、キューブが再処理されるまで正確な計算条件が得られないことがあります。 たとえば、書き戻しによってセルの修正が発生する場合があります。 計算条件は、キューブと共に再処理されます。  
  
-   セッション スコープで作成された計算条件は、MDX によってセッション中のステートメントの実行時に処理されます。 グローバルに作成された計算されるセルの定義と同様に、この種の計算されるセルの定義の場合も、セルが修正されると正確な計算条件が得られないことがあります。  
  
-   クエリ スコープで作成された計算条件は、MDX によってクエリの実行時に処理されます。 この場合もセルの修正に関する問題が当てはまりますが、MDX クエリの実行は処理時間が少ないため、データ待機時間に伴う問題は最小限に抑えられます。  
  
 一方、計算式は、計算されるセルの定義に含まれるセルを伴うキューブに対して MDX クエリが実行されるたびに MDX によって処理されます。 この処理は、作成スコープに関係なく行われます。  
  
## <a name="see-also"></a>参照  
 [CREATE CELL CALCULATION ステートメント (MDX)](/sql/mdx/mdx-data-definition-create-cell-calculation)  
  
  
