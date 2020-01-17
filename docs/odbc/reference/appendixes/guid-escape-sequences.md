---
title: GUID エスケープ シーケンス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], GUID
- escape sequences [ODBC], guid
- guid escape sequence [ODBC]
ms.assetid: 71d43ef9-4a31-493e-b9e0-f864e9ef3ce6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a74ed9d4dfe0afb8bf59abb11220a0677d000bfb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947582"
---
# <a name="guid-escape-sequences"></a>GUID エスケープ シーケンス
ODBC では、GUID リテラルのエスケープ シーケンスを使用します。 このエスケープ シーケンスの構文は次のとおりです。  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>Remarks  
 BNF 表記では、構文がとおりです。  
  
 *ODBC のエスケープ guid* :: =  
     *ODBC のイニシエーターは、esc キー guid* '*guid 値*' *esc 終端の ODBC*  
  
 *ODBC のイニシエーター esc* :: = {  
  
 *Esc 終端の ODBC* :: =}  
  
 *guid 値*:: =*クロック低い値の guid の区切りの時計と中間値の guid の区切りクロック高価値の guid の区切りクロック seq-値の guid の区切りノード値*  
  
 *guid の区切り*:: = -  
  
 *クロックの価値の低い*:: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *クロックと中間値*:: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *高価値のクロック*:: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *クロックの値 seq* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *クロックとノード値*:: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *hex_digit* :: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; A &#124; B &#124; C &#124; D &#124; E &#124; F  
  
 GUID データ型が、データ ソースでサポートされている場合、GUID のリテラルのエスケープ シーケンスはサポートされています。 アプリケーションを呼び出す必要があります**SQLGetTypeInfo**をこのデータ型がサポートされているかどうかを判断します。
