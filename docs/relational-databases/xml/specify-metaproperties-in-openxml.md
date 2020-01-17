---
title: OPENXML 内でのメタプロパティの指定 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- overflow in XML document [SQL Server]
- metaproperties [XML in SQL Server]
- unconsumed data
- extracting information of XML nodes [SQL Server]
- OPENXML statement, metaproperties
ms.assetid: 29bfd1c6-3f9a-43c4-924a-53d438e442f4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9354bf1c1539a7ba83f1af1eafdb27ed99041d76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68000696"
---
# <a name="specify-metaproperties-in-openxml"></a>OPENXML 内でのメタプロパティの指定
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  XML ドキュメントに含まれるメタプロパティ属性は、XML アイテム (要素、属性、その他の DOM ノードなど) のプロパティを示す属性です。 これらの属性は、物理的に XML ドキュメントのテキスト内に存在するものではありません。 ただし、OPENXML では、すべての XML アイテムに、これらのメタプロパティが提供されます。 これらのメタプロパティを使用すると、XML ノードの情報 (ローカルの位置や名前空間の情報など) を抽出できます。 これらの情報からは、テキストで表現されている情報よりも詳細な情報を得られます。  
  
 これらのメタプロパティは、 *ColPattern* パラメーターを使用して OPENXML ステートメント内の行セットの列にマップできます。 これらの列には、その列がマップされたメタプロパティの値が含まれます。 OPENXML の構文の詳細については、 [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)を参照してください。  
  
 これらのメタプロパティ属性にアクセスするために、SQL Server 固有の名前空間が提供されています。 ユーザーは、この名前空間 **urn:schemas-microsoft-com:xml-metaprop** を使用して、メタプロパティ属性にアクセスできます。 OPENXML クエリの結果がエッジ テーブル形式で返される場合、そのエッジ テーブルには、 **xmltext** メタプロパティ以外のメタプロパティ属性ごとに 1 つの列が含まれます。  
  
 一部のメタプロパティ属性は、処理の目的で使用されます。 たとえば **xmltext** メタプロパティ属性は、オーバーフロー処理のために使用されます。 オーバーフロー処理では、ドキュメントに含まれる未使用および未処理データを参照します。 OPENXML によって生成された行セット内の列の 1 つは、オーバーフロー列として識別されるようにすることができます。 ある列がオーバーフロー列として識別されるようにするには、 **ColPattern** パラメーターを使用して、この列を *xmltext* メタプロパティにマップします。 このマッピングを行うと、列はオーバーフロー データを受け取ります。 列に含まれるのが未使用データだけなのかすべてのデータなのかは *flags* パラメーターによって判断します。  
  
 次の表に、解析されたそれぞれの XML 要素が所有するメタプロパティ属性を示します。 これらのメタプロパティ属性には、名前空間 **urn:schemas-microsoft-com:xml-metaprop**を使用してアクセスできます。 ただし、ユーザーがこれらのメタプロパティを使用して XML ドキュメントに直接設定した値は無視されます。  
  
> [!NOTE]  
>  これらのメタプロパティは、XPath による位置指定では参照できません。  
  
|メタプロパティ属性|[説明]|  
|----------------------------|-----------------|  
|**\@mp:id**|DOM ノードに対して、システムによって生成されたドキュメント レベルの識別子を提供します。 この ID は、ドキュメントが再解析されない限り、同じ XML ノードを参照します。<br /><br /> XML ID が **0** の場合、その要素はルート要素です。 その親要素の XML ID は NULL になります。|  
|**\@mp:localname**|ノードの名前のローカル部分を格納します。 要素ノードや属性ノードの名前付けの際に、プレフィックスおよび名前空間 URI と共に使用します。|  
|**\@mp:namespaceuri**|現在の要素の名前空間 URI を指定します。 この属性の値が NULL の場合は、名前空間がありません。|  
|**\@mp:prefix**|現在の要素名の名前空間プレフィックスを格納します。<br /><br /> プレフィックスがなくて (NULL) URI が指定されている場合は、指定された名前空間が既定の名前空間であることを示します。 URI が指定されていない場合は、名前空間が関連付けられていません。|  
|**\@mp:prev**|ノードよりも前の兄弟を格納します。 これにより、ドキュメント内の要素の順序に関する情報が得られます。<br /><br /> **\@mp:prev** には、同じ親要素を持つ前の兄弟要素の XML ID が含まれます。 要素が兄弟リストの先頭にある場合、 **\@mp:prev** は NULL になります。|  
|**\@mp:xmltext**|処理の目的で使用します。 OPENXML のオーバーフロー処理で使用したように、要素とその属性とサブ要素のテキストをシリアル化したものです。|  
  
 次の表には、用意されている追加の親プロパティを示します。これらのプロパティを使用すると、階層情報を取得できます。  
  
|親メタプロパティ属性|[説明]|  
|-----------------------------------|-----------------|  
|**\@mp:parentid**|**../\@mp:id** と対応します。|  
|**\@mp:parentlocalname**|**../\@mp:localname** と対応します。|  
|**\@mp:parentnamespacerui**|**../\@mp:namespaceuri** と対応します。|  
|**\@mp:parentprefix**|**../\@mp:prefix** と対応します。|  
  
## <a name="examples"></a>使用例  
 次に、OPENXML を使用してさまざまな行セット ビューを作成する方法の例を示します。  
  
### <a name="a-mapping-the-openxml-rowset-columns-to-the-metaproperties"></a>A. OPENXML 行セット列のメタプロパティへのマップ  
 この例では、OPENXML を使用して、サンプルの XML ドキュメントの行セット ビューを作成します。 具体的には、 *ColPattern* パラメーターを使用して、OPENXML ステートメントで各種のメタプロパティ属性を行セットの列にマップする方法を示します。  
  
 この OPENXML ステートメントは、次のことを表します。  
  
-   **id** 列が **\@mp:id** メタプロパティ属性にマップされます。また、システムによって生成された要素の一意な XML ID がこの列に含まれることを示しています。  
  
-   **parent** 列が **\@mp:parentid** にマップされます。また、要素の親要素の XML ID がこの列に含まれることを示しています。  
  
-   **parentLocalName** 列が **\@mp:parentlocalname** にマップされます。また、親のローカル名がこの列に含まれることを示しています。  
  
 SELECT ステートメントは OPENXML で提供された行セットを返します。  
  
```  
DECLARE @idoc int  
DECLARE @doc nvarchar(1000)  
-- Sample XML document  
SET @doc = N'<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue white red">  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@idoc, '/root/Customer/Order', 9)  
      WITH (id int '@mp:id',   
            oid char(5),   
            date datetime,   
            amount real,   
            parentIDNo int '@mp:parentid',   
            parentLocalName varchar(40) '@mp:parentlocalname')  
EXEC sp_xml_removedocument @idoc  
```  
  
 結果を次に示します。  
  
```  
id   oid         date                amount    parentIDNo  parentLocalName    
--- ------- ---------------------- ---------- ------------ ---------------  
6    O1    1996-01-20 00:00:00.000     3.5         2        Customer  
10   O2    1997-04-30 00:00:00.000     13.4        2        Customer  
19   O3    1999-07-14 00:00:00.000     100.0       15       Customer  
25   O4    1996-01-20 00:00:00.000     10000.0     15       Customer  
```  
  
### <a name="b-retrieving-the-whole-xml-document"></a>B. XML ドキュメント全体の取得  
 この例では、OPENXML を使用して、サンプルの XML ドキュメントの 1 列の行セット ビューが作成されます。 この列 ( **Col1**) は **xmltext** メタプロパティにマップされ、オーバーフロー列になります。 そのため、この列は未使用データを受け取ります。 この例の場合、この列には、ドキュメント全体が格納されます。  
  
 SELECT ステートメントは行セット全体を返します。  
  
```  
DECLARE @idoc int  
DECLARE @doc nvarchar(1000)  
SET @doc = N'<?xml version="1.0"?>  
<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very   
             satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue   
             white red">  
     <MyTag>Testing to see if all the subelements are returned</MyTag>  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@idoc, '/')  
   WITH (Col1 ntext '@mp:xmltext')  
```  
  
 XML 宣言を使用しないでドキュメント全体を取得するには、クエリを次のように指定します。  
  
```  
SELECT *  
FROM OPENXML (@idoc, '/root')  
   WITH (Col1 ntext '@mp:xmltext')  
EXEC sp_xml_removedocument @idoc  
```  
  
 クエリはルート要素を返し、これには名前のルートおよびルート要素に含まれるデータが含まれます。  
  
### <a name="c-specifying-the-xmltext-metaproperty-to-retrieve-the-unconsumed-data-in-a-column"></a>C. xmltext メタプロパティの指定による列内の未使用データの取得  
 この例では、OPENXML を使用して、サンプルの XML ドキュメントの行セット ビューを作成します。 この例では、OPENXML 内の行セットの列に **xmltext** メタプロパティ属性をマップすることによって、未使用の XML データを取得する方法について説明します。  
  
 **comment** 列は、 **\@mp:xmltext** メタプロパティにマップすることによって、オーバーフロー列として識別されます。 *flags* パラメーターは **9** (XML_ATTRIBUTE and XML_NOCOPY) に設定されています。 この設定は、 **属性中心** のマッピングであり、未使用データのみがオーバーフロー列にコピーされることを示しています。  
  
 SELECT ステートメントは OPENXML で提供される行セットを返します。  
  
 この例では、OPENXML によって生成された行セット内の列 (**ParentLocalName**) に対して **\@mp:parentlocalname** メタプロパティが設定されます。 その結果、この列には親要素のローカル名が含まれます。  
  
 行セットには他に 2 つの列 ( **parent** と **comment**) が指定されています。 **parent** 列は **\@mp:parentid** にマップされ、この列に、要素の親要素の XML ID が含まれることを示します。 comment 列は、 **\@mp:xmltext** メタプロパティにマップすることによって、オーバーフロー列として識別されます。  
  
```  
DECLARE @idoc int  
DECLARE @doc nvarchar(1000)  
-- sample XML document  
SET @doc = N'<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue white red">  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>  
'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@idoc, '/root/Customer/Order', 9)  
      WITH (oid char(5),   
            date datetime,  
            comment ntext '@mp:xmltext')  
EXEC sp_xml_removedocument @idoc  
```  
  
 結果は次のとおりです。 oid 列と date 列は既に使用されているので、それらはオーバーフロー列には表示されません。  
  
```  
oid   date                        comment                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            
----- --------------------------- ----------------------------------------  
O1    1996-01-20 00:00:00.000     <Order amount="3.5"/>  
O2    1997-04-30 00:00:00.000     <Order amount="13.4">Customer was very   
                                   satisfied</Order>  
O3    1999-07-14 00:00:00.000     <Order amount="100" note="Wrap it blue   
                                   white red"><Urgency>   
                                   Important</Urgency></Order>  
O4    1996-01-20 00:00:00.000     <Order amount="10000"/>  
```  
  
## <a name="see-also"></a>参照  
 [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)   
 [OPENXML &#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
  
  
