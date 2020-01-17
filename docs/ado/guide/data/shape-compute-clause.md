---
title: COMPUTE 句を図形 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- compute clause [ADO]
- data shaping [ADO], COMPUTE clause
ms.assetid: 3fdfead2-b5ab-4163-9b1d-3d2143a5db8c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa6862808643f3d687fa406cb3fc2aa23c9b7d7b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924145"
---
# <a name="shape-compute-clause"></a>Shape COMPUTE 句
図形の COMPUTE 句には、親が生成されます**レコード セット**の子への参照で構成されている列を持つ**レコード セット**は省略可能内容は章では、新しい、または計算列、列、または子の集計関数の実行結果**レコード セット**または以前に整形**レコード セット**; と任意の列の子から**レコード セット**記載されています句で省略可能。  
  
## <a name="syntax"></a>構文  
  
```  
SHAPE child-command [AS] child-alias  
   COMPUTE child-alias [[AS] name], [appended-column-list]  
   [BY grp-field-list]  
```  
  
## <a name="description"></a>説明  
 この句の部分は次のとおりです。  
  
 *child-command*  
 次のいずれかで構成されます。  
  
-   中かっこ内でクエリ コマンド ("{}") を返す子**Recordset**オブジェクト。 基になるデータ プロバイダーに、コマンドが発行され、その構文は、そのプロバイダーの要件によって異なります。 通常これは、SQL 言語では、ADO では、特定のクエリ言語は必要ありません。  
  
-   既存の型の名前**Recordset**します。  
  
-   別の図形コマンド。  
  
-   テーブル キーワードは、後に、データ プロバイダーでのテーブルの名前。  
  
 *child-alias*  
 別名を参照するため、 **Recordset**によって返される、*子コマンド。* *子エイリアス*COMPUTE 句で列の一覧で、必要であり、親と子の間のリレーションシップを定義します。 **Recordset**オブジェクト。  
  
 *appended-column-list*  
 一覧の各要素が生成された親内の列を定義します。 各要素には、チャプター列、新しい列、計算列、または子の集計関数の結果の値が含まれます。 **Recordset**します。  
  
 *grp-field-list*  
 親と子列の一覧**Recordset**子の行をグループ化する方法を指定するオブジェクト。  
  
 各列に対して、 *grp フィールドのリスト*子と親に対応する列がある**レコード セット**オブジェクト。 親の行ごとに**レコード セット**、 *grp*列は、一意の値と子要素がある**レコード セット**親によって参照されている子のみの行で構成されます行を持つ*grp*列は、親の行として同じ値を持ちます。  
  
 BY 句が含まれている場合は、子**Recordset**の行に、COMPUTE 句内の列に基づいてグループが化されます。 親**レコード セット**子内の行のグループごとに 1 つの行を含む**レコード セット**します。  
  
 BY 句を省略すると、子全体**レコード セット**は 1 つのグループとその親として扱われます**Recordset**は正確に 1 つの行が含まれます。 その行は、子全体を参照**Recordset**します。 BY 句を省略すると、子全体を「総計」の集計を計算できます**Recordset**します。  
  
 以下に例を示します。  
  
```  
SHAPE {select * from Orders} AS orders             COMPUTE orders, SUM(orders.OrderAmount) as TotalSales         
```  
  
 どの方法に関係なく、親**レコード セット**の形式が子への関連付けに使用するチャプター列が含まれます (COMPUTE を使用または追加を使用して)、**レコード セット**します。 場合は、親**Recordset**子の行を集計 (SUM、MIN、MAX、およびなど) を含む列を含めることもできます。 親と子の両方**レコード セット**内の行の式を含む列を含めることができます、**レコード セット**、および新しいと、最初にある列を空にします。  
  
## <a name="operation"></a>操作  
 *子コマンド*に対して発行される、プロバイダーは、子を返します**Recordset**します。  
  
 COMPUTE 句は、親の列を指定します**レコード セット**、子への参照である**Recordset**、1 つまたは複数の集計、計算式、または新しい列。 この列が親にも追加 BY 句がある場合**Recordset**します。 BY 句を指定する方法、子の行**レコード セット**グループ化されます。  
  
 たとえば、状態、City、および作成のフィールドで構成されるテーブル、人口統計、という名前があるとします。 (表内の人口統計は、例としてのみ提供されます。)  
  
|状態|City|[母集団]|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|OR|Medford|200,000|  
|OR|Portland|400,000|  
|CA|Los Angeles|800,000|  
|CA|サンディエゴ|600,000|  
|WA|Tacoma|500,000|  
|OR|Corvallis|300,000|  
  
 ここで、この図形のコマンドを発行します。  
  
```  
rst.Open  "SHAPE {select * from demographics} AS rs "  & _  
          "COMPUTE rs, SUM(rs.population) BY state", _  
           objConnection  
```  
  
 このコマンドは、形状開きます**レコード セット**2 つのレベル。 親のレベルは、生成された**レコード セット**集計列を持つ (`SUM(rs.population)`)、子を参照する列**レコード セット**(`rs`)、および子をグループ化するための列**Recordset** (`state`)。 子レベルは、 **Recordset**クエリ コマンドによって返される (`select * from demographics`)。  
  
 子**Recordset**状態によってグループ化されたが、任意の順序でそれ以外の場合に、詳細行になります。 つまり、グループはアルファベットまたは数字の順序ではできません。 場合は、親**レコード セット**指定の順序を使用することができます、**レコード セットの並べ替え**親を順序付ける方法**Recordset**します。  
  
 開かれている親を移動できるようになりました**Recordset**子詳細へのアクセスと**レコード セット**オブジェクト。 詳細については、次を参照してください。[階層レコード セットの行にアクセスする](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)します。  
  
## <a name="resultant-parent-and-child-detail-recordsets"></a>結果の親と子詳細レコード セット  
  
### <a name="parent"></a>Parent  
  
|SUM (rs。カタログ作成)|rs|状態|  
|---------------------------|--------|-----------|  
|1,300,000|Child1 への参照|CA|  
|1,200,000|Child2 への参照|WA|  
|1,100,000|子 3 への参照|OR|  
  
## <a name="child1"></a>Child1  
  
|状態|City|[母集団]|  
|-----------|----------|----------------|  
|CA|Los Angeles|800,000|  
|CA|サンディエゴ|600,000|  
  
## <a name="child2"></a>Child2  
  
|状態|City|[母集団]|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|WA|Tacoma|500,000|  
  
## <a name="child3"></a>子 3  
  
|状態|City|[母集団]|  
|-----------|----------|----------------|  
|OR|Medford|200,000|  
|OR|Portland|400,000|  
|OR|Corvallis|300,000|  
  
## <a name="see-also"></a>参照  
 [階層レコード セット内の行へのアクセス](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [データ シェイプの概要](../../../ado/guide/data/data-shaping-overview.md)   
 [Field オブジェクト](../../../ado/reference/ado-api/field-object.md)   
 [Shape の正式文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [RecordSet オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [データ シェイプに必要なプロバイダー](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Shape の APPEND 句](../../../ado/guide/data/shape-append-clause.md)   
 [一般的な shape コマンド](../../../ado/guide/data/shape-commands-in-general.md)   
 [Value プロパティ (ADO)](../../../ado/reference/ado-api/value-property-ado.md)   
 [Visual Basic for Applications の関数](../../../ado/guide/data/visual-basic-for-applications-functions.md)
