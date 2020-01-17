---
title: NULL 処理 (SQLXML)
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updg:nullvalue attribute
- updategrams [SQLXML], null values
- nullvalue attribute
- null values [SQLXML]
ms.assetid: 5e11eebb-d94e-4ce6-a6d0-870225706bc1
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b04802083aa505f963fc1a644d71799b37e13cf7
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75252416"
---
# <a name="null-handling-sqlxml-40"></a>NULL の取り扱い (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML 構文では、NULL は "存在しない" ことを表します。 (たとえば、属性または要素の値が NULL の場合、その属性または要素は XML ドキュメントに存在しません)。SQLXML [!INCLUDE[msCoName](../../../includes/msconame-md.md)]では、 **updg: nullvalue**属性を使用して、要素または属性値に NULL を指定できます。  
  
 たとえば、次のアップデートグラムでは、 **ContactID**が64である連絡先の**TITLE**値が NULL であることを確認し、 **title**値を "Mr" に更新します。 をお問い合わせください。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync updg:nullvalue="IsNULL"  >  
    <updg:before>  
       <Person.Contact ContactID="64" Title="IsNULL" />  
    </updg:before>  
    <updg:after>  
       <Person.Contact ContactID="64" Title="Mr." />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 パラメーターをアップデートグラムに渡すときには、パラメーター値として NULL を指定できます。 これを行うには、 ** \<updg: header>** block に**nullvalue**属性を指定します。 例については、「[アップデートグラムへのパラメーターの引き渡し &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/passing-parameters-to-updategrams-sqlxml-4-0.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQLXML 4.0&#41;&#40;アップデートグラムのセキュリティに関する考慮事項](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
