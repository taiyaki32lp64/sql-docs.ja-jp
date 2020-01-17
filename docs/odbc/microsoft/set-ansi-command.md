---
title: SET ANSI コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set ANSI command [ODBC]
ms.assetid: cf9a01b2-14bf-458c-a73c-2a58ddef32d8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d32e4dc27568b37f273ef654ebd45d26ca23e555
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997768"
---
# <a name="set-ansi-command"></a>SET ANSI コマンド
異なる長さの文字列の比較が行われる方法を決定する、Visual FoxPro SQL コマンド内の演算子を = です。  
  
## <a name="syntax"></a>構文  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>引数  
 ON  
 ドライバーの既定値 (Visual FoxPro の既定値は OFF)。パッドは、空白で文字列を短くするために必要になりますが長くなるのと同じ文字列の長さ。 2 つの文字列は、それら全体の長さの文字の文字を比較します。 この比較を検討してください。  
  
```  
'Tommy' = 'Tom'  
```  
  
 結果は False (します。F.) 埋められる場合は、'Tom' が 'Tom' と 'Tom' と 'Tommy' 文字列が文字の文字と一致しないために、ANSI の設定がオンの場合。  
  
 このメソッドでは、Visual FoxPro SQL コマンドの比較演算子の使用を = =。  
  
 OFF  
 短い文字列は空白が埋め込まれませんことを指定します。 2 つの文字列の比較より短い文字列の末尾に到達するまでの文字の文字。 この比較を検討してください。  
  
```  
'Tommy' = 'Tom'  
```  
  
 結果は True (します。T.) と ANSI の設定がオフ、ため、比較は、'Tom' の後に停止します。  
  
## <a name="remarks"></a>コメント  
 かどうか 2 つの文字列のうち、小さい方が空白で埋められます SQL 文字列の比較が行われたときに ANSI の設定を決定します。 ANSI の設定も何も起こりませんは演算子 = =使用する場合、演算子、= = 短い文字列が比較のための空白で埋められます常にします。  
  
## <a name="string-order"></a>文字列の順序  
 SQL コマンドの 2 つの文字列比較では左から右の順序は irrelevantswitching = の一方の側から文字列を = = または演算子には、比較の結果に影響しません。  
  
## <a name="see-also"></a>関連項目  
 [SELECT - SQL コマンド](../../odbc/microsoft/select-sql-command.md)   
 [SET EXACT コマンド](../../odbc/microsoft/set-exact-command.md)
