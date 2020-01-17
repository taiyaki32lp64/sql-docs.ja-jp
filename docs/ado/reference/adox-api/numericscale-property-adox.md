---
title: NumericScale プロパティ (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::PutNumericScale
- _Column::GetNumericScale
- _Column::NumericScale
- _Column::put_NumericScale
- _Column::get_NumericScale
helpviewer_keywords:
- NumericScale property [ADOX]
ms.assetid: 573ee5d1-57c7-4a27-be79-a0e12944ad9b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 16fdefcb06d2b1b90dfc3da39aaf6b1c9659debc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67965748"
---
# <a name="numericscale-property-adox"></a>NumericScale プロパティ (ADOX)
列の数値の小数点以下桁数を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定し、返します、**バイト**、列のデータ値の小数点以下桁数の値と、[型](../../../ado/reference/adox-api/type-property-column-adox.md)プロパティは**adNumeric**または**adDecimal**します。 **NumericScale**の他のすべてのデータ型は無視されます。  
  
## <a name="remarks"></a>コメント  
 既定値は、ゼロ (0) です。  
  
 **NumericScale**は読み取り専用の[列](../../../ado/reference/adox-api/column-object-adox.md)オブジェクトが既にコレクションに追加します。  
  
## <a name="applies-to"></a>適用対象  
 [Column オブジェクト (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
  
## <a name="see-also"></a>関連項目  
 [ADOX のコード例:NumericScale および Precision プロパティの例 (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Type プロパティ (列) (ADOX)](../../../ado/reference/adox-api/type-property-column-adox.md)
