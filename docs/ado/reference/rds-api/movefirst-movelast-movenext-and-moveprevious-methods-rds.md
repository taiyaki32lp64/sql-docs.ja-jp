---
title: MoveFirst、MoveLast、MoveNext、MovePrevious メソッド (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- MoveLast method [RDS]
- MovePrevious method [RDS]
- MoveFirst method [RDS]
- MoveNext method [RDS]
ms.assetid: 45c80bb5-136f-4204-9df2-78740fa55574
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8e99ff17cad2bebcfaed509788ea3721ddfeb0ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963884"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-rds"></a>MoveFirst、MoveLast、MoveNext、MovePrevious メソッド (RDS)
First、last に移動します。 次に、または前のレコードを、指定した[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DataControl.Recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
#### <a name="parameters"></a>パラメーター  
 *DataControl*  
 オブジェクト変数を表す、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクト。  
  
## <a name="remarks"></a>コメント  
 使用することができます、**移動**メソッド、 **rds.DataControl** Web ページ上のデータ バインド コントロールでデータ レコード間を移動するオブジェクト。 たとえば、表示する、 **Recordset**にバインドしてグリッドに、 **rds.DataControl**オブジェクト。 ユーザーがクリックして、最初に移動、最後、次に、最初、Last、Next、および前のボタンを含めることができますし、表示されている前のレコードまたは**レコード セット**します。 呼び出すことによって、これを行う、 **MoveFirst**、 **MoveLast**、 **MoveNext**、および**MovePrevious**のメソッド、 **rds.DataControl**最初、Last、Next、および前のボタンの onClick プロシージャでそれぞれオブジェクトします。 [アドレス帳例](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)これを行う方法を示しています。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>関連項目  
 [Move メソッド (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst、MoveLast、MoveNext、MovePrevious メソッド (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveRecord メソッド (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)


