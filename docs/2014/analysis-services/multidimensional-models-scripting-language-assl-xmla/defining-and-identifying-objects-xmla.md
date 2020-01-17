---
title: 定義と識別 (XMLA) のオブジェクト |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- objects [XML for Analysis]
- identifying objects [XML for Analysis]
- XML for Analysis, objects
- object references [XML for Analysis]
- object identifiers [XML for Analysis]
- object definitions [XML for Analysis]
- XMLA, objects
ms.assetid: 43b65f6d-0123-4556-81f0-c7a0b84361e5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ad6c8de47577eccd7797517c8080957d7afe1abd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62727559"
---
# <a name="defining-and-identifying-objects-xmla"></a>オブジェクトの定義と識別 (XMLA)
  XML for Analysis (XMLA) コマンド内では、オブジェクト識別子とオブジェクト参照を使用してオブジェクトが識別されます。また、XMLA コマンド内では、Analysis Services Scripting Language (ASSL) 要素を使用してオブジェクトが定義されます。  
  
## <a name="object-identifiers"></a>オブジェクト識別子  
 インスタンスで定義されているオブジェクトの一意の識別子を使用して、オブジェクトが識別される[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]します。 オブジェクト識別子は明示的に指定されるか、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] でオブジェクトが作成されるときに [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスによって決定されます。 使用することができます、 [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)オブジェクト識別子を取得するメソッドを後続`Discover`または[Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)メソッドの呼び出し。  
  
## <a name="object-references"></a>オブジェクトの参照  
 いくつかの XMLA コマンドなど[削除](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/delete-element-xmla)または[プロセス](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)、オブジェクト参照を使用して、明確な方法でオブジェクトを参照してください。 オブジェクト参照には、コマンドの実行対象となるオブジェクトのオブジェクト識別子と、そのオブジェクトの先祖のオブジェクト識別子が含まれます。 たとえば、パーティションのオブジェクト参照には、パーティションのオブジェクト識別子と、そのパーティションの親メジャー グループ、キューブ、およびデータベースのオブジェクト識別子が含まれます。  
  
## <a name="object-definitions"></a>オブジェクト定義  
 [作成](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)と[Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla) xmla コマンドを作成または変更、それぞれ、オブジェクトで、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]インスタンス。 これらのオブジェクトの定義がによって表される、 [ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla) ASSL の要素を含む要素。 オブジェクト識別子は明示的に指定するすべての主要なと多くの副次オブジェクトを使用して、 [ID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla)要素。 `ID` 要素が使用されない場合、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスによって一意の識別子が提供されます。その際の名前付け規則は識別対象のオブジェクトによって異なります。 使用する方法についての詳細、`Create`と`Alter`、オブジェクトを定義するためのコマンドを参照してください[を変更するオブジェクトの作成と&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)します。  
  
## <a name="see-also"></a>参照  
 [要素をオブジェクト&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [ParentObject 要素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [Source 要素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)   
 [Target 要素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/target-element-xmla)   
 [Analysis Services での XMLA による開発](developing-with-xmla-in-analysis-services.md)  
  
  
