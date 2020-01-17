---
title: 多次元スキーマとデータの概要 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional schemas and data
ms.assetid: ce37fa06-c581-4d80-9a9b-c3aa66408909
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e4681bb9e1fd1028ee1ddc2bd7f72efc03fb6c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923186"
---
# <a name="overview-of-multidimensional-schemas-and-data"></a>多次元スキーマとデータの概要
## <a name="understanding-multidimensional-schemas"></a>多次元スキーマの理解  
 ADO MD の中心的なメタデータ オブジェクトが、*キューブ*、構造化された一連の関連するディメンション、階層、レベル、およびメンバーから構成されます。  
  
 A*ディメンション*は、独立したビジネス エンティティから派生した、多次元データベースからのデータのカテゴリ。 通常、ディメンションには、データベースのメジャーのクエリ条件として使用する項目が含まれます。  
  
 A*階層*はディメンションの集計のパスです。 ディメンションの親子関係のある、粒度の複数のレベルがあります。 階層では、これらのレベルの関係を定義します。  
  
 A*レベル*は階層内の集計の 1 ステップです。 情報の複数の層を持つディメンションでは、各レイヤーはレベルです。  
  
 A*メンバー*がディメンション内のデータ項目。 通常、キャプションを作成したり、メンバーを使用して、データベースのメジャーを記述します。  
  
 キューブがによって表される[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) ADO MD オブジェクト ディメンション、階層、レベル、およびメンバーは、対応する ADO MD オブジェクトによっても表されます。[ディメンション](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)、[階層](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)、[レベル](../../../ado/reference/ado-md-api/level-object-ado-md.md)、および[メンバー](../../../ado/reference/ado-md-api/member-object-ado-md.md)します。  
  
### <a name="dimensions"></a>ディメンション  
 キューブのディメンションは、ビジネス エンティティと、データベースでモデル化するデータの種類によって異なります。 通常、各ディメンションは、独立したエントリ ポイントまたはデータを選択するためのメカニズムです。  
  
 たとえば、売上データを含むキューブでは、次の 5 つのディメンションがあります。販売員、Geography、時刻、製品、およびメジャー。 メジャー ディメンションには、他のディメンションが分類して売上データの値をグループ化する方法を表すときに、実際の売上データの値が含まれています。  
  
 Geography ディメンションでは、次のメンバーのセットがあります。  
  
```console
{All, North America, Europe, Canada, USA, UK, Germany, Canada-West,  
Canada-East, USA-NW, USA-SW, USA-NE, USA-SE, England, Scotland,   
Wales,Ireland, Germany-North, Germany-South, Ottawa, Toronto,   
Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston,   
Shreveport, Miami, Boston, New York, London, Dover, Glasgow,   
Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin,   
Hamburg, Munich, Stuttgart}  
```  
  
### <a name="hierarchies"></a>階層  
 階層では、ディメンションのレベルを「ロール アップ」またはグループ化の方法を定義します。 ディメンションには、1 つ以上の階層を持つことができます。 Geography ディメンションの自然階層が存在します。  
  
### <a name="levels"></a>Levels  
 前の図に示されている例の Geography ディメンションでは、各ボックスは、階層のレベルを表します。  
  
 各レベルでは、メンバーのセットを次のようには。  
  
-   世界中 `= {All}`  
  
-   大陸 `= {North America, Europe}`  
  
-   国 `= {Canada, USA, UK, Germany}`  
  
-   リージョン `= {Canada-East, Canada-West, USA-NE, USA-NW, USA-SE, USA-SW, England, Ireland, Scotland, Wales, Germany-North, Germany-South}`  
  
-   市区町村 `= {Ottawa, Toronto, Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston, Shreveport, Miami, Boston, New York, London, Dover, Glasgow, Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin, Hamburg, Munich, Stuttgart}`  
  
### <a name="members"></a>Members  
 階層のリーフ レベルのメンバーに子がありますしないと、ルート レベルのメンバーには、親はいません。 その他のすべてのメンバーは、少なくとも 1 つの親と少なくとも 1 つの子があります。 たとえば、部分、Geography ディメンションの階層ツリーを走査では、次の親子リレーションシップが得られます。  
  
-   `{All} (parent of) {Europe, North America}`  
  
-   `{North America} (parent of) {Canada, USA}`  
  
-   `{USA} (parent of) {USA-NE, USA-NW, USA-SE, USA-SW}`  
  
-   `{USA-NW} (parent of) {Boise, Seattle}`  
  
 メンバーは、ディメンションごとに 1 つまたは複数の階層に統合できます。 時間ディメンションを検討してください。 ある日レベルの Year レベルにロールアップする 2 つの方法。  
  
 この例では、もう 1 つの特性も示しています。年度の四半期の階層のあらゆるレベルでは、年、週階層の週レベルの一部のメンバーは表示されません。 そのため、階層はディメンションのすべてのメンバーを含める必要はありません。  
  
## <a name="see-also"></a>関連項目  
 [ADO MD オブジェクト モデル](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (多次元) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [ADO MD を使用したプログラミング](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [ADO MD と ADO の併用](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [多次元データの操作](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
