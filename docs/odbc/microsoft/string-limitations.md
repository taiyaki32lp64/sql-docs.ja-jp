---
title: 文字列の制限事項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7faab41bd52397ac0d352e04a9ec153571e93f1e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948760"
---
# <a name="string-limitations"></a>文字列の制限事項
SQL ステートメントの文字列の最大長は、65,000 文字です。  
  
 Microsoft Access ドライバーを使用すると、(単一引用符、いない二重引用符) で sql-92 の文字列定数のみがサポートされます。  
  
 パイプ文字 (&#124;) かどうか文字がバック引用符で囲まれているかどうか、文字列では使用できません。  
  
 相互運用性を最大に、アプリケーションが、パラメーターの文字列を渡す必要がありますのではなく渡す文字列を引用符で囲まれました。
