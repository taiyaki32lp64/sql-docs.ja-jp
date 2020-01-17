---
title: DeleteRecord メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_DeleteRecord
- _Record::DeleteRecord
helpviewer_keywords:
- DeleteRecord method [ADO]
ms.assetid: 2726498c-dbd8-4266-983b-ae7d62c39142
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 409c4e21395b7b903cf4ff03726fbd37a2a218d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919081"
---
# <a name="deleterecord-method-ado"></a>DeleteRecord メソッド (ADO)
によって表されるエンティティを削除する[レコード](../../../ado/reference/ado-api/record-object-ado.md)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Record.DeleteRecord Source, Async  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Source*  
 任意。 A**文字列**を削除する (たとえば、ファイルまたはディレクトリ) のエンティティを識別する URL を含む値です。 場合*ソース*を省略するか、空の文字列を現在によって表されるエンティティを指定します[レコード](../../../ado/reference/ado-api/record-object-ado.md)は削除されます。 場合は、レコードがコレクションのレコード ([RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)の**adCollectionRecord**、ディレクトリなど) (たとえば、サブディレクトリ) のすべての子も削除されます。  
  
 *Async*  
 任意。 A**ブール**値と**True**、削除操作を非同期に指定します。  
  
## <a name="remarks"></a>コメント  
 これによって表されるオブジェクトで操作**レコード**メソッドの完了後に失敗する可能性があります。 呼び出した後**DeleteRecord**、**レコード**ために閉じる必要がありますの動作、**レコード**予測によって、プロバイダーを更新したときになる可能性があります、**レコード**データ ソースとします。  
  
 場合は、この**レコード**から取得された、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)、この操作の結果はすぐに反映されませんし、**レコード セット**します。 更新、**レコード セット**を閉じてから再度開くこと、または実行することによって、**レコード セット** [Requery](../../../ado/reference/ado-api/requery-method.md)メソッド、 [Update](../../../ado/reference/ado-api/update-method.md)メソッド、または[再同期](../../../ado/reference/ado-api/resync-method.md)メソッド。  
  
> [!NOTE]
>  Http スキームを使用して Url が自動的に呼び出さ、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)します。 詳細については、次を参照してください。[絶対と相対 Url](../../../ado/guide/data/absolute-and-relative-urls.md)します。  
  
## <a name="applies-to"></a>適用対象  
 [Record オブジェクト (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Delete メソッド (ADO Fields コレクション)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete メソッド (ADO Parameters コレクション)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete メソッド (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)
