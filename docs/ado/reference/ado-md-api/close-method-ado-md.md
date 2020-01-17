---
title: Close メソッド (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Close
- Cellset::Close
helpviewer_keywords:
- Close method [ADO MD]
ms.assetid: a3aa594d-f9d4-4654-8625-ec20153ff5d9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 09e83fd8645a5c0ab604a640478c4cced4870742
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949810"
---
# <a name="close-method-ado-md"></a>Close メソッド (ADO MD)
開いているセルセットを閉じます。  
  
## <a name="syntax"></a>構文  
  
```  
  
Cellset.Close  
```  
  
## <a name="remarks"></a>コメント  
 使用して、**閉じます**を終了するメソッド、[セルセット](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)オブジェクトに関連するいずれかでデータを含む、関連付けられているデータはリリース[セル](../../../ado/reference/ado-md-api/cell-object-ado-md.md)、[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)、[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)、または[メンバー](../../../ado/reference/ado-md-api/member-object-ado-md.md)オブジェクト。 閉じる、**セルセット**メモリ; からは削除されません、プロパティの設定を変更し、後でもう一度開きます。 メモリからオブジェクトを完全に排除するに、オブジェクト変数を設定します。 **Nothing**します。  
  
 後で呼び出すことができます、[オープン](../../../ado/reference/ado-md-api/open-method-ado-md.md)メソッドを再度開く、**セルセット**同一または別を使用してソース文字列。 中に、**セルセット**の任意のプロパティを取得または基になるデータを参照するメソッドを呼び出す、オブジェクトが閉じているか、メタデータには、エラーが生成されます。  
  
## <a name="applies-to"></a>適用対象  
 [CellSet オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>関連項目  
 [軸オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [Cell オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [メンバー オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)   
 [Open メソッド (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)   
 [位置オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/position-object-ado-md.md)   
 [State プロパティ (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
