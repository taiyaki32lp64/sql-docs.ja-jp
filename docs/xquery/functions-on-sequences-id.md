---
title: id 関数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:id function
- id function
ms.assetid: de99fc60-d0ad-4117-a17d-02bdde6512b4
author: rothja
ms.author: jroth
ms.openlocfilehash: 21bf98ac97c9a695b7b9576412d43c832011322d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004659"
---
# <a name="functions-on-sequences---id"></a>シーケンスの関数 - id
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  提供された xs:IDREF 値の 1 つ以上の値と一致する xs:ID 値を持つ要素ノードのシーケンスを返します *$arg*します。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:id($arg as xs:IDREF*) as element()*  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 1 つ以上の xs:IDREF 値。  
  
## <a name="remarks"></a>コメント  
 関数の結果は、xs:ID 値と等しく、xs:IDREFs の 1 つ以上 xs:IDREFs の候補の一覧で、ドキュメント順で、XML インスタンス内の要素のシーケンスです。  
  
 xs:IDREF 値がどの要素とも一致しない場合は、空のシーケンスを返します。  
  
## <a name="examples"></a>使用例  
 このトピックではさまざまなに格納されている XML インスタンスに対して XQuery の例について**xml**内の列を入力、[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]データベース。  
  
### <a name="a-retrieving-elements-based-on-the-idref-attribute-value"></a>A. IDREF 属性値に基づいて要素を取得します。  
 次の例では、fn:id を使用して、取得、<`employee`>、IDREF マネージャー属性に基づいて、要素。 この例では、マネージャー属性は IDREF 型の属性で、eid 属性は ID 型の属性です。  
  
 、特定のマネージャー属性の値の、 **id()** 検索の機能、<`employee`> 要素の ID 型属性値が入力の IDREF 値と一致します。 つまり、特定の従業員の**id()** 関数は、従業員のマネージャーを返します。  
  
 この例では次のことが行われます。  
  
-   XML スキーマ コレクションが作成されます。  
  
-   型指定された**xml** XML スキーマ コレクションを使用して変数を作成します。  
  
-   クエリによって参照される ID 属性値を持つ要素を取得する、 **manager**の IDREF 属性、<`employee`> 要素。  
  
```  
-- If exists, drop the XML schema collection (SC).  
-- drop xml schema collection SC  
-- go  
  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:e="emp" targetNamespace="emp">  
            <element name="employees" type="e:EmployeesType"/>  
            <complexType name="EmployeesType">  
                 <sequence>  
                      <element name="employee" type="e:EmployeeType" minOccurs="0" maxOccurs="unbounded" />  
                 </sequence>  
            </complexType>    
  
            <complexType name="EmployeeType">  
                        <attribute name="eid" type="ID" />  
                        <attribute name="name" type="string" />  
                        <attribute name="manager" type="IDREF" />  
            </complexType>         
</schema>'  
go  
```  
  
```  
declare @x xml(SC)  
set @x='<e:employees xmlns:e="emp">  
<employee eid="e1" name="Joe" manager="e10" />  
<employee eid="e2" name="Bob" manager="e10" />  
<employee eid="e10" name="Dave" manager="e10" />  
</e:employees>'  
  
select @x.value(' declare namespace e="emp";   
 (fn:id(e:employees/employee[@name="Joe"]/@manager)/@name)[1]', 'varchar(50)')   
Go  
```  
  
 クエリでは、値として"Dave"を返します。 これは、Dave が Joe のマネージャーであることを示します。  
  
### <a name="b-retrieving-elements-based-on-the-orderlist-idrefs-attribute-value"></a>B. OrderList IDREFS 属性値に基づいて要素を取得する  
 次の例では、OrderList 属性で、<`Customer`> 要素は IDREFS 型の属性。 この例では特定の顧客に対応する注文 ID がリストされます。 各注文 id は、<`Order`> 下の子要素、<`Customer`> 順序の値を指定します。  
  
 クエリ式 `data(CustOrders:Customers/Customer[1]/@OrderList)[1]` では、最初の顧客の最初の値が IDRES 一覧から取得されます。 この値に渡されます、 **id()** 関数。 関数で検索し、<`Order`> 要素の OrderID 属性値への入力に一致、 **id()** 関数。  
  
```  
drop xml schema collection SC  
go  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:Customers="Customers" targetNamespace="Customers">  
            <element name="Customers" type="Customers:CustomersType"/>  
            <complexType name="CustomersType">  
                        <sequence>  
                            <element name="Customer" type="Customers:CustomerType" minOccurs="0" maxOccurs="unbounded" />  
                        </sequence>  
            </complexType>  
             <complexType name="OrderType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="OrderValue" type="integer" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="OrderID" type="ID" />  
            </complexType>  
  
            <complexType name="CustomerType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="spouse" type="string" minOccurs="0" maxOccurs="unbounded"/>  
                                <element name="Order" type="Customers:OrderType" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="CustomerID" type="string" />  
                <attribute name="OrderList" type="IDREFS" />  
            </complexType>  
 </schema>'  
go  
declare @x xml(SC)  
set @x='<CustOrders:Customers xmlns:CustOrders="Customers">  
                <Customer CustomerID="C1" OrderList="OrderA OrderB"  >  
                              <spouse>Jenny</spouse>  
                                <Order OrderID="OrderA"><OrderValue>11</OrderValue></Order>  
                                <Order OrderID="OrderB"><OrderValue>22</OrderValue></Order>  
  
                </Customer>  
                <Customer CustomerID="C2" OrderList="OrderC OrderD" >  
                                <spouse>John</spouse>  
                                <Order OrderID="OrderC"><OrderValue>33</OrderValue></Order>  
                                <Order OrderID="OrderD"><OrderValue>44</OrderValue></Order>  
  
                        </Customer>  
                <Customer CustomerID="C3"  OrderList="OrderE OrderF" >  
                                <spouse>Jane</spouse>  
                                <Order OrderID="OrderE"><OrderValue>55</OrderValue></Order>  
                                <Order OrderID="OrderF"><OrderValue>55</OrderValue></Order>  
                </Customer>  
                <Customer CustomerID="C4"  OrderList="OrderG"  >  
                                <spouse>Tim</spouse>  
                                <Order OrderID="OrderG"><OrderValue>66</OrderValue></Order>  
                        </Customer>  
                <Customer CustomerID="C5"  >  
                </Customer>  
                <Customer CustomerID="C6" >  
                </Customer>  
                <Customer CustomerID="C7"  >  
                </Customer>  
</CustOrders:Customers>'  
select @x.query('declare namespace CustOrders="Customers";  
  id(data(CustOrders:Customers/Customer[1]/@OrderList)[1])')  
  
-- result  
<Order OrderID="OrderA">  
  <OrderValue>11</OrderValue>  
</Order>  
```  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 制限事項を次に示します。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 引数が 2 つのバージョンをサポートしていません**id()** します。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 引数の型を必要と**id()** xs:IDREF* のサブタイプにします。  
  
## <a name="see-also"></a>関連項目  
 [シーケンスの関数](https://msdn.microsoft.com/library/672d2795-53ab-49c2-bf24-bc81a47ecd3f)  
  
  
