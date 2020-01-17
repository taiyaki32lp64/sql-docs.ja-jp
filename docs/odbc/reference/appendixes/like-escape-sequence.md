---
title: LIKE エスケープ シーケンス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 629ceaf666ae732d0838a216272c308dcb5b5658
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041713"
---
# <a name="like-escape-sequence"></a>LIKE エスケープ シーケンス
ODBC では、LIKE 句のエスケープ シーケンスを使用します。 このエスケープ シーケンスの構文は次のとおりです。  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>Remarks  
 BNF 表記では、構文がとおりです。  
  
 *ODBC のエスケープ似た*:: =  
  
 *ODBC のイニシエーター esc*エスケープ '*エスケープ文字*' *esc 終端の ODBC*  
  
 *エスケープ文字*:: =*文字*  
  
 *ODBC のイニシエーター esc* :: = {  
  
 *Esc 終端の ODBC* :: =}  
  
 ドライバーが LIKE エスケープをサポートしているかを決定するシーケンス、アプリケーションが呼び出すことができます**SQLGetInfo** SQL_LIKE_ESCAPE_CLAUSE 情報の種類にします。
