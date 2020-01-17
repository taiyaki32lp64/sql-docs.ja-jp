---
title: MoveRecord メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::MoveRecord
- _Record::raw_MoveRecord
helpviewer_keywords:
- MoveRecord method [ADO]
ms.assetid: 6d2807b0-b861-4583-bcaf-fb0b82e0f2d0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 157e38c2c9c23ff8f7e92af40385b0962c6dcb70
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918074"
---
# <a name="moverecord-method-ado"></a>MoveRecord メソッド (ADO)
によって表されるエンティティの移動、[レコード](../../../ado/reference/ado-api/record-object-ado.md)別の場所にします。  
  
## <a name="syntax"></a>構文  
  
```  
  
Record.MoveRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Source*  
 任意。 A**文字列**を識別する URL を含む値、**レコード**移動します。 場合*ソース*を省略するか、空の文字列、これによって表されるオブジェクトを指定します**レコード**が移動します。 たとえば場合、**レコード**ファイル、ファイルの内容を表しますがで指定された場所に移動されます*先*します。  
  
 *変換先*  
 任意。 A**文字列**場所を指定する URL を含む値、*ソース*は移動されます。  
  
 *UserName*  
 任意。 A**文字列**値が必要な場合へのアクセスを承認するユーザー ID を含む*先*します。  
  
 *Password*  
 任意。 A**文字列**必要な場合は、以下のことを確認するためのパスワードを格納している*UserName*します。  
  
 *[オプション]*  
 任意。 A [MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md)値が既定値は**adMoveUnspecified**します。 このメソッドの動作を指定します。  
  
 *Async*  
 任意。 A**ブール**値と**True**、この操作を非同期にする必要がありますを指定します。  
  
## <a name="return-value"></a>戻り値  
 **文字列**値です。 値では通常、*先*が返されます。 ただし、返される正確な値は、プロバイダーによって異なります。  
  
## <a name="remarks"></a>コメント  
 値*ソース*と*先*することはできませんと同じです。 それ以外の場合、実行時エラーが発生します。 少なくとも、サーバー、パス、およびリソースの名前が異なる必要があります。  
  
 インターネット、パブリッシング用プロバイダーを使用して移動、ファイルに対しては、このメソッドはそれ以外の場合に指定されていない場合に移動されるファイル内のすべてのハイパー テキスト リンクを更新*オプション*します。 このメソッドは失敗*先*しない限り (たとえば、ファイルまたはディレクトリ)、既存のオブジェクトを識別する**adMoveOverWrite**が指定されて。  
  
> [!NOTE]
>  使用して、 **adMoveOverWrite**慎重オプションします。 たとえば、ディレクトリにファイルを移動するときに、このオプションを指定するディレクトリを削除されファイルに置き換えます。  
  
 特定の属性、**レコード**オブジェクトなど、 [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)この操作の完了後、プロパティは更新されません。 更新、**レコード**オブジェクトのプロパティを閉じて、**レコード**、もう一度開いて、ファイルまたはディレクトリを移動した場所の URL。  
  
 この場合**レコード**から取得された、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)、移動したファイルまたはディレクトリの新しい場所がすぐに反映されません、**レコード セット**します。 更新、**レコード セット**を閉じてから再度開くことができます。  
  
> [!NOTE]
>  Http スキームを使用して Url が自動的に呼び出さ、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)します。 詳細については、次を参照してください。[絶対と相対 Url](../../../ado/guide/data/absolute-and-relative-urls.md)します。  
  
## <a name="applies-to"></a>適用対象  
 [Record オブジェクト (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Move メソッド (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst、MoveLast、MoveNext、MovePrevious メソッド (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst、MoveLast、MoveNext、MovePrevious メソッド (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)
