---
title: データ型の制限事項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], data types
- data types [ODBC], desktop database drivers
- desktop database drivers [ODBC], data types
ms.assetid: 81c4eab7-1f6b-47a0-b940-89d6c6a14dae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 64d16a9181c475427677371d1e6e180570225b7a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096460"
---
# <a name="data-type-limitations"></a>データ型の制限事項
Microsoft ODBC のデスクトップ データベース ドライバーでは、データ型には、以下の制限を強制します。  
  
|データの種類|説明|  
|---------------|-----------------|  
|すべてのデータ型|型変換に失敗すると、影響を受ける列を NULL に設定されている可能性があります。|  
|BINARY|長さ 0 のバイナリ列を作成すると、255 バイトのバイナリ列実際に返されます。|  
|DATE|DATE データ型は、CONVERT 関数によって別のデータ型 (または自体) に変換できません。|  
|10 進数 (正確な数値)|サポートされていません。|  
|浮動小数点データ型|浮動小数点数の小数点以下桁数は、Windows コントロール パネルの国際化のセクションで設定されている数値書式によって制限される可能性があります。|  
|NUMERIC|最大有効桁数と小数点以下桁数が 28 をサポートしています。|  
|TIMESTAMP|TIMESTAMP データ型は、CONVERT 関数によってそれ自体に変換できません。|  
|TINYINT|TINYINT 値は常に符号付きではありません。|  
|長さ 0 の文字列|DBASE、Excel、Paradox、または Textdriver を使用すると、長さ 0 の文字列を列に挿入します。 実際に挿入 NULL 代わりにします。|
