---
title: テーブル名の制限 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, table name limitations
- table name limitations [ODBC]
- Excel driver [ODBC], table name limitations
ms.assetid: d9843e4b-1d05-4d5a-9dc3-ee9ec59edb97
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 152a0aa1e8d92424b2f60c49f44888de7d3e528c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67939776"
---
# <a name="table-name-limitations"></a>テーブル名の制限
テーブル名は、任意の有効な文字 (スペースなど) を含めることができます。 テーブル名に文字、数字、およびアンダー スコアを除くすべての文字が含まれている場合、バック引用符 (') で囲んで、名前を区切る必要があります。  
  
 Microsoft Excel のドライバーが使用され、データベースの参照では、テーブル名は修飾されていない、ときに、既定のデータベースが暗黙的に指定します。 Microsoft Excel での名前が含まれている場合、"!"文字を自動的に変換されます「$」文字を代わりにします。  
  
 Microsoft Excel のテーブル名を参照する\<ファイル名 > Microsoft Excel 3.0 と 4.0 のファイルはサポートされています。 Microsoft Excel のテーブル名を参照する\<ブック名 > Microsoft Excel 5.0、7.0、または 97 ファイルがサポートされています。  
  
 DBASE ドライバーを使用する場合は、ASCII 値は 127 を超える文字がアンダー スコアに変換されます。  
  
 Microsoft Access ドライバーを使用すると、テーブル名は 64 文字に制限されます。  
  
 DBASE、3.0、4.0、Paradox、またはテキストの Microsoft Excel のドライバーを使用すると、MS-DOS の特別なキーワード CON、AUX、LPT1、LPT2 する必要がありますテーブル名として使用されません。
