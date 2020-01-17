---
title: データの解析 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- parsing [Integration Services]
- data parsing [Integration Services]
ms.assetid: 8893ea9d-634c-4309-b52c-6337222dcb39
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fd52b851d4ff35fe1fc9a3a9fed05be0b8098fa9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62900991"
---
# <a name="parsing-data"></a>データの解析
  パッケージ内のデータ フローは、異種データ ストア間でデータの抽出や読み込みを行います。データ ストアでは、標準およびカスタムのさまざまなデータ型を使用します。 データ フローでは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の変換元は、データの抽出、文字列データの解析、および [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型へのデータ変換を行います。 次に続く変換で、データを解析して別のデータ型に変換したり、列のコピーを別のデータ型で作成することもあります。 コンポーネントで使用する式で、引数やオペランドを別のデータ型にキャストする場合もあります。 さらに、データがデータ ストアに読み込まれるとき、変換先でデータを解析して、変換先が使用するデータ型に変換する場合もあります。 詳細については、「 [Integration Services Data Types](integration-services-data-types.md)」を参照してください。  
  
## <a name="types-of-parsing"></a>解析の種類  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、データ変換用に次の 2 種類の解析が用意されています: 高速解析、標準解析。  
  
-   高速解析は、高速で単純な解析ルーチンのセットで、ロケール固有のデータ型の変換はサポートされません。最も頻繁に使用される日付と時間の形式のみがサポートされます。 詳細については、「 [高速解析](../fast-parse.md)」参照してください。  
  
-   標準解析は、解析ルーチンの大規模なセットで、Oleaut32.dll と Ole2dsip.dll で使用できるオートメーション データ型変換 API で提供される、すべてのデータ型の変換がサポートされています。 詳細については、「 [標準解析](../standard-parse.md)」参照してください。  
  
  
