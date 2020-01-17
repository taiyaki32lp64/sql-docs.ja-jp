---
title: レコード セット内を移動する方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- Recordset object [ADO], moving
- MovePrevious method [ADO]
ms.assetid: 9f8cf1b2-3def-453f-a0ff-4646c5f15262
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ea83f40c6d6e595277a173c181c24f33e382393
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924886"
---
# <a name="more-ways-to-move-in-a-recordset"></a>レコードセット内を移動する他の方法
次の 4 つのメソッドを移動、またはスクロールしてで使用される、 **Recordset**:[MoveFirst、MoveLast、MoveNext、MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)します。 (これらのメソッドの一部は順方向専用カーソルで使用できます。)  
  
 **MoveFirst**で最初のレコードを現在のレコードの位置を変更、 **Recordset**します。 **MoveLast**に現在のレコードが最後の位置の変更を記録、 **Recordset**します。 使用する**MoveFirst**または**MoveLast**、 **Recordset**オブジェクトには、ブックマークまたは旧バージョンとカーソルの動きをサポートする必要があります。 それ以外の場合、メソッドの呼び出しでエラーが発生します。  
  
 **MoveNext**転送を現在のレコードの位置に 1 つの場所に移動します。 最後の場合の記録を呼び出すと**MoveNext**、 **EOF**に設定されます**True**します。 **MovePrevious**現在のレコード 1 つの場所との下位の位置に移動します。 呼び出すと、最初のレコードではかどうか**MovePrevious**、 **BOF**に設定されます**True**します。 確認することをお勧め、 **EOF**と**BOF**これらのメソッドを使用する場合のプロパティのいずれかの端を移動する場合、レコードの現在の有効な位置にカーソルを戻す移動して、 **Recordset**、次のようにします。  
  
```  
. . .  
oRs.MoveNext  
If oRs.EOF Then oRs.MoveLast  
. . .   
```  
  
 またはの場合、 **MovePrevious**メソッド。  
  
```  
. . .   
oRs.MovePrevious  
If oRs.BOF Then oRs.MoveFirst  
. . .  
```  
  
 場合で、**レコード セット**がフィルター処理または並べ替え位置が変更される場合も、現在のレコードのデータが変更されました。 このような場合、 **MoveNext**メソッドは通常、動作しますが、位置が移動した 1 つであるに注意してください古い位置ではなく、新しい位置から転送を記録します。 など、レコードは、並べ替えられたの末尾に移動するように、現在のレコード内のデータを変更する**レコード セット**、呼び出すことを意味**MoveNext**結果を現在のレコードに設定する ADO では、後の最後のレコードの位置、 **Recordset** (**EOF** = **True**)。  
  
 さまざまな Move メソッドの動作、 **Recordset**内のデータをある程度は、オブジェクトの依存、**レコード セット**します。 新しいレコードを追加する、 **Recordset**がデータ ソースによって定義され、暗黙的に依存する可能性がありますが、特定の順序で、または新しいレコードのデータを明示的に最初に追加されました。 たとえば場合、並べ替えや結合を設定するクエリで行われる、**レコード セット**、内の適切な場所に新しいレコードが挿入されます、**レコード セット**します。 順序指定しない場合は明示的に作成するときに、 **Recordset**、データ ソースの実装で変更の返された行の順序を誤って変更する可能性があります。 追加、並べ替え、フィルター処理、および編集の機能で、**レコード セット**順序に影響を与えることができ、場合によって、レコード セット内の行が表示されます。  
  
 そのため、 **MoveNext**、 **MovePrevious**、 **MoveFirst**、 **MoveLast**、および**移動**はすべてその他の操作を区別は、同じ実行**Recordset**します。 ADO は、常を明示的に移動するが、場合によっては、介在する変更が難しく、その後の移動の効果を理解するまで、現在の位置を維持するために再試行してください。 呼び出す場合など、 **MoveFirst** 、並べ替えの最初の行の位置に**Recordset**降順に昇順の並べ替えを変更して、同じ行の上に残っていることが、最後の行になります**Recordset**します。 **MoveFirst**を別の行 (新しい最初の行) に移動します。  
  
 途中で特定の行を配置した場合、別の例として、**レコード セット**呼び出す**削除**を呼び出して**MoveNext**、レコードができました削除されたレコードの直後します。 呼び出し元が**MovePrevious** 、レコードが削除されたレコードがのメンバーシップがアクティブで数えられる不要になったため、現在のレコードを削除する 1 つの前、**レコード セット**します。  
  
 -現在のレコードに対して相対的に移動するメソッドのすべてのプロバイダーで一貫性のある移動セマンティクスを定義することは特に困難です**MovePrevious**、 **MoveNext**、および**の移動** - 現在のレコードのデータの変更が発生した場合。 並べ替えを操作する場合はフィルター処理など**Recordset**、他のすべてのレコードより前にそのように、現在のレコード内のデータを変更するが、変更したデータも不要になったフィルターに一致する、where をはっきりしない場合は、**MoveNext**操作から実行する必要があります。 最も安全な結論が内で相対移動操作、**レコード セット**が絶対移動よりも低く (を使用するなど**MoveFirst**または**MoveLast**) が、データの場合変更レコードの編集中は、追加、または削除します。 並べ替えとフィルター処理は、この種類の値が変わらないようにするために、主キーまたは ID に基づく必要があります。
