---
title: Charset プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Charset
helpviewer_keywords:
- Charset property [ADO]
ms.assetid: e42507cb-9b46-4ce4-8191-2948eaf14ca2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 69d65a5330ea83b955629cd9de9684ecc47906ec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920083"
---
# <a name="charset-property-ado"></a>Charset プロパティ (ADO)
文字セットを示します、テキストの内容[Stream](../../../ado/reference/ado-api/stream-object-ado.md)の内部バッファー内の記憶域に変換する必要があります、 **Stream**オブジェクト。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を**文字列**文字を指定する値の設定先の内容、 **Stream**変換されます。 既定値は**Unicode**します。 使用できる値は、インターネット文字セット名 (たとえば、「iso 8859 1」、「Windows 1252」、およびなど) として、インターフェイスを介して渡される一般的な文字列です。 システムで認識されている文字セット名の一覧は、Windows レジストリに HKEY_CLASSES_ROOT\MIME\Database\Charset のサブキーを参照してください。  
  
## <a name="remarks"></a>コメント  
 テキストで**Stream**オブジェクト、文字セットで指定されたテキスト データが格納されている、 **Charset**プロパティ。 既定では Unicode です。 **Charset**プロパティに入ってくるデータを変換するために使用される、 **Stream**または今後のうち、 **Stream**します。 たとえば場合、 **Stream** ISO 8859-1 のデータと、BSTR にデータをコピーすることが含まれています、 **Stream**オブジェクトは、データを Unicode に変換されます。 この逆も当てはまります。  
  
 開くのため**Stream**、現在[位置](../../../ado/reference/ado-api/position-property-ado.md)の先頭にある必要があります、 **Stream** (0) に設定することを**Charset**します。  
  
 **Charset**はテキストでのみ使用**Stream**オブジェクト ([型](../../../ado/reference/ado-api/type-property-ado-stream.md)は**adTypeText**)。 場合、このプロパティは無視されます**型**は**adTypeBinary**します。  
  
 コード サンプルは、次を参照してください。[手順 4。詳細情報のテキスト ボックスに入力](../../../ado/guide/data/step-4-populate-the-details-text-box.md)します。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
