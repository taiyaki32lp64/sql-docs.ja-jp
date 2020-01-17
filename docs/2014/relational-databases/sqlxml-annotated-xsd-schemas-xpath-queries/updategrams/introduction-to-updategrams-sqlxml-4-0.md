---
title: アップデート グラム (SQLXML 4.0) の概要 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- explicit schema mapping [SQLXML]
- updategrams [SQLXML], mapping schema specifying
- namespaces [SQLXML]
- updategrams [SQLXML], about updategrams
- attribute-centric mapping
- invalid characters [SQLXML]
- element-centric mapping [SQLXML]
- mapping schema [SQLXML], updategrams
- namespaces [SQLXML], updategrams
- executing updategrams [SQLXML]
- implicit schema mapping
ms.assetid: cfe24e82-a645-4f93-ab16-39c21f90cce6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 114bc96623b608cfbb520a9d2f35f23a04310a74
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014799"
---
# <a name="introduction-to-updategrams-sqlxml-40"></a>アップデートグラムの概要 (SQLXML 4.0)
  変更することができます (挿入、更新、または削除) でデータベース[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]アップデート グラムまたは OPENXML を使用して文書化、既存の XML から[!INCLUDE[tsql](../../../includes/tsql-md.md)]関数。  
  
 OPENXML 関数は、既存の XML ドキュメントを断片化し、INSERT、UPDATE または DELETE ステートメントに渡すことができる行セットを提供することで、データベースを変更する関数です。 OPENXML を使用すると、データベース テーブルに対して操作を直接実行できます。 したがって、ソースにテーブルなどの行セット プロバイダーがある場合は常に、OPENXML を使用するのが最適です。  
  
 アップデートグラムを使用すると、OPENXML と同様にデータベースに対してデータを挿入、更新、または削除できます。ただし、アップデートグラムは注釈付き XSD (または XDR) スキーマにより提供される XML ビューに対して動作します。たとえば、更新はマッピング スキーマにより提供される XML ビューに適用されます。 マッピング スキーマには、XML 要素と属性を対応するデータベース テーブルと列にマップするための、必要な情報が含まれています。 アップデートグラムでは、このマッピング情報を使用してデータベース テーブルと列が更新されます。  
  
> [!NOTE]  
>  このドキュメントは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でサポートされるテンプレートとマッピング スキーマについて理解していることを前提としています。 詳細については、次を参照してください。[注釈付き XSD スキーマの概要&#40;SQLXML 4.0&#41;](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)します。 XDR を使用する従来のアプリケーションでは、次を参照してください。[注釈付き XDR スキーマ&#40;SQLXML 4.0 では非推奨&#41;](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)します。  
  
## <a name="required-namespaces-in-the-updategram"></a>アップデートグラムで必要な名前空間  
 アップデート グラムでは、キーワードなど **\<同期 >** 、 **\<する前に >** 、および **\<後 >** 、内に存在`urn:schemas-microsoft-com:xml-updategram`名前空間。 名前空間プレフィックスは、任意のものを使用できます。 このドキュメントでは、`updg` 名前空間を表すものとして `updategram` プレフィックスを使用します。  
  
## <a name="reviewing-syntax"></a>構文の確認  
 アップデート グラムはテンプレートを **\<同期 >** 、 **\<する前に >** 、および **\<後 >** ブロックの構文を形成する、アップデート グラムです。 次のコードは、最も単純な構文です。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema= "AnnotatedSchemaFile.xml"] >  
    <updg:before>  
        ...  
    </updg:before>  
    <updg:after>  
        ...  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 次に、これらの各ブロックの役割について説明します。  
  
 **\<before>**  
 レコード インスタンスの既存の状態 ("before 状態") を指定します。  
  
 **\<after>**  
 データの変更後の新しい状態を指定します。  
  
 **\<sync>**  
 含まれています、 **\<する前に >** と **\<後 >** ブロックします。 A **\<同期 >** ブロックの 1 つ以上のセットを含めることができます **\<する前に >** と **\<後 >** ブロックします。 1 つ以上のセットがある場合 **\<する前に >** と **\<後 >** ブロック、これらのブロック (空いる) 場合でも必要があります指定のペアとして。 さらに、アップデート グラムは複数のいずれかに **\<同期 >** ブロックします。 各 **\<同期 >** ブロックは、トランザクションの 1 つの単位 (です。 つまり、内のすべて、 **\<同期 >** ブロックが実行されるか、何も実行されます)。 複数指定する場合 **\<同期 >** アップデート グラムでは、1 つの障害でブロック **\<同期 >** ブロックには影響しません、 **\<同期>** ブロックします。  
  
 アップデート グラムによるを削除するかどうか、挿入、方法、またはレコード インスタンスを更新する方法の内容に依存、 **\<する前に >** と **\<後 >** ブロック。  
  
-   レコード インスタンスがでのみが表示された場合、 **\<する前に >** いない対応するインスタンスを使用してブロック、 **\<後 >** ブロック、アップデート グラムでは、削除操作を実行します。  
  
-   レコード インスタンスがでのみが表示された場合、 **\<後 >** いない対応するインスタンスを使用してブロック、 **\<する前に >** ブロックは、挿入操作。  
  
-   レコード インスタンスが表示される場合、 **\<する前に >** ブロック対応するインスタンスであり、 **\<後 >** ブロックは、更新操作。 この場合、アップデート グラムがで指定されている値にレコード インスタンスが更新、 **\<後 >** ブロックします。  
  
## <a name="specifying-a-mapping-schema-in-the-updategram"></a>アップデート グラムでマッピング スキーマを指定します。  
 アップデートグラムでは、暗黙的または明示的に、マッピング スキーマによって XML データを操作できます。つまり、マッピング スキーマを指定しても指定しなくてもアップデートグラムは動作します。マッピング スキーマは XSD と XDR の両方がサポートされています。 マッピング スキーマを指定しない場合、アップデート グラムで暗黙的なマッピング (既定のマッピング) ここで、内の各要素、 **\<する前に >** ブロックまたは **\<後 >** 。テーブルと各要素の子要素にマップされてブロックまたは属性は、データベース内の列にマップされます。 マッピング スキーマを明示的に指定する場合、アップデートグラムの要素と属性は、マッピング スキーマ内の要素と属性に一致する必要があります。  
  
### <a name="implicit-default-mapping"></a>暗黙的なマッピング (既定)  
 単純な更新を実行するアップデートグラムではほとんどの場合、マッピング スキーマは必要ありません。 この場合、アップデートグラムは既定のマッピング スキーマに従います。  
  
 次のアップデート グラムは、暗黙的なマッピングを示しています。 この例では、アップデートグラムによって新しい顧客が Sales.Customer テーブルに挿入されます。 このアップデート グラムは暗黙的なマッピングを使用するため、 \<Sales.Customer > 要素は Sales.Customer テーブルにマップされ、CustomerID および SalesPersonID 属性は Sales.Customer テーブル内の対応する列にマップします。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
</updg:before>  
<updg:after>  
    <Sales.Customer CustomerID="1" SalesPersonID="277" />  
    </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="explicit-mapping"></a>明示的なマッピング  
 XSD または XDR のいずれかのマッピング スキーマを指定した場合、アップデートグラムではそのスキーマによって、更新するデータベース テーブルと列が決定されます。  
  
 アップデートグラムにおいて、マッピング スキーマで指定される親子リレーションシップに基づいて複数のテーブルにレコードを挿入するなど、複雑な更新を実行する場合は、`mapping-schema` 属性でマッピング スキーマを明示的に指定する必要があります。アップデートグラムはこの属性で指定されたマッピング スキーマに対して実行されます。  
  
 アップデートグラムはテンプレートであり、アップデートグラム内でマッピング スキーマに指定するパスは、テンプレート ファイルの場所 (アップデートグラムが保存されている場所) に対する相対パスです。 詳細については、次を参照してください。[注釈付きマッピング スキーマを指定するアップデート グラムで&#40;SQLXML 4.0&#41;](specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)します。  
  
## <a name="element-centric-and-attribute-centric-mapping-in-updategrams"></a>アップデートグラムでの要素中心および属性中心のマッピング  
 アップデートグラムでマッピング スキーマが指定されていないときに使用される既定のマッピングでは、アップデートグラムの要素がテーブルにマップされ、要素中心マッピングの場合は子要素、属性中心マッピングの場合は属性が、それぞれ列にマップされます。  
  
### <a name="element-centric-mapping"></a>要素中心のマッピング  
 要素中心のアップデートグラムでは、要素に、要素のプロパティを表す子要素を含めます。 たとえば、次のアップデートグラムを参照してください。 **\<Person.Contact >** 要素が含まれています、  **\<FirstName >** と **\<LastName >** 子要素。 これらの子要素のプロパティになって、  **\<Person.Contact >** 要素。  
  
 アップデート グラムは暗黙的なマッピングを使用してこのアップデート グラムでは、マッピング スキーマを指定しないため、場所、  **\<Person.Contact >** 要素は Person.Contact テーブルにマップし、その子要素が firstname にマップし、LastName 列。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:after>  
    <Person.Contact>  
       <FirstName>Catherine</FirstName>  
       <LastName>Abel</LastName>  
    </Person.Contact>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="attribute-centric-mapping"></a>属性中心のマッピング  
 属性中心のマッピングでは、要素に属性を指定します。 たとえば、次のアップデートグラムでは属性中心のマッピングが使用されています。 この例で、  **\<Person.Contact >** 要素から成る、 **FirstName**と**LastName**属性。 これらの属性は、プロパティ、  **\<Person.Contact >** 要素。 前の例のようにこのアップデート グラムでスキーマを指定しないマッピング、暗黙的なマッピングにマップするには依存していますので、  **\<Person.Contact >** 要素は Person.Contact テーブルされ、要素の属性に、テーブル内の各列。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
    <Person.Contact FirstName="Catherine" LastName="Abel" />  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="using-both-element-centric-and-attribute-centric-mapping"></a>要素中心と属性中心の両方のマッピングの使用  
 次のアップデートグラムに示すように、要素中心と属性中心のマッピングは併用できます。 なお、  **\<Person.Contact >** 要素には属性と子要素の両方が含まれています。 また、このアップデートグラムは暗黙的なマッピングに従います。 つまり、 **FirstName**属性と **\<LastName >** 子要素は Person.Contact テーブルの対応する列にマップします。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
    <Person.Contact FirstName="Catherine" >  
       <LastName>Abel</LastName>  
    </Person.Contact>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="working-with-characters-valid-in-sql-server-but-not-valid-in-xml"></a>SQL Server で有効であり、XML で有効でない文字の取り扱い  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、テーブル名に空白を含めることができます。 ただし、このようなテーブル名は XML では有効でありません。  
  
 無効な文字をエンコードする[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]識別子がではありません有効な XML 識別子を使用して、' __xHHHH\_\_' HHHH は、ほとんどの文字の 4 桁の 16 進 ucs-2 コードのエンコードの値として。上位ビットから順。 このエンコード方式を使用して、空白文字は x0020 (4 桁 16 進数コード、空白文字の); に置き換えを取得しますしたがって、内のテーブル名 [Order Details] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] _x005B_Order_x0020_Details_x005D になります\_xml。  
  
 同様に、3 つの部分の要素の名前を指定する必要がありますに可能性があります\<[データベース]. [owner]。[テーブル] >。 角かっこ文字 ([と]) で XML が無効ですが、このとしてを指定する必要がありますので\<_x005B_database_x005D\_._x005B_owner_x005D\_._x005B_table_x005D\_> ここで、_x005B\_が、左角かっこ ([) と _x005D のエンコード\_右角かっこ (]) のエンコードです。  
  
## <a name="executing-updategrams"></a>アップデートグラムの実行  
 アップデートグラムはテンプレートであり、テンプレートのすべての処理メカニズムが適用されます。 SQLXML 4.0 では、アップデートグラムを次のいずれかの方法で実行できます。  
  
-   ADO コマンドに含めて送信する。  
  
-   OLE DB コマンドとして送信する。  
  
## <a name="see-also"></a>参照  
 [アップデート グラムのセキュリティに関する考慮事項&#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
