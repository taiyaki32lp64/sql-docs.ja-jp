---
title: FOR XML での EXPLICIT モードの使用 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- EXPLICIT FOR XML mode
- FOR XML clause, EXPLICIT mode
- FOR XML EXPLICIT mode
ms.assetid: 8b26e8ce-5465-4e7a-b237-98d0f4578ab1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8976b77bf0823c9735e6e6e67fc3159bcb54ecdf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63231272"
---
# <a name="use-explicit-mode-with-for-xml"></a>FOR XML での EXPLICIT モードの使用
  トピック「 [FOR XML を使用した XML の構築](../xml/for-xml-sql-server.md)」で説明されているように、RAW モードと AUTO モードでは、クエリ結果から生成される XML の構造を厳密に制御することはできません。 一方、EXPLICIT モードを使用すると、クエリ結果から生成される XML の構造を柔軟に制御することができます。  
  
 ただし、必要な XML に関する追加情報 (XML 内の入れ子構造など) をクエリの一部として明示的に指定するために、EXPLICIT モードのクエリを記述する際には特殊な記述方法が必要になります。 このため、要求する XML によっては、EXPLICIT モードのクエリを記述する作業が複雑になることがあります。 EXPLICIT モードのクエリを記述するよりも、 [PATH モード](../xml/use-path-mode-with-for-xml.md) で入れ子を使用する方が作業が容易になる場合もあります。  
  
 EXPLICIT モードでは、目的の XML をクエリによって記述するので、正しい形式で有効な XML が生成されるかどうかを確認する必要があります。  
  
## <a name="rowset-processing-in-explicit-mode"></a>EXPLICIT モードでの行セットの処理  
 EXPLICIT モードでは、クエリを実行した結果として生じた行セットが XML に変換されます。 EXPLICIT モードで XML ドキュメントを作成するには、特殊な形式の行セットが必要になります。 そのためには、XML を処理ロジックで生成できるように、決められた形式の行セット ( **ユニバーサル テーブル**) を生成できるような選択クエリを記述する必要があります。  
  
 まず、クエリで次の 2 つのメタデータ列を生成します。  
  
-   1 列目は **Tag**という名前で、現在の要素のタグ番号 (整数型) を指定します。 行セットから構築される要素ごとに、一意のタグ番号をクエリが提供しなければなりません。  
  
-   2 列目は **Parent**という名前で、親要素のタグ番号を指定します。 これにより、Tag 列と Parent 列の階層情報が定義されます。  
  
 XML を生成する際には、これらのメタデータ列の値が、列名の情報と共に使用されます。 列名は、特殊な方法でクエリ内に指定します。 **Parent** 列の値が 0 または NULL であれば、その要素に親要素がないことを示します。 このような要素は、最上位の要素として XML に追加されます。  
  
 クエリで生成したユニバーサル テーブルが、どのように処理され、XML として生成されるか、例を検証しましょう。ここでは、次のユニバーサル テーブルを生成するクエリを記述したとします。  
  
 ![ユニバーサル テーブルのサンプル](../../database-engine/media/xmlutable.gif "ユニバーサル テーブルのサンプル")  
  
 このユニバーサル テーブルについて説明します。  
  
-   最初の 2 列は **Tag** 列と **Parent** 列で、これらはメタデータ列です。 これらの値は、階層を決定します。  
  
-   列名は、このトピックの後半で説明するように、決められた方法で指定する必要があります。  
  
-   このユニバーサル テーブルから XML を生成する際、このテーブルのデータは列方向に (列グループに) パーティション分割されます。 このグループ化は、 **Tag** 列の値と列名によって決まります。 XML の生成時には、各行ごとに 1 つの列グループが選択され、1 つの要素が構築されます。 この処理は、この例では次のように行われます。  
  
    -   1 行目の **Tag** 列の値は 1 なので、同じタグ番号を列名に含んでいる **Customer!1!cid**  列と **Customer!1!name** 列でグループが形成されます。 これらの列が行の処理に使用され、生成される要素の形式は <`Customer id=... name=...`> のようになります。 列名の形式については、このトピックの後半で説明します。  
  
    -   **Tag** 列の値が 2 の行については、**Order!2!id** 列と **Order!2!date** 列でグループが形成され、<`Order id=... date=... /`> という形式の要素が生成されます。  
  
    -   **Tag** 列の値が 3 の行については、**OrderDetail!3!id!id** 列と **OrderDetail!3!pid!idref** 列でグループが形成されます。 これらの列からは、<`OrderDetail id=... pid=...`> という形式の要素が生成されます。  
  
-   XML 階層の生成時、行は順番に処理されます。 XML 階層は、次のように決定されます。  
  
    -   1 行目では、**Tag** 列に値 1 が指定され、**Parent** 列には NULL が指定されています。 したがって、対応する <`Customer`> 要素は、XML の最上位要素として追加されます。  
  
        ```  
        <Customer cid="C1" name="Janine">  
        ```  
  
    -   2 行目では、**Tag** 列に値 2、**Parent** 列に値 1 が指定されています。 したがって、<`Customer`> 要素の子要素として、<`Order`> 要素が追加されます。  
  
        ```  
        <Customer cid="C1" name="Janine">  
           <Order id="O1" date="1/20/1996">  
        ```  
  
    -   次の 2 行では、**Tag** 列に値 3、**Parent** 列に値 2 が指定されています。 したがって、<`Order`> 要素の子要素として、2 つの <`OrderDetail`> 要素が追加されます。  
  
        ```  
        <Customer cid="C1" name="Janine">  
           <Order id="O1" date="1/20/1996">  
              <OrderDetail id="OD1" pid="P1"/>  
              <OrderDetail id="OD2" pid="P2"/>  
        ```  
  
    -   最後の行では、**Tag** 列に値 2 が指定され、**Parent** 列には値 1 が指定されています。 したがって、<`Customer`> 親要素には、別の <`Order`> 子要素が追加されます。  
  
        ```  
        <Customer cid="C1" name="Janine">  
           <Order id="O1" date="1/20/1996">  
              <OrderDetail id="OD1" pid="P1"/>  
              <OrderDetail id="OD2" pid="P2"/>  
           </Order>  
           <Order id="O2" date="3/29/1997">  
        </Customer>  
        ```  
  
 つまり、EXPLICIT モードでは、**Tag** メタデータ列と **Parent** メタデータ列の値、各列名に提供されている情報、および列の正しい順序に基づいて、必要な XML を生成できるということになります。  
  
### <a name="universal-table-row-ordering"></a>ユニバーサル テーブルの行の順序  
 XML の生成時、ユニバーサル テーブルの行は順番に処理されます。 そのため、親と関連付けられている適切な子インスタンスを取得するには、各親ノードの直後がその親の子ノードになるという順序で、行セットの行が並んでいる必要があります。  
  
## <a name="specifying-column-names-in-a-universal-table"></a>ユニバーサル テーブルでの列名の指定  
 EXPLICIT モードのクエリを記述する際に、結果の行セットの列名は、この形式を使用して指定します。 列名では、ディレクティブを使用して、要素と属性の名前や他の追加情報などを含めた変換情報を指定します。  
  
 次に一般的な形式を示します。  
  
```  
  
ElementName!TagNumber!AttributeName!Directive  
```  
  
 各部分の説明は、次のとおりです。  
  
 *ElementName*  
 結果の要素の汎用識別子。 たとえば、*ElementName* として **Customers** が指定されている場合、\<Customers> 要素が生成されます。  
  
 *TagNumber*  
 要素に割り当てられる一意なタグの値。 この値と **Tag** および **Parent**の 2 つのメタデータ列の組み合わせにより、生成される XML 内の要素の入れ子構造が決定されます。  
  
 *AttributeName*  
 指定した *ElementName*要素に作成する属性の名前。 これは、 *Directive* を指定しない場合の動作です。  
  
 *Directive* に **xml**、 **cdata**、または **element**のいずれかが指定されている場合、この値は *ElementName*要素の子要素の構築に使用され、列値がその子要素に追加されます。  
  
 *Directive*を指定した場合、 *AttributeName* は省略できます。 たとえば、ElementName!TagNumber!!Directive という形式を指定したとします。 この場合、列値は、 *ElementName*に直接格納されます。  
  
 *Directive*  
 *Directive* は、XML を生成するための追加情報を指定する場合に使用しますが、省略可能です。 *Directive* には、2 つの目的があります。  
  
 1 つ目の目的は、値を ID、IDREF、および IDREFS としてエンコードすることです。 それには、 **Directives**として、 **ID**、 **IDREF** 、および *IDREFS*キーワードを指定します。 これらのディレクティブを指定すると、属性の型が上書きされます。 これにより、ドキュメント内でのリンクを作成できるようになります。  
  
 *Directive* を使用する 2 つ目の目的は、文字列データをどのように XML にマップするかを指定することです。 **Directive**としては、 **hide**、 **element、elementxsinil**、 **xml**、 **xmltext** 、 *cdata*の各キーワードを使用できます。 **hide** ディレクティブを指定した場合は、ノードが非表示になります。 このディレクティブは、ノードを並べ替えるだけの目的で値を取得し、生成する XML にはその値を表示しない場合に役立ちます。  
  
 **element** ディレクティブを指定すると、属性ではなく子要素 (含まれる要素) が生成されます。 含まれる要素のデータは、エンティティとしてエンコードされます。 たとえば、文字 **<** は &lt;になります。 列の値が NULL であれば、要素は生成されません。 列の値が NULL である場合にも要素を生成する場合は、 **elementxsinil** ディレクティブを指定します。 このディレクティブを指定すると、xsi:nil=TRUE 属性を持つ要素が生成されます。  
  
 **xml** ディレクティブは、 **element** ディレクティブと似ていますが、エンティティのエンコードが行われない点が異なります。 また、 **element** ディレクティブは **ID**、 **IDREF**、または **IDREFS**と組み合わせて使用できますが、 **xml** ディレクティブは **hide**以外のディレクティブと組み合わせて使用することができない点にも注意してください。  
  
 **cdata** ディレクティブを使用した場合は、データが CDATA セクション内に取り込まれます。 CDATA セクションの内容については、エンティティのエンコードが行われません。 元のデータ型は、 **varchar**、 **nvarchar**、 **text**、または **ntext**などのテキスト型でなければなりません。 このディレクティブと組み合わせて使用できるのは、 **hide**ディレクティブだけです。 このディレクティブを使用する場合、 *AttributeName* は指定できません。  
  
 この 2 つのグループ間でディレクティブを組み合わせることは、ほとんどの場合に可能ですが、同じグループ内のディレクティブを組み合わせることはできません。  
  
 *Directive* と *AttributeName* が指定されていない場合を考えます。たとえば、 **Customer!1**の場合、 **Customer!1!!element** のように **element**ディレクティブが暗黙的に指定され、列のデータが *ElementName*に格納されます。  
  
 **xmltext** ディレクティブを指定すると、列の内容は 1 つのタグで囲まれ、ドキュメントの残りの部分に統合されます。 このディレクティブは、OPENXML によって列に格納されている未使用のオーバーフロー XML データを収集する場合に役に立ちます。 詳細については、「[OPENXML &#40;SQL Server&#41;](../xml/openxml-sql-server.md)」を参照してください。  
  
 *AttributeName* を指定した場合、タグ名は指定した名前に置き換えられます。 それ以外の場合、属性は囲み要素の現在の属性リストに追加され、内容は囲み要素の内容として先頭に追加されます。このとき、エンティティのエンコードは行われません。 このディレクティブを指定する列は、 **varchar**、 **nvarchar**、 **char**、 **nchar**、 **text**、または **ntext**などのテキスト型でなければなりません。 このディレクティブと組み合わせて使用できるのは、 **hide**ディレクティブだけです。 このディレクティブは、列に格納されているオーバーフロー データを収集する場合に役立ちます。 内容が、正しい形式の XML でない場合は、動作が不確定な状態になります。  
  
## <a name="in-this-section"></a>このセクションの内容  
 次の例では、EXPLICIT モードの使用方法を示します。  
  
-   [例: 従業員情報の取得](../xml/example-retrieving-employee-information.md)  
  
-   [例: ELEMENT ディレクティブの指定](../xml/example-specifying-the-element-directive.md)  
  
-   [例: ELEMENTXSINIL ディレクティブの指定](../xml/example-specifying-the-elementxsinil-directive.md)  
  
-   [例: EXPLICIT モードを使用した兄弟の構築](../xml/example-constructing-siblings-with-explicit-mode.md)  
  
-   [例: ID ディレクティブと IDREF ディレクティブの指定](../xml/example-specifying-the-id-and-idref-directives.md)  
  
-   [例: ID ディレクティブと IDREFS ディレクティブの指定](../xml/example-specifying-the-id-and-idrefs-directives.md)  
  
-   [例: HIDE ディレクティブの指定](../xml/example-specifying-the-hide-directive.md)  
  
-   [例: ELEMENT ディレクティブとエンティティのエンコードの指定](../xml/example-specifying-the-element-directive-and-entity-encoding.md)  
  
-   [例: CDATA ディレクティブの指定](../xml/example-specifying-the-cdata-directive.md)  
  
-   [例: XMLTEXT ディレクティブの指定](../xml/example-specifying-the-xmltext-directive.md)  
  
## <a name="see-also"></a>参照  
 [FOR XML での RAW モードの使用](../xml/use-raw-mode-with-for-xml.md)   
 [FOR XML での AUTO モードの使用](../xml/use-auto-mode-with-for-xml.md)   
 [FOR XML での PATH モードの使用](../xml/use-path-mode-with-for-xml.md)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [FOR XML &#40;SQL Server&#41;](../xml/for-xml-sql-server.md)  
  
  
