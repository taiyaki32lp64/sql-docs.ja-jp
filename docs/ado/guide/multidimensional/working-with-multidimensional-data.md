---
title: 多次元データを扱う |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional data [ADO]
ms.assetid: 84387746-aa3e-44fd-ad6c-a8214a6966dc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 61f3e34af2a9331118b41657cf958021b972b04a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923131"
---
# <a name="working-with-multidimensional-data"></a>多次元データの操作
A*セルセット*多次元データに対するクエリの結果です。 軸、以下の 4 つの軸は、通常、通常 2 つまたは 3 つのコレクションで構成されます。 *軸*を探すか、キューブ内の特定の値をフィルター処理に使用される 1 つまたは複数のディメンションのメンバーのコレクションです。  
  
 A*位置*軸に沿ったポイントです。 1 つのディメンションで構成される軸では、それらの位置は、ディメンション メンバーのサブセットです。 軸は、1 つ以上のディメンションのかどうかは、各位置が、複合エンティティは、 *n* where 部分*n*その軸に沿った指向ディメンションの数です。 位置の各部分は、1 つの構成要素であるディメンションのメンバーです。  
  
 たとえば、売上データを格納しているキューブから、Geography、Product のディメンションは、セルセットの x 軸に沿って方向は、場合この軸に沿った位置含めることができます"USA"と「コンピューター」メンバー この例では、x 軸に沿った位置を決定するが各ディメンションのメンバーが軸に沿った指向が必要です。  
  
 A*セル*は軸の座標が交差する位置に配置されているオブジェクトです。 各セルには、データ自体、書式設定された文字列 (セルのデータの表示可能な項目のフォーム)、およびセルの序数値を含む、関連付けられている情報の複数の部分。 (各セルはセルセットの一意の序数値です。 セル セットの最初のセルの序数値は 0、8 つの列を含むセル セットの 2 行目で一番左のセル序数値は 8 になります。)  
  
 たとえば、キューブには、次の 6 つのディメンション (で指定された例から、このキューブ スキーマが若干異なりますに注意してください。[多次元スキーマの概要とデータ](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md))。  
  
-   営業担当者  
  
-   大陸、国、州、および、geography (自然階層)  
  
-   四半期四半期、月、日  
  
-   Years  
  
-   メジャーの Sales、PercentChange、BudgetedSales  
  
-   Products  
  
 次のセル セットでは、1991 すべての製品の売上を表します。  
  
> [!NOTE]
>  セルの値の例では、最初の桁が x 軸の位置と y 軸の位置に、2 番目の数字を表す軸位置の序数の順序付けされたペアとして表示できます。  
  
 このセル セットの特性は次のとおりです。  
  
-   軸ディメンション:四半期数、販売員、Geography  
  
-   ディメンションをフィルター処理します。メジャー、年の製品  
  
-   2 つの軸:(X、または軸 0) の列と行 (y または軸 1)  
  
-   x 軸: 入れ子になった 2 つの販売員と Geography ディメンションは、  
  
-   y 軸:ディメンションの四半期  
  
 X 軸では、2 つの入れ子になったディメンションがあります。販売員と Geography です。 Geography 型から 4 つのメンバーが選択されます。シアトル、ボストン、米国南部、および日本です。 2 つのメンバーは、営業担当者から選択されます。バレンタイン Nash. この軸 (2 * 8 = 4) の 8 つの位置の合計が生成されます。  
  
 各座標は、販売員のディメンションから 1 つと、Geography ディメンションからの 2 つのメンバーの位置として表されます。  
  
```console
(Valentine, Seattle), (Valentine, Boston), (Valentine, USA_North),  
(Valentine, Japan), (Nash, Seattle), (Nash, Boston), (Nash, USA_North),  
(Nash, Japan)  
```  
  
 Y 軸には、次の 8 つの位置を含む 1 つだけのディメンションがあります。  
  
```console
Jan, Feb, Mar, Qtr2, Qtr3, Oct, Nov, Dec  
```  
  
 セル セット、セル、軸、および位置はすべてで表される ADO MD で対応するオブジェクト。[セルセット](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)、[セル](../../../ado/reference/ado-md-api/cell-object-ado-md.md)、[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)、および[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)します。  
  
## <a name="see-also"></a>関連項目  
 [ADO MD オブジェクト モデル](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (多次元) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [多次元スキーマとデータの概要](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [ADO MD を使用したプログラミング](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [ADO MD と ADO の併用](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)
