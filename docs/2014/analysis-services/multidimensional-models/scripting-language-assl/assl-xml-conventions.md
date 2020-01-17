---
title: ASSL XML 規則 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- whitespace [Analysis Services Scripting Language]
- trailing whitespace
- XSD data types [Analysis Services Scripting Language]
- inheritance [Analysis Services Scripting Language]
- cardinality [Analysis Services Scripting Language]
- white space [Analysis Services Scripting Language]
- ASSL, XML conventions
- defaults [Analysis Services Scripting Language]
- leading whitespace
- Analysis Services Scripting Language, XML conventions
- XML [Analysis Services Scripting Language]
- hierarchies [Analysis Services Scripting Language]
- inherited defaults [Analysis Services Scripting Language]
ms.assetid: bce4edad-4420-41ce-9672-8c00c5c0dec6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 41e0a3fcf4348efcb2108a1205c1d2d8eabfb85c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62736395"
---
# <a name="assl-xml-conventions"></a>ASSL XML 規則
  Analysis Services スクリプト言語 (ASSL) はオブジェクトの階層を要素の型のセットとして表し、それぞれが含むことのできる子要素を定義します。  
  
 ASSL では、次の XML 規則を使用してオブジェクトの階層を表します。  
  
-   すべてのオブジェクトおよびプロパティは、'xml:lang' などの標準の XML 属性を除き、要素として表されます。  
  
-   要素名と列挙値の両方が pascal 形式の Microsoft .NET Framework 名前付け規則に従っていないアンダー スコアで大文字小文字の区別します。  
  
-   すべての値の大文字と小文字の区別が保持されます。 列挙の値も大文字と小文字が区別されます。  
  
 これらの規則の他にも、Analysis Services はカーディナリティ、継承、空白文字、データ型、既定値などに関する一定の規則に従います。  
  
## <a name="cardinality"></a>Cardinality  
 要素に 1 より大きいカーディナリティがある場合は、この要素をカプセル化する XML 要素のコレクションがあります。 コレクションの名前は、コレクションに含まれている要素の複数形を使用します。 たとえば、次の XML フラグメントは `Dimensions` 要素内の `Database` コレクションを表します。  
  
 `<Database>`  
  
 `...`  
  
 `<Dimensions>`  
  
 `<Dimension>`  
  
 `...`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `...`  
  
 `</Dimension>`  
  
 `</Dimensions>`  
  
 `</Database>`  
  
 ``  
  
 要素の順序は重要ではありません。  
  
## <a name="inheritance"></a>継承  
 継承は、重複しているが大幅に異なるプロパティのセットを持つ、明確に区別されるオブジェクトがある場合に使用されます。 このように重複しているが明確に区別されるオブジェクトの例として、仮想キューブ、リンク キューブ、および標準キューブがあります。 重複しているが明確に区別されるオブジェクトの場合、Analysis Services では XML インスタンス名前空間の標準的な `type` 属性を使用して、継承を示します。 たとえば、次の XML フラグメントは、`type` 要素が標準キューブまたは仮想キューブのどちらから継承するかを `Cube` 属性が識別する方法を示しています。  
  
 `<Cubes>`  
  
 `<Cube xsi:type="RegularCube">`  
  
 `<Name>Sales</Name>`  
  
 `...`  
  
 `</Cube>`  
  
 `<Cube xsi:type="VirtualCube">`  
  
 `<Name>SalesAndInventory</Name>`  
  
 `...`  
  
 `</Cube>`  
  
 `</Cubes>`  
  
 ``  
  
 継承は通常、複数の型に同じ名前のプロパティがある場合は使用されません。 たとえば、`Name` プロパティと `ID` プロパティは多くの要素に含まれますが、抽象型には昇格されていません。  
  
## <a name="whitespace"></a>空白文字  
 要素値内の空白文字が保持されます。 ただし、先頭と末尾の空白文字は常に切り捨てられます。 たとえば、次の要素には同じテキストがありますが、そのテキスト内の空白文字の数が異なるので、別の値として扱われます。  
  
 `<Description>My text<Description>`  
  
 `<Description>My  text<Description>`  
  
 ``  
  
 しかし、次の要素は先頭と末尾の空白文字のみが異なるので、同じ値として扱われます。  
  
 `<Description>My text<Description>`  
  
 `<Description>  My text  <Description>`  
  
 ``  
  
## <a name="data-types"></a>データ型  
 Analysis Services では、次のように XML スキーマ定義言語 (XSD) の標準的なデータ型を使用します。  
  
 `Int`  
 -231 ~ 231-1 の範囲の整数値。  
  
 `Long`  
 -263 ~ 263-1 の範囲の整数値。  
  
 `String`  
 次のグローバル ルールに従う文字列値。  
  
-   制御文字は除去されます。  
  
-   先頭と末尾の空白文字は切り捨てられます。  
  
-   内部の空白文字は保持されます。  
  
 `Name` プロパティと `ID` プロパティには、文字列要素の有効な文字に特別な制限があります。 詳細については`Name`と`ID`規則を参照してください[ASSL オブジェクトとオブジェクトの特性](assl-objects-and-object-characteristics.md)します。  
  
 `DateTime`  
 A`DateTime`から .NET Framework の構造体。 `DateTime` の値を NULL にすることはできません。 `DataTime` データ型がサポートしている下限の日付は 1601 年 1 月 1 日です。プログラマはこの日付を `DateTime.MinValue` として使用できます。 サポートされている下限の日付は、`DateTime` の値が欠落していることを示します。  
  
 `Boolean`  
 {true, false} や {0, 1} のように値が 2 つだけの列挙。  
  
## <a name="default-values"></a>既定値  
 Analysis Services で使用される既定値を次の表に示します。  
  
|XML データ型|既定値|  
|-------------------|-------------------|  
|`Boolean`|False|  
|`String`|"" (空の文字列)|  
|`Integer` または `Long`|0 (ゼロ)|  
|`Timestamp`|12時 00分: 00 AM、1/1/0001 (に対応する、.NET フレームワーク`System.DateTime`0 タイマー刻みで)|  
  
 要素が存在するが空の場合は、既定値ではなく NULL 文字列の値を含んでいるとして解釈されます。  
  
### <a name="inherited-defaults"></a>継承された既定値  
 オブジェクトに指定されているプロパティには、子または子孫オブジェクトの同じプロパティに既定値を提供するものがあります。 たとえば、`Cube.StorageMode` は `Partition.StorageMode` に既定値を提供します。 Analysis Services で継承された既定値に適用されるルールは、次のとおりです。  
  
-   子オブジェクトのプロパティが XML で NULL の場合、その値の既定値は継承された値になります。 ただし、サーバーから値をクエリする場合は、XML 要素の NULL 値が返されます。  
  
-   子オブジェクトのプロパティが子オブジェクトで直接設定されたか、または継承されたかをプログラムで判断することはできません。  
  
 一部の要素には、要素が欠落しているときに適用される既定値が定義されています。 たとえば、次の XML フラグメントで、一方の `Dimension` 要素には `Dimension` 要素が含まれ、もう一方の `Visible` 要素には含まれませんが、これらの `Dimension` 要素は同じものです。  
  
 `<Dimension>`  
  
 `<Name>Product</Name>`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `<Name>Product</ Name>`  
  
 `<Visible>true</Visible>`  
  
 `</Dimension>`  
  
 継承された既定値の詳細については、次を参照してください。 [ASSL オブジェクトとオブジェクトの特性](assl-objects-and-object-characteristics.md)します。  
  
  
