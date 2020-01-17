---
title: データ シェイプの例 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], about data shaping
ms.assetid: 1bfdcad4-52e1-45bc-ad21-783657ef0a44
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a946329ad95a2b226f186e571152268baa5f37c3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925664"
---
# <a name="data-shaping-example"></a>データ シェイプの例
次のデータ シェイプのコマンドは、階層構造を構築する方法を示します**Recordset**から、**顧客**と**注文**Northwind データベースのテーブル。  
  
```  
SHAPE {SELECT CustomerID, ContactName FROM Customers}   
APPEND ({SELECT OrderID, OrderDate, CustomerID FROM Orders} AS chapOrders   
RELATE customerID TO customerID)   
```  
  
 開くこのコマンドを使用するときに、**レコード セット**オブジェクト (ように[のデータ シェイプの例を Visual Basic](../../../ado/guide/data/visual-basic-example-of-data-shaping.md))、チャプターが作成されます (**chapOrders**) の各レコードが返されます**顧客**テーブル。 この章のサブセットから成る、 **Recordset**から返される、**注文**テーブル。 **ChapOrders** 」の章には、特定の顧客の注文に関するすべての要求された情報が含まれています。 この例では 3 つの列の章で構成されます。**OrderID**、 **OrderDate**、および**CustomerID**します。  
  
 型の結果の最初の 2 つのエントリ**レコード セット**次に示します。  
  
|CustomerID|[ContactName]|OrderID|OrderDate|CustomerID|  
|----------------|-----------------|-------------|---------------|----------------|  
|ALFKI|Maria Ander|10643<br /><br /> 10692<br /><br /> 10702<br /><br /> 10835<br /><br /> 10952<br /><br /> 11011|1997-08-25<br /><br /> 1997-10-03<br /><br /> 1997-10-13<br /><br /> 1998-01-15<br /><br /> 1998-03-16<br /><br /> 1998-04-09|ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI|  
|ANATR|Ana Trujillo|10308<br /><br /> 10625<br /><br /> 10759<br /><br /> 10926|1996-09-18<br /><br /> 1997-08-08<br /><br /> 1997-11-28<br /><br /> 1998-03-04|ANATR<br /><br /> ANATR<br /><br /> ANATR<br /><br /> ANATR|  
  
 図形コマンドの追加は、子の作成に使用**Recordset**に関連する親**レコード セット**(で既に説明した図形のキーワードの直後に、プロバイダー固有のコマンドから返される以前 RELATE 句で)。 親と子は、共通の少なくとも 1 つの列をある通常。親の行の列の値では、すべての行、子の列の値の場合と同じです。  
  
 図形のコマンドを使用する 2 つ目の方法があります。 具体的には、親を生成する**レコード セット**子から**レコード セット**。 子のレコード**レコード セット**別にグループ化は、通常 BY 句、および 1 つの行を使用して、親に追加**Recordset**子の結果として得られる各グループ。 BY 句を省略した場合、子**レコード セット**フォームを 1 つのグループとその親は**レコード セット**は正確に 1 つの行が含まれます。 これは子全体を「総計」の集計を計算するために役立ちます**Recordset**します。  
  
 図形のコマンド コンス トラクターでは、形状をプログラムで作成することもできます**Recordset**します。 コンポーネントにアクセスすることができますし、 **Recordset**プログラムまたは適切なビジュアル コントロールを使用します。 その他の ADO コマンド テキストのような図形コマンドが発行されます。 詳細については、次を参照してください。[図形は一般にコマンド](../../../ado/guide/data/shape-commands-in-general.md)します。  
  
 どの方法に関係なく、親**レコード セット**が形式ですが、子への関連付けに使用するチャプター列が格納されます**レコード セット**します。 する場合は、親**Recordset**子行に対する列の集計 (SUM、MIN、MAX、およびなど) が含まれていることもできます。 親と子の両方**レコード セット**内の行の式を含む列を持つことができます、**レコード セット**、および新しいと、最初にある列を空にします。  
  
 このセクションでは、次のトピックを続行します。  
  
-   [Visual Basic のデータ シェイプの例](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)
