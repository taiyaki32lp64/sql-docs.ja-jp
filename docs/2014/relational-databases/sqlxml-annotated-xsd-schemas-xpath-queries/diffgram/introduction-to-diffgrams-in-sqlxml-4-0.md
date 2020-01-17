---
title: SQLXML 4.0 で Diffgram の概要 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotations [SQLXML]
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: 1902d67f-baf3-46e6-a36c-b24b5ba6f8ea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 48b54c71aff65c72af1f69554a6e049958044c31
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013015"
---
# <a name="introduction-to-diffgrams-in-sqlxml-40"></a>SQLXML 4.0 の DiffGram の概要
  ここでは、DiffGram の概要を説明します。  
  
## <a name="diffgram-format"></a>DiffGram の書式  
 一般的な DiffGram の書式は次のとおりです。  
  
```  
<?xml version="1.0"?>  
<diffgr:diffgram   
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"  
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1"  
         xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
   <DataInstance>  
      ...  
   </DataInstance>  
   [<diffgr:before>  
        ...  
   </diffgr:before>]  
  
   [<diffgr:errors>  
        ...  
   </diffgr:errors>]  
</diffgr:diffgram>  
```  
  
 DiffGram の書式は次のブロックで構成されています。  
  
 **\<DataInstance>**  
 この要素の名前**DataInstance**はこのドキュメントでは説明目的で使用します。 値である .NET Framework におけるデータセットから DiffGram が生成された場合など、**名前**データセットのプロパティは、この要素の名前として使用ができます。 このブロックには、変更後のすべての関連データを指定します。変更されていないデータも指定できます。 DiffGram の処理ロジックをこのブロック内の要素を無視する、 **diffgr:hasChanges**属性が指定されていません。  
  
 **\<diffgr:before>**  
 省略可能なブロックです。更新または削除する必要がある元のレコード インスタンス (要素) を指定します。 (更新または削除) に変更されるすべてのデータベース テーブル、DiffGram での最上位要素として表示する必要があります、 **\<する前に >** ブロックします。  
  
 **\<diffgr:errors>**  
 省略可能なブロックです。DiffGram の処理ロジックでは無視されます。  
  
## <a name="diffgram-annotations"></a>DiffGram の注釈  
 これらの注釈は DiffGram 名前空間で定義されている **"urn:schemas-microsoft-com:xml-diffgram-01"** :  
  
 **id**  
 この属性を使用して要素のペアを **\<する前に >** と **\<DataInstance >** ブロックします。  
  
 **hasChanges**  
 挿入または更新操作は、DiffGram は、値は、この属性を指定する必要があります**挿入**または**変更**します。 この属性が存在しない場合の対応する要素、  **\<DataInstance >** 処理では無視されますロジックや更新が実行されます。 実際のサンプルを参照してください。 [DiffGram の例&#40;SQLXML 4.0&#41;](diffgram-examples-sqlxml-4-0.md)します。  
  
 **parentID**  
 この属性は、DiffGram の要素間の親子リレーションシップを指定するときに使用します。 この属性があるだけで、\<する前に > ブロックします。 この属性は更新の適用時に SQLXML で使用されます。 親子リレーションシップは、DiffGram の要素の処理順序を決定するために使用されます。  
  
## <a name="understanding-the-diffgram-processing-logic"></a>DiffGram の処理ロジックについて  
 DiffGram の処理ロジックでは、一定の規則に従い、挿入、更新、削除のうちどの操作であるかが判断されます。 次の表は、この規則についてまとめたものです。  
  
|操作|説明|  
|---------------|-----------------|  
|Insert|要素が表示されたら、DiffGram は挿入操作を示します、 **\<DataInstance >** ブロックが、対応する **\<する前に >** ブロック、および、 **diffgr:hasChanges**属性が指定されて (**diffgr:hasChanges = 挿入**) 要素にします。 ここでは、DiffGram がで指定されたレコード インスタンスを挿入、  **\<DataInstance >** をデータベースにブロックします。<br /><br /> 場合、 **diffgr:hasChanges**属性が指定されていない、処理ロジックで、要素は無視され、挿入は実行されません。 実際のサンプルを参照してください。 [DiffGram の例&#40;SQLXML 4.0&#41;](diffgram-examples-sqlxml-4-0.md)します。|  
|更新|内の要素がある場合に、DiffGram は更新操作を示します、\<する前に > が対応する要素が存在するブロック、  **\<DataInstance >** ブロック (つまり、両方の要素がある、 **diffgr:id**同じ値を持つ属性) と**diffgr:hasChanges**属性が値を指定**変更**内の要素に対して、 **\<DataInstance >** ブロックします。<br /><br /> 場合、 **diffgr:hasChanges**属性が要素で指定されていない、  **\<DataInstance >** ブロック、処理ロジックでエラーが返されます。 実際のサンプルを参照してください。 [DiffGram の例&#40;SQLXML 4.0&#41;](diffgram-examples-sqlxml-4-0.md)します。<br /><br /> 場合**diffgr:parentID**で指定された、 **\<する前に >** ブロックで指定されている要素の親子リレーションシップ**parentID**で使用されますレコードが更新される順序が決定されます。|  
|DELETE|要素が表示されたら、DiffGram を削除操作を示します、 **\<する前に >** ブロックが、対応する **\<DataInstance >** ブロックします。 この場合、DiffGram はで指定されたレコード インスタンスを削除します。、 **\<する前に >** データベースからのブロック。 実際のサンプルを参照してください。 [DiffGram の例&#40;SQLXML 4.0&#41;](diffgram-examples-sqlxml-4-0.md)します。<br /><br /> 場合**diffgr:parentID**で指定された、 **\<する前に >** ブロックで指定されている要素の親子リレーションシップ**parentID**で使用されますレコードが削除される順序が決定されます。|  
  
> [!NOTE]  
>  DiffGram にパラメーターを渡すことはできません。  
  
  
