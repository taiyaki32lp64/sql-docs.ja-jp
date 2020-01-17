---
title: ParentURL プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::ParentURL
helpviewer_keywords:
- ParentURL property [ADO]
ms.assetid: 65120ce6-3900-4cd4-b322-3b9816d74737
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 54b2db44fe2e1971356f96d33aa8de0b02781b1e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931640"
---
# <a name="parenturl-property-ado"></a>ParentURL プロパティ (ADO)
親を指す絶対 URL 文字列を示す[レコード](../../../ado/reference/ado-api/record-object-ado.md)、現在の**レコード**オブジェクト。  
  
## <a name="return-value"></a>戻り値  
 返します、**文字列**、親の URL を示す値**レコード**します。  
  
## <a name="remarks"></a>コメント  
 **ParentURL**プロパティは、開くために使用するソースによって異なります。、**レコード**オブジェクト。 たとえば、**レコード**によって参照されるディレクトリの相対パス名を含むソースを開くことができます、 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)プロパティ。  
  
 たとえば、"first"の下のフォルダーが含まれるは「次」。 開く、**レコード**次の構文を使用してオブジェクト。  
  
```  
record.ActiveConnection = "https://first"  
record.Open "second"  
```  
  
 値、 `the` **ParentURL**プロパティは`"https://first"`と同じ**ActiveConnection**します。  
  
 ソースが次のように、絶対 URL を指定もできます`"https://first/second"`します。 **ParentURL**プロパティは、 `"https://first"`、その上のレベル`"second"`します。  
  
 このプロパティは、場合、null 値にすることがあります。  
  
-   現在のオブジェクトの親が存在しません。たとえば場合、**レコード**オブジェクトは、ディレクトリのルートを表します。  
  
-   **レコード**オブジェクトは、URL で指定できないエンティティを表します。  
  
 このプロパティは読み取り専用です。  
  
> [!NOTE]
>  このプロパティはなど、ドキュメントのソース プロバイダーによってサポートのみ、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)します。 詳細については、次を参照してください。[レコードとプロバイダー提供のフィールド](../../../ado/guide/data/records-and-provider-supplied-fields.md)します。  
  
> [!NOTE]
>  Http スキームを使用して Url が自動的に呼び出さ、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)します。 詳細については、次を参照してください。[絶対と相対 Url](../../../ado/guide/data/absolute-and-relative-urls.md)します。  
  
> [!NOTE]
>  現在のレコードが、ADO からのデータ レコードを含むかどうか**レコード セット**へのアクセス、 **ParentURL**プロパティ URL がないことを示す、実行時エラーが発生します。  
  
## <a name="applies-to"></a>適用対象  
 [Record オブジェクト (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
