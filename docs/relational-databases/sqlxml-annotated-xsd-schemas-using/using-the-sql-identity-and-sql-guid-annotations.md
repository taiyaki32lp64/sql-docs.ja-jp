---
title: sql:identity 注釈と sql:guid 注釈の使用
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:guid
- annotated XSD schemas, IDENTITY-type columns
- annotated XSD schemas, GUID values
- DiffGrams [SQLXML], annotations
- identity annotation
- XSD schemas [SQLXML], GUID values
- GUIDs [SQLXML]
- guid annotation
- sql:identity
- IDENTITY-type column
- XSD schemas [SQLXML], IDENTITY-type columns
- updategrams [SQLXML], GUID values
ms.assetid: 7661dfd0-6573-4692-a8f1-3597adcd33c4
author: MightyPen
ms.author: genemi
ms.reviewer: ''
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 50483d7f6f84371b42bf0c79fbc74a1f85a65eab
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246819"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>sql:identity 注釈と sql:guid 注釈の使用
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース列にマップされている任意のノードの XSD スキーマで、 **sql: identity**注釈と**sql: guid**注釈を指定できます。 アップデートグラム形式では**updg: id**属性と**updg: guid**属性がサポートされていますが、DiffGram 形式ではサポートされていません。 **Updg: identity**属性は、id 型の列を更新するときの動作を定義します。 **Updg: guid**属性では、から[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] guid 値を取得し、アップデートグラムで使用できます。 詳細および作業サンプルについては、「 [XML アップデートグラムを使用したデータの挿入 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)」を参照してください。  
  
 **Sql: identity**注釈と**sql: guid**注釈によって、この機能が diffgram に拡張されます。  
  
 DiffGram を実行すると、DiffGram がアップデートグラムに変換された後、アップデートグラムが実行されます。 XSD スキーマで**sql: identity**注釈と**sql: guid**注釈を指定することで、実際にアップデートグラムの動作を定義します。 したがって、すべての注釈はアップデートグラムのコンテキストで記述します。 これらの注釈は DiffGram とアップデートグラムの両方で使用できますが、アップデートグラムには ID 値と GUID 値をより効率的に処理する機能が既に用意されています。  
  
 **Sql: identity**注釈と**sql: guid**注釈は、複合コンテンツ要素で定義できます。  
  
## <a name="sqlidentity-annotation"></a>sql:identity 注釈  
 ID 型のデータベース列にマップされている任意のノードの XSD スキーマで、 **sql: identity**注釈を指定できます。 この注釈に指定された値は、ID 型列の更新方法を定義します (アップデートグラムで提供されている値を使用して列を変更するか[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、値を無視することによって、この列に対して生成された値が使用されます)。  
  
 **Sql: identity**注釈には、次の2つの値を割り当てることができます。  
  
 ignore  
 アップデートグラムで列に提供される値を無視し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で生成される ID 値を使用します。  
  
 useValue  
 アップデートグラムで提供される値を使用して、IDENTITY 型列を更新します。 アップデートグラムでは、列が ID 値かどうかは確認されません。  
  
 アップデートグラムで ID 型の列の値を指定する場合は、スキーマで**sql: IDENTITY = "useValue"** を指定する必要があります。  
  
## <a name="sqlguid-annotation"></a>sql:guid 注釈  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で GUID 値を生成し、その値をアップデートグラムで使用できます。 Diffgram のコンテキストでは、 **sql: guid**注釈を使用して、SQL Server によって生成される guid 値を使用するか、その列のアップデートグラムで提供される値を使用するかを指定できます。  
  
 **Sql: guid**注釈には、次の2つの値を割り当てることができます。  
  
 generate  
 更新操作で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で生成される GUID を列に使用することを指定します。  
  
 useValue  
 アップデートグラムで提供される値を列に使用することを指定します。 これは、既定値です。  
  
  
