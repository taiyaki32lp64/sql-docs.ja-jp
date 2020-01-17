---
title: 高速解析 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- fast parse [Integration Services]
ms.assetid: 6688707d-3c5b-404e-aa2f-e13092ac8d95
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b13ddc498962ca23e6bc1f5e7a10d88af47ff7d6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058869"
---
# <a name="fast-parse"></a>高速解析
  高速解析は、データを解析するための高速で単純なルーチンのセットです。 これらのルーチンはロケール依存型ではなく、日付、時刻、および整数形式のサブセットのみをサポートします。  
  
## <a name="requirements-and-limitations"></a>要件と制限  
 パッケージに高速解析を実装することで、ロケール固有の形式と頻繁に使用される ISO 8601 の基本形式や拡張形式では、日付、時刻、および数値データを解釈できなくなりますが、パッケージのパフォーマンスは向上します。 たとえば、高速解析では、YYYYMMDD や YYYY-MM-DD など、通常使用される日付形式表記のみがサポートされます。ロケール固有の解析の実行や、通貨データ内の特殊文字の認識は行いません。また、整数の 16 進数表記と科学的表記は変換できません。  
  
 フラット ファイル ソースまたはデータ変換の変換を使用する場合のみ、高速解析を使用できます。 著しくパフォーマンスが向上する可能性があるので、可能な限りこれらのデータ フロー コンポーネントで高速解析を使用するよう検討してください。  
  
 パッケージ内のデータ フローでロケール依存型の解析が必要な場合は、高速解析ではなく、標準的な解析を使用することをお勧めします。 たとえば、高速解析では、コンマなど 10 進数の記号が含まれるロケール依存型のデータ、年 - 月 - 日形式以外の日付形式、および通貨記号は認識されません。  
  
 高速解析では、世紀、年、月など、1 つ以上の日付の部分を暗黙で表記する切り捨て表記は認識されません。 たとえば、高速解析は、世紀を暗黙で示して年月を表記する ' **-YYMM**' 形式と、年を暗黙で示して月を表記する ' **--MM**' 形式の、どちらも認識しません。 ただし、有効桁数を減らした表記の一部は認識されます。 たとえば、高速解析では、時間と分のみを示す 'hhmm;' 形式と、年のみを示す '**YYYY**' 形式は認識されます。  
  
 高速解析は、列レベルで指定されます。 フラット ファイル ソースおよびデータ変換の変換では、出力列で高速解析を指定できます。 入力と出力には、ロケール依存型の列およびロケール非依存型の列の、両方を含めることができます。  
  
 高速解析がサポートするデータ形式の詳細については、「 [Numeric Data Formats](../../2014/integration-services/numeric-data-formats.md) 」および「 [Date and Time Formats](../../2014/integration-services/date-and-time-formats.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 [高速解析を設定する](../../2014/integration-services/set-fast-parse.md)  
  
  
