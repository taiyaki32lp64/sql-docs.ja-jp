---
title: 列名の制限 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], column names
- ODBC desktop database drivers [ODBC], column names
ms.assetid: 5a339f61-c52f-40ad-8deb-d785f72753d4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14e62555db2e88c6573f3bdca0d4a1a2733d428b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006240"
---
# <a name="column-name-limitations"></a>列名の制限
列名は、任意の有効な文字 (スペースなど) を含めることができます。 列名に文字、数字、およびアンダー スコアを除くすべての文字が含まれている場合、バック引用符 (') で囲んで、名前を区切る必要があります。  
  
 Microsoft Access や Microsoft Excel のドライバーを使用すると、列名は 64 文字に制限されていますし、長い名前は、エラーを生成します。 Paradox ドライバーを使用する場合、最大の列名は、25 文字です。 テキストのドライバーを使用すると最大の列名が、64 文字より長い名前は切り捨てられます。  
  
 DBASE ドライバーを使用する場合は、ASCII 値は 127 を超える文字がアンダー スコアに変換されます。  
  
 Microsoft Excel のドライバーを使用すると、列名が存在する場合は、ときに、最初の行があります。 Microsoft excel を使用する名前、"!"文字は、バック引用符 (') で囲む必要があります。 "!"文字は、ため、「$」文字に変換されます、"!"文字は名前がバック引用符で囲まれている場合にも ODBC 名では無効です。 その他のすべての有効な Microsoft Excel 文字 (パイプ文字を除く (&#124;)) でスペースを含む列名を使用できます。 区切られた識別子は、Microsoft Excel の列名にスペースを含めるために使用する必要があります。 指定されていない列の名前はドライバーによって生成された名前、たとえば、"Col1"最初の列に置き換えられます。  
  
 パイプ文字 (&#124;) か名前がバック引用符で囲まれているかどうか、列名では使用できません。  
  
 テキストのドライバーを使用する場合、ドライバーは、列名が指定されていない場合、既定の名前を提供します。 たとえば、ドライバーは、最初の列 F1、F2、2 番目の列およびなどを呼び出します。
