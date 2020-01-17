---
title: 数値リテラルの構文 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC literals [ODBC], numeric
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: fb17498d-4f1d-4b3d-b33d-1e62c7d3c32d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9daa81e2e0c2e927ee7407d4a00d5d48c333bd54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990723"
---
# <a name="numeric-literal-syntax"></a>数値リテラルの構文
次の構文は、ODBC での数値リテラルに使用されます。  
  
 *数値リテラル*:: =*符号付き数値リテラル&#124;符号なし数値リテラル*  
  
 *signed-numeric-literal* ::= [*sign*] *unsigned-numeric-literal*  
  
 *符号なし数値リテラル*:: =*正確な数値リテラル&#124;おおよその数値リテラル*  
  
 *正確な数値リテラル*:: =*符号なし整数*[*期間*[*符号なし整数*] *&#124;期間符号なし整数*  
  
 *サインオン*:: =*プラス記号&#124;マイナス記号*  
  
 *おおよその数値リテラル*:: =*仮数 E の指数*  
  
 *仮数*:: =*正確な数値リテラル*  
  
 *指数*:: =*符号付き整数*  
  
 *signed-integer* ::= [*sign*] *unsigned-integer*  
  
 *符号なし整数*:: =*桁.*  
  
 *プラス記号*:: = *+*  
  
 *マイナス記号*:: = -  
  
 *数字*:: = 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *期間*:: =。
