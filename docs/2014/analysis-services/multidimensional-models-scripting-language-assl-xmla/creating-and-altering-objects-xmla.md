---
title: 作成して、オブジェクト (XMLA) の変更 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- objects [XML for Analysis]
- subordinate objects [XML for Analysis]
- XML for Analysis, objects
- modifying objects
- removing objects
- deleting objects
- XMLA, objects
ms.assetid: a2080867-e130-440c-92eb-f768869f34a8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3dcc6eedc97b3d476d79420b4e067883e17f03d2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62702299"
---
# <a name="creating-and-altering-objects-xmla"></a>オブジェクトの作成と変更 (XMLA)
  主要なオブジェクトは、個別に作成、変更、削除することができます。 主要なオブジェクトには以下のオブジェクトが含まれます。  
  
-   サーバー  
  
-   データベース  
  
-   ディメンション  
  
-   キューブ  
  
-   メジャー グループ  
  
-   [メジャー グループ]  
  
-   パースペクティブ  
  
-   [マイニング モデル]  
  
-   ロール  
  
-   サーバーまたはデータベースに関連付けられているコマンド  
  
-   データ ソース  
  
 使用する、[作成](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)のインスタンスで、主要なオブジェクトを作成するコマンド[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、および[Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)インスタンス上の既存の主要なオブジェクトを変更するコマンド。 使用して両方のコマンドを実行、 [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)メソッド。  
  
## <a name="creating-objects"></a>オブジェクトを作成します。  
 `Create` メソッドを使用してオブジェクトを作成する場合は、まず、作成する [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトを含む親オブジェクトを識別する必要があります。 内のオブジェクト参照を提供することで、親オブジェクトを識別する、 [ParentObject](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)のプロパティ、`Create`コマンド。 それぞれのオブジェクト参照には、`Create` コマンドの対象の親オブジェクトを一意に識別するのに必要なオブジェクト識別子が含まれます。 オブジェクト参照の詳細については、次を参照してください。[を識別するオブジェクトの定義および&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)します。  
  
 たとえば、キューブに新しいメジャー グループを作成するには、キューブへのオブジェクト参照を指定する必要があります。 `ParentObject` プロパティでのキューブへのオブジェクト参照には、データベース識別子とキューブ識別子の両方が含まれます。別のデータベースでも同じキューブ識別子が使用されている可能性があるためです。  
  
 [ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla)要素には作成する主要なオブジェクトを定義する Analysis Services スクリプト言語 (ASSL) 要素が含まれています。 ASSL の詳細については、次を参照してください。 [Analysis Services スクリプト言語を使用した開発&#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)します。  
  
 `AllowOverwrite` コマンドの `Create` 属性を true に設定すると、指定された識別子を持つ既存の主要なオブジェクトを上書きできます。 そうしない場合、親オブジェクト内に指定された識別子を持つ主要なオブジェクトが既に存在するときに、エラーが発生します。  
  
 詳細については、`Create`コマンドを参照してください[要素の作成&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)します。  
  
### <a name="creating-session-objects"></a>セッション オブジェクトの作成  
 セッション オブジェクトは一時オブジェクトであり、クライアント アプリケーションで使用される明示的または暗黙的なセッションでのみ使用でき、セッションの終了時には削除されます。 セッション オブジェクトを作成するには設定して、`Scope`の属性、`Create`コマンドを*セッション*します。  
  
> [!NOTE]  
>  使用する場合、*セッション*を設定する、`ObjectDefinition`要素に含めることができますのみ[ディメンション](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl)、[キューブ](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl)、または[MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) ASSL要素。  
  
## <a name="altering-objects"></a>オブジェクトの変更  
 使用してオブジェクトを変更するときに、`Alter`メソッド、オブジェクト参照を提供することによって変更されるオブジェクト最初に識別する必要があります、[オブジェクト](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)のプロパティ、`Alter`コマンド。 それぞれのオブジェクト参照には、`Alter` コマンドの対象のオブジェクトを一意に識別するのに必要なオブジェクト識別子が含まれます。 オブジェクト参照の詳細については、次を参照してください。[を識別するオブジェクトの定義および&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)します。  
  
 たとえば、キューブの構造を変更するためには、キューブへのオブジェクト参照を指定する必要があります。 `Object` プロパティでのキューブへのオブジェクト参照には、データベース識別子とキューブ識別子の両方が含まれます。別のデータベースでも同じキューブ識別子が使用されている可能性があるためです。  
  
 `ObjectDefinition` 要素には、変更する主要なオブジェクトを定義する ASSL 要素が含まれます。 ASSL の詳細については、次を参照してください。 [Analysis Services スクリプト言語を使用した開発&#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)します。  
  
 `AllowCreate` コマンドの `Alter` 属性を true に設定すると、指定された主要なオブジェクトが存在しない場合に、それを作成することができます。 そうしない場合、指定された主要なオブジェクトが存在していないときに、エラーが発生します。  
  
### <a name="using-the-objectexpansion-attribute"></a>ObjectExpansion 属性の使用  
 設定することができます、主要なオブジェクトのプロパティのみを変更し、主要なオブジェクトに格納される副次オブジェクトを再定義しない場合、`ObjectExpansion`の属性、`Alter`コマンドを*objectproperties です*します。 `ObjectDefinition` プロパティには、主要なオブジェクトのプロパティに対応する要素だけを含めればよく、その場合 `Alter` コマンドは主要なオブジェクトに関連付けられている副次オブジェクトに変更を加えません。  
  
 設定する必要があります、主要なオブジェクトに対する副次オブジェクトを再定義する、`ObjectExpansion`属性を*ExpandFull*オブジェクトの定義は、主要なオブジェクトに含まれるすべての副次オブジェクトを含める必要があります。 `ObjectDefinition` コマンドの `Alter` プロパティに、主要なオブジェクトに格納される副次オブジェクトが明示的に含められていない場合、含まれない副次オブジェクトは削除されます。  
  
### <a name="altering-session-objects"></a>セッション オブジェクトの変更  
 によって作成されたセッション オブジェクトを変更する、`Create`コマンド、設定、`Scope`の属性、`Alter`コマンドを*セッション*します。  
  
> [!NOTE]  
>  使用する場合、*セッション*を設定する、`ObjectDefinition`要素に含めることができますのみ[ディメンション](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl)、[キューブ](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl)、または[MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) ASSL要素。  
  
## <a name="creating-or-altering-subordinate-objects"></a>下位オブジェクトの作成または変更  
 `Create` または `Alter` コマンドで作成または変更できるのは最上位の主要なオブジェクトだけですが、作成中または変更中の主要なオブジェクトには、囲んでいる `ObjectDefinition` プロパティの中に、従属する他の主要なオブジェクトや副次オブジェクトの定義を含めることができます。 たとえば、キューブを定義する場合、`ParentObject` で親データベースを指定します。`ObjectDefinition` でのキューブ定義にはキューブのメジャー グループを定義でき、さらにメジャー グループ内ではそれぞれのメジャー グループのパーティションを定義できます。 副次オブジェクトは、それを格納する主要なオブジェクトの中でのみ定義できます。 メジャーおよびマイナー オブジェクトの詳細については、次を参照してください。[データベース オブジェクト&#40;Analysis Services - 多次元データ&#41;](../multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)します。  
  
## <a name="examples"></a>使用例  
  
### <a name="description"></a>説明  
 次の例を参照するリレーショナル データ ソースの作成、[!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]サンプル[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。  
  
### <a name="code"></a>コード  
  
```  
<Create xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <ParentObject>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    </ParentObject>  
    <ObjectDefinition>  
        <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RelationalDataSource">  
            <ID>AdventureWorksDW2012</ID>  
            <Name>AdventureWorksDW2012</Name>  
            <ConnectionString>Data Source=localhost;Initial Catalog=AdventureWorksDW2008R2;Integrated Security=True</ConnectionString>  
            <ImpersonationInfo>  
                <ImpersonationMode>ImpersonateServiceAccount</ImpersonationMode>  
            </ImpersonationInfo>  
            <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
            <Timeout>PT0S</Timeout>  
        </DataSource>  
    </ObjectDefinition>  
</Create>  
```  
  
### <a name="description"></a>説明  
 次の例では、前の例で作成されたリレーショナル データ ソースを変更して、データ ソースのクエリ タイムアウトを 30 秒に設定します。  
  
### <a name="code"></a>コード  
  
```  
<Alter ObjectExpansion="ObjectProperties" xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DataSourceID>AdventureWorksDW2012</DataSourceID>  
    </Object>  
    <ObjectDefinition>  
        <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RelationalDataSource">  
            <ID>AdventureWorksDW2012</ID>  
            <Name>AdventureWorksDW2012</Name>  
            <ConnectionString>Data Source=fr-dwk-02;Initial Catalog=AdventureWorksDW2008R2;Integrated Security=True</ConnectionString>  
            <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
            <Timeout>PT30S</Timeout>  
        </DataSource>  
    </ObjectDefinition>  
</Alter>  
```  
  
### <a name="comments"></a>コメント  
 `ObjectExpansion`の属性、`Alter`コマンドに設定された*objectproperties です*します。 この設定では、 [ImpersonationInfo](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl)要素で定義されているデータ ソースから除外する、補助オブジェクトを使用して`ObjectDefinition`します。 そのため、そのデータ ソースに関する権限借用情報は、最初の例で指定したとおりにサービス アカウントに対して設定されたままになります。  
  
## <a name="see-also"></a>参照  
 [Execute メソッド&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)   
 [Analysis Services スクリプト言語 (ASSL) での開発](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Analysis Services での XMLA による開発](developing-with-xmla-in-analysis-services.md)  
  
  
