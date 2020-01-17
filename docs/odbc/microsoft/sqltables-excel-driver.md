---
title: SQLTables (Excel ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLTables
- SQLTables function [ODBC], Excel Driver
ms.assetid: 9410b686-4b5b-4b51-b5ef-f9d2e7a48faa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 89157178aa9c134bdb1b9518343007adb1e1e05f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132423"
---
# <a name="sqltables-excel-driver"></a>SQLTables (Excel ドライバー)
> [!NOTE]  
>  このトピックでは、Excel ドライバー固有の情報を提供します。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
|引数|コメント|  
|--------------|--------------|  
|*szTableOwner*|唯一の有効な引数*szTableOwner*ドライバーのサポートの所有者名が NULL です。 *SzTableOwner*を NULL に設定すると、すべてのテーブルが返されます。 TABLE_OWNER 列で NULL が返されます。|  
|*szTableQualifier*|Microsoft Excel 3.0 または 4.0 のドライバーを使用する場合を呼び出す場合**SQLTables**に値を持つ*szTableQualifier*既存のテーブルの名前でない、ドライバーはその名前を持つテーブルを作成します。<br /><br /> TABLE_QUALIFIER 列で、 **SQLTables**ディレクトリへのパスを返します。|  
|*SzTableType*|Microsoft Excel 3.0 または 4.0 では、"TABLE"はサポートされている唯一のテーブルの種類です。<br /><br /> 以降のバージョンの Microsoft Excel ファイルでは、シート名 (末尾に「$」でテーブル) の「システム テーブル」が返されます、ワークシート内のテーブルの"TABLE"が返されます。|
