---
title: スカラー関数エスケープ シーケンス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function
- scalar functions [ODBC], escape sequences
- ODBC escape sequences [ODBC], scalar function
ms.assetid: aaf5d516-e090-445f-8839-9e39581c69c7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 36e108fcc61b2390d5fd72ac4ad322778ccfb4b2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057067"
---
# <a name="scalar-function-escape-sequence"></a>スカラー関数のエスケープ シーケンス
ODBC スカラー関数のエスケープ シーケンスを使用します。 このエスケープ シーケンスの構文は次のとおりです。  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>Remarks  
 BNF 表記では、構文がとおりです。  
  
 *ODBC スカラー関数エスケープ*:: =  
  
 *ODBC のイニシエーター esc* fn*スカラー関数 ODBC esc 終端*  
  
 *スカラー関数*:: =*関数名*(*引数リスト*)  
  
 (、非終端要素の定義*関数名*と*関数名*(*引数リスト*) は、スカラー関数の一覧から派生[付録 e:スカラー関数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md))。  
  
 *ODBC のイニシエーター esc* :: = {  
  
 *Esc 終端の ODBC* :: =}  
  
 データ ソースには、プロシージャがサポートされ、ドライバーは ODBC プロシージャの呼び出し構文をサポートしているかどうかを調べるにアプリケーションを呼び出すことができます**SQLGetInfo**します。 詳細については、次を参照してください[付録 e:。スカラー関数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)します。
