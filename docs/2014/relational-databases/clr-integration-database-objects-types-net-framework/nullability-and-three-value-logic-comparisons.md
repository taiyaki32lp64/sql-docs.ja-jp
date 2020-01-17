---
title: Null 値許容と 3 値論理比較 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- precision [CLR integration]
- overflow detections [CLR integration]
- null values [CLR integration]
- three-value logic comparisons [CLR integration]
- data types [CLR integration]
- SqlBoolean data type
ms.assetid: 13da4c7f-1010-4b2d-a63c-c69b6bfd96f1
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4f1b4823db4ae961024ac2a786c948d8349f31be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62919633"
---
# <a name="nullability-and-three-value-logic-comparisons"></a>NULL 値の許容と 3 値論理比較
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ型に慣れているユーザーであれば、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の `System.Data.SqlTypes` 名前空間でもよく似たセマンティクスや有効桁数を使用していることがわかるはずです。 ただし、いくつか違いもあります。このトピックでは、これらの違いの中から最も重要な点について説明します。  
  
## <a name="null-values"></a>NULL 値  
 CLR (共通言語ランタイム) のネイティブ データ型と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型の主な違いは、CLR データ型では NULL 値が許容されないのに対して、SQL Server データ型では完全な NULL セマンティクスが用意されているという点です。  
  
 比較は NULL 値の影響を受けます。 つまり、2 つの値 x と y を比較するときに、x または y が NULL の場合、一部の論理比較では true または false ではなく UNKNOWN 値に評価されます。  
  
## <a name="sqlboolean-data-type"></a>SqlBoolean データ型  
 `System.Data.SqlTypes` 名前空間では、この 3 つの論理値を表す `SqlBoolean` 型が導入されます。 `SqlTypes` 間の比較では、`SqlBoolean` 型の値が返されます。 UNKNOWN 値は、`SqlBoolean` 型の NULL 値で表現されます。 `IsTrue` 型の値を確認するために、プロパティ `IsFalse`、`IsNull`、および `SqlBoolean` が用意されています。  
  
## <a name="operations-functions-and-null-values"></a>演算、関数、および NULL 値  
 すべての算術演算子 (+、-、 \*、/、%)、ビットごとの演算子 (~、&、|)、ほとんどの関数は、オペランドのいずれかまたはの引数に NULL を返すと`SqlTypes`は NULL。 `IsNull` プロパティで返される値は、常に true または false です。  
  
## <a name="precision"></a>有効桁数  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR の decimal データ型の最大値は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の numeric データ型や decimal データ型の最大値とは異なります。 また、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR の decimal データ型では、最大有効桁数が想定されます。 ただし、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の CLR で、`SqlDecimal` の最大有効桁数、最大小数点以下桁数、およびセマンティクスは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の decimal データ型と同じです。  
  
## <a name="overflow-detection"></a>オーバーフローの検出  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR では、非常に大きな 2 つの数を加算しても例外がスローされないことがあります。 チェック演算子を使用しないと、負の整数に "回り込んだ" 結果が返されます。 `System.Data.SqlTypes` では、すべてのオーバーフロー エラー、アンダーフロー エラー、および 0 除算エラーに対して例外がスローされます。  
  
## <a name="see-also"></a>参照  
 [.NET Framework での SQL Server データ型](sql-server-data-types-in-the-net-framework.md)  
  
  
