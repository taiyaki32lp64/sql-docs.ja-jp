---
title: テンプレートのキャッシュ (SQLXML)
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- templates [SQLXML], caching
ms.assetid: 73e151c6-b24e-4422-a116-51e0846bc6f5
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ac28f41ca90b686dd469640abaaabe6855b07766
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246659"
---
# <a name="template-caching-sqlxml-40"></a>テンプレートのキャッシュ (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  テンプレートをキャッシュすると、パフォーマンスが大幅に向上します。 テンプレートのキャッシュを設定している場合、テンプレートは初回実行時にメモリに残るので、 以降のテンプレート実行でパフォーマンスが向上します。  
  
 テンプレートのキャッシュ サイズは、レジストリに次のキーを追加することで設定できます。  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\TemplateCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 テンプレートのサイズは、使用できるメモリと使用しているテンプレートの数に基づいて設定します。 **TemplateCacheSize**の既定値は31です。 テンプレートのアクセスが遅い場合はキャッシュ サイズを増やし、メモリが少ない場合はキャッシュ サイズを減らします。  
  
 パフォーマンスを向上させるために、通常使用するテンプレートの数より**TemplateCacheSize**を設定することをお勧めします。 **TemlateCacheSize**がテンプレートの数より少ない場合、テンプレートの数が増えるにつれてパフォーマンスが低下します。 **TemplateCacheSize**は最大128に設定できます。  
  
 キャッシュされたテンプレートが使用されるときには、毎回テンプレート ファイルの変更回数がチェックされ、更新が必要がどうかが決定されます。 これは、ディスク コピーがキャッシュ コピーより新しいためです。  
  
> [!NOTE]  
>  テンプレートのパラメーターとコマンド プロパティはキャッシュされません。  
  
## <a name="see-also"></a>参照  
 [スキーマキャッシュ &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)   
 [XSL キャッシュ &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
  
  
