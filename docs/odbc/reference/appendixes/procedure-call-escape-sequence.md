---
title: プロシージャ呼び出しのエスケープ シーケンス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], procedure call
- procedure call escape sequence [ODBC]
- ODBC escape sequences [ODBC], procedure call
ms.assetid: 269fbab0-e5f2-4a98-86c0-2d7b647acaae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aa936eb9f8ef3328945d4ece63fb36432a5fd618
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100592"
---
# <a name="procedure-call-escape-sequence"></a>プロシージャ呼び出しのエスケープ シーケンス
ODBC では、プロシージャ呼び出しのエスケープ シーケンスを使用します。 このエスケープ シーケンスの構文は次のとおりです。  
  
 **{** [? =]**呼び出す** *プロシージャ名*[ **(** [*パラメーター*] [、[*パラメーター*]. **)** ] **}**  
  
 BNF 表記では、構文がとおりです。  
  
 *ODBC のエスケープ プロシージャ*:: =  
  
 &#124; です。*ODBC esc イニシエーター* [? =] 呼び出す*プロシージャ esc 終端の ODBC*  
  
 *プロシージャ*:: =*プロシージャ名*&#124; です。*プロシージャ名*(*プロシージャ パラメーターのリストを*)  
  
 *プロシージャ識別子*:: =*ユーザー定義名*  
  
 *プロシージャ名*:: =*プロシージャ識別子*  
  
 &#124; です。*所有者名*.*プロシージャ識別子*  
  
 &#124; です。*カタログ名のカタログの区切り* *プロシージャ識別子*  
  
 &#124; です。*カタログ名のカタログの区切り*[*所有者名*].*プロシージャ識別子*  
  
 (3 番目の構文は、データ ソースは所有者をサポートしていない場合にのみ有効です)。  
  
 *所有者名*:: =*ユーザー定義名*  
  
 *カタログ名*:: =*ユーザー定義名*  
  
 *カタログの区切り*:: = {*実装定義*}  
  
 (カタログの区切り記号がによって返される**SQLGetInfo** SQL_CATALOG_NAME_SEPARATOR 情報オプションを使用します)。  
  
 *プロシージャ パラメーター リスト*:: =*プロシージャ パラメーター*  
  
 &#124; です。*プロシージャ パラメーター*、*プロシージャ パラメーター リスト*  
  
 *プロシージャ パラメーター* :: =*動的パラメーター* &#124; です。*リテラル*&#124; です。*空文字列*  
  
 *空の文字列*:: =  
  
 *ODBC のイニシエーター esc* :: = {  
  
 *Esc 終端の ODBC* :: =}  
  
 (プロシージャ パラメーターが空の文字列の場合は、プロシージャ既定値、パラメーターに対して使用します。)  
  
 データ ソースには、プロシージャがサポートされ、ドライバーは ODBC プロシージャの呼び出し構文をサポートしているかどうかを調べるにアプリケーションを呼び出すことができます**SQLGetInfo** SQL_PROCEDURES 情報の種類にします。
