---
title: 正規の形式とパターン制限 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- pattern restrictions
- canonical forms
ms.assetid: 088314ec-7d0b-4a05-8a33-f35da5bfe59c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eec8bda347b52835e84f4c9a505d9ad82cdf1a40
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211557"
---
# <a name="canonical-forms-and-pattern-restrictions"></a>正規の形式とパターン制限
  XSD パターン ファセットを使用すると、単純型の字句空間を制限できます。 複数の字句表現が可能であるような型にパターン制限を適用すると、一部の値が原因で検証時に予想外の動作が発生することがあります。  
  
 このような動作は、その値の字句表現がデータベースに格納されていないために発生します。 したがって、このような値は、出力としてシリアル化される際に、それぞれの正規表現に変換されます。 ドキュメントに含まれる値の正規の形式が型のパターン制限に準拠していない場合に、ユーザーがそのドキュメントの再挿入を試みると、そのドキュメントは拒否されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではこれを回避するために、再挿入できない値を含む XML ドキュメントはすべて、正規の形式がパターン制限に違反しているという理由で拒否します。 たとえば、値 "33.000" は、"33 **.0+" というパターン制限が指定されている** xs:decimal\\からの派生型に対して有効であると判断されません。 "33.000" はこのパターンに準拠していますが、正規の形式である "33" がパターンに違反しているためです。  
  
 したがって、プリミティブ型の `boolean`、`decimal`、`float`、`double`、`dateTime`、`time`、`date`、`hexBinary`、および `base64Binary` から派生した型にパターン ファセットを適用する場合は注意が必要です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から警告が発行されます。  
  
 浮動小数点値の不正確なシリアル化にも同様の問題があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で使用されている浮動小数点のシリアル化アルゴリズムにより、近い値が同じ正規表現になることがあり得ます。 ただし、浮動小数点値がシリアル化され、再挿入される際に、その値がわずかに変化することがあります。 その結果、再挿入時にその型の **enumeration**、 **minInclusive**、 **minExclusive**、 **maxInclusive**、または **maxExclusive**の各ファセットに違反する値になることがまれにあります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではこれを回避するために、シリアル化や再挿入を行えない `xs:float` または `xs:double` から派生した値を拒否します。  
  
## <a name="see-also"></a>関連項目  
 [サーバー上の XML スキーマ コレクションの要件と制限](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
