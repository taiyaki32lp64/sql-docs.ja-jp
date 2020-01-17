---
title: SQLXML 4.0 の DiffGram の概要
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotations [SQLXML]
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: 1902d67f-baf3-46e6-a36c-b24b5ba6f8ea
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3994a9d0bc863367edf5b1844772b94a63f19d4d
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257249"
---
# <a name="introduction-to-diffgrams-in-sqlxml-40"></a>SQLXML 4.0 の DiffGram の概要
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
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
 この要素の名前**Datainstance**は、このドキュメントで説明するために使用されます。 たとえば、.NET Framework のデータセットから DiffGram が生成された場合、この要素の名前としてデータセットの**name**プロパティの値が使用されます。 このブロックには、変更後のすべての関連データを指定します。変更されていないデータも指定できます。 DiffGram 処理ロジックでは、次のブロック内の要素は無視されます。このブロックは、次の**よう**な属性が指定されていません。  
  
 **\<diffgram:>前**  
 省略可能なブロックです。更新または削除する必要がある元のレコード インスタンス (要素) を指定します。 DiffGram によって変更 (更新または削除) されるすべてのデータベーステーブルは、 ** \<前の>** ブロックの最上位レベルの要素として表示される必要があります。  
  
 **\<diffgram: エラー>**  
 省略可能なブロックです。DiffGram の処理ロジックでは無視されます。  
  
## <a name="diffgram-annotations"></a>DiffGram の注釈  
 これらの注釈は、DiffGram 名前空間 **"urn: schema-01"** で定義されています。  
  
 **番号**  
 この属性は、 ** \<>** と** \<datainstance>** ブロックの前にある要素をペアにするために使用されます。  
  
 **hasChanges**  
 挿入操作または更新操作の場合、DiffGram では、**挿入**または**変更**された値を使用してこの属性を指定する必要があります。 この属性が存在しない場合、 ** \<>datainstance**内の対応する要素は処理ロジックによって無視され、更新は実行されません。 実際のサンプルについては、「 [DiffGram の例 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)」を参照してください。  
  
 **parentID**  
 この属性は、DiffGram の要素間の親子リレーションシップを指定するときに使用します。 この属性は、 \<before> ブロックにのみ表示されます。 この属性は更新の適用時に SQLXML で使用されます。 親子リレーションシップは、DiffGram の要素の処理順序を決定するために使用されます。  
  
## <a name="understanding-the-diffgram-processing-logic"></a>DiffGram の処理ロジックについて  
 DiffGram の処理ロジックでは、一定の規則に従い、挿入、更新、削除のうちどの操作であるかが判断されます。 次の表は、この規則についてまとめたものです。  
  
|Operation|説明|  
|---------------|-----------------|  
|挿入|DiffGram は、要素が** \<datainstance>** block に存在するが、対応** \<する before>** ブロックに含まれていない場合に挿入操作を示します。また、要素には、**次のよう**に、変更後の属性が指定されています (**diffgram gr: haschanges = inserted**)。 この場合、DiffGram は** \<datainstance>** block に指定されたレコードインスタンスをデータベースに挿入します。<br /><br /> 次の**よう**に、属性が指定されていない場合、要素は処理ロジックによって無視され、挿入は実行されません。 実際のサンプルについては、「 [DiffGram の例 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)」を参照してください。|  
|更新プログラム、更新|DiffGram は、 ** \<datainstance>** ブロックに対応する要素が存在\<する (つまり、両方の**要素の値**が同じ値である)> ブロックの前に要素がある場合に、 ** \<datainstance>** block 内の要素で変更された値を使用して、変更**後****の属性が**指定されている場合に、更新操作を示します。<br /><br /> Datainstance>block の要素で、**次のように変更**属性が指定されていない場合、処理ロジックによってエラーが返されます。 ** \<** 実際のサンプルについては、「 [DiffGram の例 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)」を参照してください。<br /><br /> [ ** \<前の>** ブロック] で [を使用する] が指定**されている場合、** **parentid**によって指定された要素の親子リレーションシップは、レコードの更新順序を決定するために使用されます。|  
|削除|DiffGram は、 ** \<** 要素が>ブロックの前に存在するが、対応する** \<datainstance>** ブロックには存在しない場合に、削除操作を示します。 この場合、DiffGram は、 ** \<before>** ブロックで指定されたレコードインスタンスをデータベースから削除します。 実際のサンプルについては、「 [DiffGram の例 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)」を参照してください。<br /><br /> [ ** \<前の>** ブロック] で [を使用する] が指定**されている場合、** **parentid**によって指定された要素の親子リレーションシップは、レコードの削除順序を決定するために使用されます。|  
  
> [!NOTE]  
>  DiffGram にパラメーターを渡すことはできません。  
  
  
