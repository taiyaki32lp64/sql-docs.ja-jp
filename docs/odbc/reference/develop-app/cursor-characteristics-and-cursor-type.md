---
title: カーソルの特性とカーソルの種類 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: 6f67edd2-ae71-4ca0-9b2d-abf4c20dc17b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e8803e7827102f564be63454b0387df938064d84
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002056"
---
# <a name="cursor-characteristics-and-cursor-type"></a>カーソルの特定とカーソルの種類
アプリケーションでは、(順方向専用、静的、キーセット ドリブンまたは動的) カーソルの種類を指定する代わりに、カーソルの特性を指定できます。 これを行うには、アプリケーションを選択します (SQL_ATTR_CURSOR_SCROLLABLE ステートメント属性を設定) して、カーソルのスクロール機能と感度 (SQL_ATTR_CURSOR_SENSITIVITY ステートメント属性を設定する) をステートメントでカーソルを開く前に処理します。 ドライバーは、アプリケーションが要求した特性を最も効率的に提供する、カーソルの種類から選択します。  
  
 たびに、アプリケーションは、ステートメント属性 SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_SCROLLABLE、SQL_ATTR_CURSOR_SENSITIVITY、SQL_ATTR_CURSOR_TYPE またはのいずれかを設定、ドライバーには、この一連の他のステートメント属性を必要な変更をします。4 つの属性の値が変わらないようにします。 その結果、アプリケーションでは、カーソルの特性を指定する場合、ドライバー属性を変更できるこの暗黙の型の選択に基づくカーソルの種類を示すアプリケーションでは、型を指定する場合、ドライバーは、選択した型の特性を持つ一貫性があるその他の属性のいずれかを変更できます。 これらのステートメント属性の詳細については、次を参照してください。、 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)関数の説明。  
  
 カーソルの種類とカーソルの特性の両方を指定するステートメント属性を設定するアプリケーションでは、そのドライバー、アプリケーションの要件を満たすに使用できる最も効率的な方法ではないカーソルを取得するリスクを実行します。  
  
 ステートメント属性の暗黙的な設定は、ドライバー定義する点を除いて、これらの規則に従う必要があります。  
  
-   順方向専用カーソルはスクロール可能です。SQL_ATTR_CURSOR_SCROLLABLE での定義を参照してください。 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)します。  
  
-   Insensitive カーソルは更新できません (および、同時実行は読み取り専用のため)。ISO SQL 標準で insensitive のカーソルの定義に基づきます。  
  
 そのため、ステートメント属性の暗黙的な設定は、次の表で説明されている場合に発生します。  
  
|アプリケーションでは、属性を設定するには|その他の属性が暗黙的に設定します。|  
|-----------------------------------|-------------------------------------|  
|SQL_ATTR_CONCURRENCY を SQL_CONCUR_READ_ONLY|SQL_ATTR_CURSOR_SENSITIVITY SQL_INSENSITIVE にします。|  
|SQL_CONCUR_LOCK や SQL_CONCUR_ROWVER、SQL_CONCUR_VALUES SQL_ATTR_CONCURRENCY|SQL_ATTR_CURSOR_SENSITIVITY SQL_UNSPECIFIED または SQL_SENSITIVE、ドライバーで定義されています。 これは、ことができますに設定しないで SQL_INSENSITIVE、insensitive カーソルは常に読み取り専用であるためです。|  
|SQL_ATTR_CURSOR_SCROLLABLE が SQL_NONSCROLLABLE に|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY に|  
|SQL_ATTR_CURSOR_SCROLLABLE が SQL_SCROLLABLE に|SQL_CURSOR_STATIC、SQL_CURSOR_KEYSET_DRIVEN、または、ドライバーで指定したとおり、SQL_CURSOR_DYNAMIC SQL_ATTR_CURSOR_TYPE します。 SQL_CURSOR_FORWARD_ONLY には設定されません。|  
|SQL_ATTR_CURSOR_SENSITIVITY が SQL_INSENSITIVE に|SQL_ATTR_CONCURRENCY を SQL_CONCUR_READ_ONLY します。<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC にします。|  
|SQL_ATTR_CURSOR_SENSITIVITY が SQL_SENSITIVE に|SQL_ATTR_CONCURRENCY SQL_CONCUR_LOCK や SQL_CONCUR_ROWVER、SQL_CONCUR_VALUES、ドライバーで指定したとおりにします。 SQL_CONCUR_READ_ONLY には設定されません。<br /><br /> SQL_CURSOR_FORWARD_ONLY、SQL_CURSOR_STATIC、SQL_CURSOR_KEYSET_DRIVEN、または、ドライバーで指定したとおり、SQL_CURSOR_DYNAMIC SQL_ATTR_CURSOR_TYPE します。|  
|SQL_ATTR_CURSOR_SENSITIVITY が SQL_UNSPECIFIED に|SQL_ATTR_CONCURRENCY を SQL_CONCUR_READ_ONLY、SQL_CONCUR_LOCK、SQL_CONCUR_ROWVER、SQL_CONCUR_VALUES、ドライバーによって指定されたまたはします。<br /><br /> SQL_CURSOR_FORWARD_ONLY、SQL_CURSOR_STATIC、SQL_CURSOR_KEYSET_DRIVEN、または、ドライバーで指定したとおり、SQL_CURSOR_DYNAMIC SQL_ATTR_CURSOR_TYPE します。|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_DYNAMIC に|SQL_SCROLLABLE に SQL_ATTR_SCROLLABLE します。<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY SQL_SENSITIVE にします。 (ただし SQL_ATTR_CONCURRENCY を SQL_CONCUR_READ_ONLY と等しくない場合にのみです。 更新可能な動的カーソルは常に独自のトランザクションで加えられた変更に敏感です。)|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY に|SQL_ATTR_CURSOR_SCROLLABLE を SQL_NONSCROLLABLE します。|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_KEYSET_DRIVEN に|SQL_SCROLLABLE に SQL_ATTR_SCROLLABLE します。<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED または SQL_SENSITIVE (ドライバーの定義済み条件に従って、SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY でない場合)。|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC に|SQL_SCROLLABLE に SQL_ATTR_SCROLLABLE します。<br /><br /> SQL_ATTR_SENSITIVITY SQL_INSENSITIVE (SQL_ATTR_CONCURRENCY が SQL_CONCUR_READ_ONLY の場合) にします。<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED または SQL_SENSITIVE (SQL_ATTR_CONCURRENCY が SQL_CONCUR_READ_ONLY でない場合)。|
