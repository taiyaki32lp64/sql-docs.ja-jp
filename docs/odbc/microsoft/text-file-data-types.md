---
title: テキスト ファイル データの種類 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], data types
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- text file data types [ODBC]
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: e113112e-ae42-469e-8e4b-a365a10d9071
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 829f924d8d4893d45a48c193cd27fdd7ac261e3d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67939713"
---
# <a name="text-file-data-types"></a>テキスト ファイルのデータ型
次の表では、テキスト データ型を ODBC SQL データ型にマップする方法を示します。 すべての ODBC SQL データ型は、テキストの ODBC ドライバーでサポートされていることに注意してください。  
  
|テキストのデータ型|ODBC データ型|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|[FLOAT]|SQL_DOUBLE|  
|INTEGER|SQL_INTEGER|  
|LONGCHAR|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** ODBC データ型を返します。 付録 d のすべての変換、 *ODBC プログラマ リファレンス*の前の表に示す SQL データ型はサポートされます。  
  
 次の表は、テキスト データ型に制限事項を示します。  
  
|データの種類|説明|  
|---------------|-----------------|  
|CHAR|0 の char 型の列を作成または指定されていない長さが実際に 255 ビット列を返します。<br /><br /> 区切られたファイルは、char 型の列が可能性があります。 または先頭と末尾; 区切り記号を二重引用符がない可能性があります。固定長のファイルの区切り記号として二重引用符は使用されません。|  
|DATETIME|MM DD の年 (たとえば、92-01-17)<br /><br /> MMM DD 年 (たとえば、年 1 月の 17-92)<br /><br /> DD-MMM-年 (たとえば、92-17-年 1 月)<br /><br /> -YYYY-MM-DD (たとえば、1992-01-17)<br /><br /> YYYY MMM--DD (たとえば、1992 年 1 月 17 日)<br /><br /> 混在した日付の区切り記号は、テーブル内では許可されません。<br /><br /> テキストの ISAM は、Windows コントロール パネルの 国際対応の設定に応じて、米国またはヨーロッパの形式で、DATETIME フィールドを書式設定します。|  
|[FLOAT]|最大の幅には、符号および小数点が含まれます。 Schema.ini、幅が、次のように表されます。<br /><br /> 14.083 は FLOAT 幅 6 です。<br /><br /> -14.083 は FLOAT 幅 7 です。<br /><br /> +14.083 は FLOAT 幅 7 です。<br /><br /> 14083。 FLOAT 幅 6 は、します。<br /><br /> ODBC には、常に、float 型の列の 8 が返されます。<br /><br /> Float 型の列をたとえば配置科学的表記法でもできます。<br /><br /> -3.04E + 2 は Float 幅 8<br /><br /> 25E4 は Float 幅 4 です。<br /><br /> **注**列に 10 進数と科学的表記法を混在させることはできません。<br /><br /> NULL 値は、固定長ファイルで空白の埋め込み文字列で表されます、区切りファイルの省略しています。<br /><br /> Float データは、先行する空白が埋め込まれていることができます。|  
|INTEGER|整数型の列の有効な値は、-32766 に 32767 です。<br /><br /> Schema.ini、幅が、次のように表されます。<br /><br /> 14083 は幅 5 の整数<br /><br /> 0 は幅 1 の整数<br /><br /> ODBC は、常に整数型の列に 4 を返します。<br /><br /> 最大の幅には、符号が含まれます。 整数型の列の最大の幅は、固定形式のテーブルで使用できる空白により大きくすることは、幅が 11 が。|  
|LONGCHAR|固定長のいずれかで LONGCHAR 列の幅、理論的制限または区切り記号付きのテーブルが 65500 K。 テキストの ISAM は最大で約 32 K の信頼性の高いサポートを提供する可能性が高くなります。|  
  
 データ型の複数の制限事項が記載[データ型の制限事項](../../odbc/microsoft/data-type-limitations.md)します。
