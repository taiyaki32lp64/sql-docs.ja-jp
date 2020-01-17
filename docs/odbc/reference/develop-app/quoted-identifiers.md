---
title: 識別子を引用符で囲まれた |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], quoted identifiers
- quoted identifiers [ODBC]
ms.assetid: 729ba55f-743b-4a04-8c39-ac0a9914211d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3bc4d8378c243edf9f01cca58ff8be11d675711a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079000"
---
# <a name="quoted-identifiers"></a>引用符で囲まれた識別子
SQL ステートメント内で特殊文字または一致するキーワードを含む識別子を囲む必要が*識別子引用符文字*; このような文字で囲まれた識別子と呼ばれる*の識別子を引用符で囲まれた*(とも呼ばれます*区切られた識別子*sql-92 で)。 次に、Accounts Payable 識別子が引用符で囲まれたなど**選択**ステートメント。  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 識別子を囲むため理由は、ステートメントを解析します。 たとえば、Accounts Payable がない引用符で囲まれた、前のステートメントで場合、パーサーはアカウントと Payable、2 つのテーブルがあったとし、コンマで区切られたことが構文エラーを返します。 引用符文字の識別子はドライバー固有であり SQL_IDENTIFIER_QUOTE_CHAR オプションで取得**SQLGetInfo**します。 SQL_SPECIAL_CHARACTERS と SQL_KEYWORDS オプションでキーワードと特殊文字の一覧が取得されます**SQLGetInfo**します。  
  
 安全に相互運用可能なアプリケーションは多くの場合、Oracle では、ROWID 列などの擬似列を除くすべての識別子を引用します。 **SQLSpecialColumns**擬似列の一覧を返します。 また、オブジェクト名に特殊文字を表示する場所にアプリケーション固有の制限がある場合はこれらの位置で特殊文字を使用しないように相互運用可能なアプリケーションのことをお勧めします。
