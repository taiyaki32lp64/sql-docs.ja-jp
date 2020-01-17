---
title: ODBC のパラメーターのバインド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- binding parameters [ODBC]
ms.assetid: 7538a82b-b08b-4c8f-9809-e4ccea16db11
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1bc40d4800e7cd013b7ac908400c0492286314e3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107634"
---
# <a name="binding-parameters-odbc"></a>パラメーターのバインド (ODBC)
SQL ステートメント内の各パラメーター、関連付けられている必要がありますまたは*バインド、* ステートメントが実行される前に、アプリケーション内の変数にします。 アプリケーションでは、パラメーターに変数をバインドした場合は、ドライバーにその変数のアドレス、C データ型では、- がについて説明します。 パラメーター自体で SQL データ型、有効桁数、およびなども説明します。 ドライバーでは、そのステートメントを保持し、ステートメントが実行されたときに、変数から値を取得する情報を使用して構造体のこの情報を格納します。  
  
 パラメーターのバインドまたはステートメントを実行する前にいつでも再バインドできます。 パラメーターは、ステートメントの実行後に再バインドは、もう一度、ステートメントが実行されるまで、バインドは適用されません。 パラメーターを別の変数にバインドするには、アプリケーション単に再バインド; 新しい変数とパラメーター以前のバインドは自動的に解放されます。  
  
 まで呼び出すことによってすべてのパラメーターがバインドされていない、パラメーターに、別の変数がバインドされるまで、変数のパラメーターにバインドされたまま**SQLFreeStmt** SQL_RESET_PARAMS オプション、またはステートメントが解放されるまでです。 このため、アプリケーションがバインドされた後変数がまで解放されないことを確認してあります。 詳細については、次を参照してください。[割り当ておよび解放バッファー](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)します。  
  
 パラメーターのバインドは、ステートメント用のドライバーによって保持される構造体に格納されている情報だけであるために、任意の順序で設定できます。 実行される SQL ステートメントから独立していることもできます。 たとえば、アプリケーションは、3 つのパラメーターをバインドし、次の SQL ステートメントを実行します。  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 次に、アプリケーションがすぐに SQL ステートメントを実行する場合  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 次のように同じステートメント ハンドルのパラメーター バインド、**挿入**のため、これらのステートメントの構造体に格納されているバインド ステートメントを使用します。 ほとんどの場合、これは不適切なプログラミング手法と、避ける必要があります。 代わりに、アプリケーションを呼び出す必要があります**SQLFreeStmt**古いすべてのパラメーターのバインドを解除し、新しいものをバインドする SQL_RESET_PARAMS オプションを使用します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [バインディング パラメーター マーカー](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [名前によるパラメーターのバインド (名前付きパラメーター)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [パラメーター バインディングのオフセット](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [パラメーターの記述](../../../odbc/reference/develop-app/describing-parameters.md)
