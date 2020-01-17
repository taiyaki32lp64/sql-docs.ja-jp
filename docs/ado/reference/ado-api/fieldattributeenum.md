---
title: FieldAttributeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldAttributeEnum
helpviewer_keywords:
- FieldAttributeEnum enumeration [ADO]
ms.assetid: 6e34d886-005a-40dc-bd5c-6adcbf81e5cd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0d375ed3dd4ea7ae7e2e5405d1feec962c5f56ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918701"
---
# <a name="fieldattributeenum"></a>FieldAttributeEnum
1 つまたは複数の属性を指定します、[フィールド](../../../ado/reference/ado-api/field-object.md)オブジェクト。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adFldCacheDeferred**|0x1000|プロバイダーは、フィールドの値をキャッシュし、キャッシュからそれ以降の読み取りが行われることを示します。|  
|**adFldFixed**|0x10|フィールドが固定長のデータが含まれていることを示します。|  
|**adFldIsChapter**|0x2000|フィールドに、この親フィールドに関連する特定の子レコード セットを指定するチャプター値が含まれていることを示します。 通常」の章のフィールドは、データの整形やフィルターで使用されます。|  
|**adFldIsCollection**|0x40000|フィールドを指定、レコードによって表されるリソースがテキスト ファイルなどの単純なリソースではなく、フォルダーなどの他のリソースのコレクションを示します。|  
|**adFldKeyColumn**|0x8000|列の主キーの一部またはすべてフィールドを指定することを示します。|  
|**adFldIsDefaultStream**|0x20000|フィールドに、レコードによって表されるリソースの既定のストリームが含まれていることを示します。 たとえば、既定のストリームは、ルート URL を指定すると自動的に提供される Web サイト上のルート フォルダーの HTML コンテンツを指定できます。|  
|**adFldIsNullable**|0x20|フィールドが null 値を受け入れることを示します。|  
|**adFldIsRowURL**|0x10000|フィールドに、リソース レコードによって表されるデータ ストアからの名前を示す URL が含まれていることを示します。|  
|**adFldLong**|0x80|フィールドがフィールド長のバイナリであることを示します。 使用できることを示します、 [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)と[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)メソッド。|  
|**adFldMayBeNull**|0x40|フィールドから null 値を読み取ることを示します。|  
|**adFldMayDefer**|0x2|フィールドが遅延することを示しますが、フィールドの値は、レコード全体ですが明示的にアクセスする場合にのみ、データ ソースから取得されません。|  
|**adFldNegativeScale**|0x4000|フィールドが負数の拡大縮小値をサポートする列の数値を表すことを示します。 小数点以下桁数がで指定された、 [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)プロパティ。|  
|**adFldRowID**|0x100|フィールドに書き込むことはできませんし、行 (レコード番号、一意の識別子、やなど) を識別する以外の意味のある値を持つ永続的な行識別子が含まれていることを示します。|  
|**adFldRowVersion**|0x200|フィールドに、ある種更新プログラムを追跡するために使用される日付または時刻のスタンプにはが含まれていることを示します。|  
|**adFldUnknownUpdatable**|0x8|プロバイダーがフィールドを記述することができるかどうかを判断できないことを示します。|  
|**adFldUnspecified**|-1 0 xffffffff|プロバイダーに、フィールドの属性が指定されていないことを示します。|  
|**adFldUpdatable**|0x4|フィールドに記述できることを示します。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 パッケージ: **com.ms.wfc.data**  
  
|定数|  
|--------------|  
|AdoEnums.FieldAttribute.CACHEDEFERRED|  
|AdoEnums.FieldAttribute.FIXED|  
|AdoEnums.FieldAttribute.ISNULLABLE|  
|AdoEnums.FieldAttribute.LONG|  
|AdoEnums.FieldAttribute.MAYBENULL|  
|AdoEnums.FieldAttribute.MAYDEFER|  
|AdoEnums.FieldAttribute.NEGATIVESCALE|  
|AdoEnums.FieldAttribute.ROWID|  
|AdoEnums.FieldAttribute.ROWVERSION|  
|AdoEnums.FieldAttribute.UNKNOWNUPDATABLE|  
|AdoEnums.FieldAttribute.UNSPECIFIED|  
|AdoEnums.FieldAttribute.UPDATABLE|  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[Append メソッド (ADO)](../../../ado/reference/ado-api/append-method-ado.md)|[Attributes プロパティ (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)|
