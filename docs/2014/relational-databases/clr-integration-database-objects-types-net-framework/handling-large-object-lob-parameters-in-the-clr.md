---
title: CLR でラージ オブジェクト (LOB) のパラメーターの処理 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- large data, CLR integration
- LOB data [SQL Server], CLR integration
- SqlBytes data type
- SqlChars data type
ms.assetid: d07956f6-9543-4476-9426-536f95991150
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 09797eac229a4b3b92f94a60b6e1c06c9ec12f08
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62919498"
---
# <a name="handling-large-object-lob-parameters-in-the-clr"></a>CLR での LOB (ラージ オブジェクト) パラメーターの処理
  `SqlBytes` と `SqlChars` は、それぞれ、LOB (ラージ オブジェクト) バイナリ型 (`varbinary(max)`) パラメーターと LOB 文字型 (`nvarchar(max)`) パラメーターを渡すために使用します。 これらの型を使用すると、マネージド領域に LOB 値全体をコピーするのではなく、データベースから CLR (共通言語ランタイム) ルーチンに LOB 値をストリーミングできます。 `SqlBinary` と `SqlString` は、小さなバイナリ値や文字列値のみに使用する必要があります。  
  
## <a name="see-also"></a>関連項目  
 [.NET Framework での SQL Server データ型](sql-server-data-types-in-the-net-framework.md)  
  
  
