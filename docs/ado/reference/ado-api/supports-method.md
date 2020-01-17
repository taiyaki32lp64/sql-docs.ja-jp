---
title: メソッドをサポートしています |。Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Supports
- Recordset15::Supports
helpviewer_keywords:
- Supports method [ADO]
ms.assetid: 298fc41c-0b55-42fc-b373-c5133b4da6a5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cce5ab3b735d3c641da4a6234e860d0528f107c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936702"
---
# <a name="supports-method"></a>Supports メソッド
指定したかどうかを判断します[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトは、特定の種類の機能をサポートしています。  
  
## <a name="syntax"></a>構文  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="return-value"></a>戻り値  
 返します、**ブール**で識別されるすべての機能かどうかを示す値、 *CursorOptions*引数が、プロバイダーによってサポートされています。  
  
#### <a name="parameters"></a>パラメーター  
 *CursorOptions*  
 A**長い**の 1 つまたは複数で構成される式[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)値。  
  
## <a name="remarks"></a>コメント  
 使用して、**サポート**機能の種類を特定する方法、**レコード セット**サポートしています。 場合、**レコード セット**オブジェクトが定数に対応するが、機能をサポートしている*CursorOptions*、**サポート**メソッドを返します**True。** . 返しますそれ以外の場合、 **False**します。  
  
> [!NOTE]
>  ただし、**サポート**メソッドが返す可能性があります**True**の特定の機能が保証されないこと、プロバイダーが利用できる機能は、あらゆる状況下で。 **サポート**メソッドは単に特定の条件が満たされたと仮定した場合で、指定された機能をプロバイダーがサポートできるかどうかを返します。 など、**サポート**メソッドを示します、**レコード セット**オブジェクトが、カーソルが一部の列は更新できない複数のテーブル結合に基づいている場合でも、更新プログラムをサポートします。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [Supports メソッドの例 (VB)](../../../ado/reference/ado-api/supports-method-example-vb.md)   
 [Supports メソッドの例 (vc++)](../../../ado/reference/ado-api/supports-method-example-vc.md)   
 [CursorType プロパティ (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
