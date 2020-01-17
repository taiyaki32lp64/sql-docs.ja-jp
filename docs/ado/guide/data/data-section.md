---
title: データ セクション |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data section [ADO]
ms.assetid: 43dc42a8-7057-48e6-93d6-880d5c5c51a4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6aebf318652e604c5f5ad4c30ef389fdfd9e78c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925640"
---
# <a name="data-section"></a>データ セクション
データ セクションでは、更新、挿入、または削除保留中のと共に、行セットのデータを定義します。 [データ] セクションでは、0 個以上の行を含めることができます。 行がスキーマによって定義されている 1 つの行セットからのデータのみを含めることができます。 また、前述したように、データを含まない列を省略できます。 データ セクションの属性またはサブ要素が使用され、その構成要素がスキーマのセクションで定義されていない場合は、暗黙的に無視されます。  
  
## <a name="string"></a>String  
 テキスト データでの予約済み XML 文字は、適切な文字エンティティを置き換える必要があります。 たとえば、「Joe のガレージ」会社名では、単一引用符をエンティティによって置き換えする必要があります。 実際の行は、次のようになります。  
  
```  
<z:row CompanyName="Joe's Garage"/>  
```  
  
 次の文字は XML に予約されていると、文字エンティティを置換する必要があります: {"、"、&、\<、>}。  
  
## <a name="binary"></a>Binary  
 バイナリ データは、マップされる bin.hex でエンコードされた (つまり、2 つの文字を 1 バイトのマップ、ニブルあたり 1 つの文字) です。  
  
## <a name="datetime"></a>DateTime  
 バリアントの VT_DATE 形式が XML データのデータ型によって直接サポートされていません。 データと時刻の両方のコンポーネントを含む日付の正しい形式は、yyyy、mm-ddThh:mm:ss します。  
  
 XML で指定された日付形式に関する詳細については、次を参照してください。、 [W3C の XML データの指定](https://go.microsoft.com/fwlink/?LinkId=5692)します。  
  
 XML データの指定が 2 つの同等のデータ型を定義する場合 (たとえば、i4 int = =)、ADO には、フレンドリ名を書き込みますが、読み取りは両方が。  
  
## <a name="managing-pending-changes"></a>保留中の変更を管理します。  
 レコード セットは、イミディ エイトで開くことまたはバッチ更新モード。 クライアント側のカーソルでバッチ更新モードで開くと、UpdateBatch メソッドが呼び出されるまで、レコード セットに加えられたすべての変更が保留状態は。 保留中の変更は、レコード セットを保存するときに保持も。 Urn: スキーマで定義された"update"の要素の使用によって表される XML では、-microsoft-com:rowset します。 さらに、行セットを更新する場合、更新可能なプロパティ、行の定義では true。 たとえば、Shippers テーブルには、保留中の変更が含まれています、行の定義とのことを定義する参照のようになります次です。  
  
```  
<s:ElementType name="row" content="eltOnly" updatable="true">  
  <s:attribute type="ShipperID"/>  
  <s:attribute type="CompanyName"/>  
  <s:attribute type="Phone"/>  
  <s:extends type="rs:rowbase"/>  
</s:ElementType>  
```  
  
 画面のデータを永続化プロバイダーは、ADO は更新可能なレコード セット オブジェクトを構築できるようにこの指示します。  
  
 次のサンプル データは、挿入、変更、および削除が永続化されたファイルで検索する方法を示しています。  
  
```  
<rs:data>  
  <z:row ShipperID="2" CompanyName="United Package"   
    Phone="(503) 555-3199"/>  
<rs:update>  
  <rs:original>  
    <z:row ShipperID="3" CompanyName="Federal Shipping"   
      Phone="(503) 555-9931"/>  
  </rs:original>  
  <z:row Phone="(503) 552-7134"/>  
</rs:update>  
<rs:insert>  
  <z:row ShipperID="12" CompanyName="Lightning Shipping"   
    Phone="(505) 111-2222"/>  
  <z:row ShipperID="13" CompanyName="Thunder Overnight"   
    Phone="(505) 111-2222"/>  
  <z:row ShipperID="14" CompanyName="Blue Angel Air Delivery"   
    Phone="(505) 111-2222"/>  
</rs:insert>  
<rs:delete>  
  <z:row ShipperID="1" CompanyName="Speedy Express" Phone="(503) 555-9831"/>  
</rs:delete>  
</rs:data>  
```  
  
 更新プログラムには、常に続く行が変更されたデータ全体の元の行データが含まれています。 変更された行には、すべての列または実際に変更された列のみを含めることができます。 前の例では、出荷業者の 2 行は変更されませんあり Phone 列のみ運送会社 3 の値が変更および変更された行に含まれる唯一の列は、そのため。 12、13、14 の運送会社に挿入された行は、バッチ化 rs: 挿入の 1 つのタグです。 これは、前の例で示されていませんが、削除された行もバッチ処理できる同時に、注意してください。  
  
## <a name="see-also"></a>参照  
 [レコードを XML 形式で保持する](../../../ado/guide/data/persisting-records-in-xml-format.md)
