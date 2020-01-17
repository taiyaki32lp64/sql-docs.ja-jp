---
title: distinct-values 関数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- distinct-values function
- fn:distinct-values function
ms.assetid: f4c2bb53-2bec-4f1a-9c00-cf997fb7ae5b
author: rothja
ms.author: jroth
ms.openlocfilehash: d2f856c9b351c776651f08e66f90c7f567a5dcfc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68223732"
---
# <a name="functions-on-sequences---distinct-values"></a>シーケンスの関数 - distinct-values
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  重複する値で指定されたシーケンスから削除します *$arg*します。 場合 *$arg*空のシーケンスが空のシーケンスを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:distinct-values($arg as xdt:anyAtomicType*) as xdt:anyAtomicType*  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 アトミック値のシーケンス。  
  
## <a name="remarks"></a>コメント  
 すべての種類に渡されるアトミック値の**distinct-values()** 同じ基本型のサブタイプにする必要があります。 受け付けられるベースの型をサポートする型では、 **eq**操作。 これらの型には、次の 3 つの組み込み数値基本データ型、日付/時刻の基本型、xs:string、xs:boolean、および xdt:untypedAtomic が含まれます。 Xdt:untypedAtomic 型の値は、xs:string にキャストされます。 これらの型の混在がある場合、またはその他の種類の他の値が渡された場合は、静的エラーが発生します。  
  
 結果**distinct-values()** 元のカーディナリティを持つ、xdt:untypedAtomic の場合に xs:string など、渡された型の基本型を受信します。 入力が静的に空の場合、結果が暗黙的し、静的エラーが発生します。  
  
 Xs:string 型の値は、XQuery の既定の Unicode コード ポイント照合順序と比較されます。  
  
## <a name="examples"></a>使用例  
 このトピックではさまざまなに格納されている XML インスタンスに対して XQuery の例について**xml**型の列には、AdventureWorks データベース。  
  
### <a name="a-using-the-distinct-values-function-to-remove-duplicate-values-from-the-sequence"></a>A. Distinct-values() 関数を使用して、シーケンスから重複する値を削除するには  
 この例では電話番号を含む XML インスタンスが割り当てられている、 **xml**型の変数。 この変数を使用してに対して指定した XQuery、 **distinct-values()** 重複部分を含まない電話番号の一覧をコンパイルする関数。  
  
```  
declare @x xml  
set @x = '<PhoneNumbers>  
 <Number>111-111-1111</Number>  
 <Number>111-111-1111</Number>  
 <Number>222-222-2222</Number>  
</PhoneNumbers>'  
-- 1st select  
select @x.query('  
  distinct-values( data(/PhoneNumbers/Number) )  
') as result  
```  
  
 結果を次に示します。  
  
```  
111-111-1111 222-222-2222    
```  
  
 次のクエリでは、一連の数値 (1, 1, 2) に渡される、 **distinct-values()** 関数。 関数は、シーケンス内の重複する値を削除し、結果として得られた 2 つの値を返します。  
  
```  
declare @x xml  
set @x = ''  
select @x.query('  
  distinct-values((1, 1, 2))  
') as result  
```  
  
 クエリでは、1 2 を返します。  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 制限事項を次に示します。  
  
-   **Distinct-values()** 関数では、整数値を xs:decimal にマップします。  
  
-   **Distinct-values()** のみ関数を上記の型をサポートし、基本データ型の混在をサポートしていません。  
  
-   **Distinct-values()** xs:duration 型の値に対して関数がサポートされていません。  
  
-   照合順序を指定する構文オプションはサポートされていません。  
  
## <a name="see-also"></a>関連項目  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
