---
title: セルのオブジェクト (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell
helpviewer_keywords:
- Cell object [ADO MD]
ms.assetid: dcc2f044-b785-4a29-9bc5-b673f66eedf9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bbf97a4095f2295b8851f87ba20ab083938e70ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947742"
---
# <a name="cell-object-ado-md"></a>Cell オブジェクト (ADO MD)
セル セットに含まれる軸座標が交差する位置にデータを表します。  
  
## <a name="remarks"></a>コメント  
 A**セル**によってオブジェクトが返される、[項目](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)のプロパティを[セルセット](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)オブジェクト。  
  
 コレクションのプロパティと、**セル**オブジェクトを次を行うことができます。  
  
-   内のデータを返す、**セル**で、[値](../../../ado/reference/ado-md-api/value-property-ado-md.md)プロパティ。  
  
-   表示の書式設定を表す文字列を返す、**値**プロパティを[FormattedValue](../../../ado/reference/ado-md-api/formattedvalue-property-ado-md.md)プロパティ。  
  
-   序数値を返す、**セル**内、**セルセット**で、[序数](../../../ado/reference/ado-md-api/ordinal-property-ado-md-cell.md)プロパティ。  
  
-   位置を決定、**セル**内、 [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)で、[位置](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)コレクション。  
  
-   その他の情報の取得、**セル**標準の ADO を使用した[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)コレクション。  
  
 **プロパティ**コレクションには、プロバイダーが指定したプロパティが含まれています。 次の表は、使用可能な可能性があるプロパティを一覧表示します。 実際のプロパティの一覧は、プロバイダーの実装によって異なる場合があります。 使用可能なプロパティの詳細な一覧については、プロバイダーのドキュメントを参照してください。  
  
|名前|説明|  
|----------|-----------------|  
|背景色|セルを表示するときに使用する背景色です。|  
|FontFlags|フォントの効果を指定するビットマスク。|  
|フォント名|セルの値を表示するために使用するフォントです。|  
|フォントサイズ|セルの値を表示するために使用するフォント サイズです。|  
|ForeColor|セルを表示するときに使用される前景色。|  
|FormatString|書式設定された文字列値します。|  
  
 このセクションには、次のトピックが含まれています。  
  
-   [プロパティ、メソッド、およびイベント](../../../ado/reference/ado-md-api/cell-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [軸の例 (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Cellset オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Positions コレクション (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)   
 [Properties コレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
