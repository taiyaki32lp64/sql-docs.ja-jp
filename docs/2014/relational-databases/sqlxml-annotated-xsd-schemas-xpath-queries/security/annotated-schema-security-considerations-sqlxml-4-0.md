---
title: スキーマのセキュリティに関する考慮事項 (SQLXML 4.0) の注釈を付ける |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping schema [SQLXML], security
- annotated XDR schemas, security
- XDR schemas [SQLXML], security
- annotations [SQLXML]
- annotated XSD schemas, security
- SQLXML, annotated XSD schemas
- SQLXML, annotated XDR schemas
- security [SQLXML], annotated schemas
- XSD schemas [SQLXML], security
ms.assetid: 7d7e44dc-b6d3-4e0f-95c7-8f99930c94f2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 635c5c433f583ecad9f8dda1e35e4c981742212e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010575"
---
# <a name="annotated-schema-security-considerations-sqlxml-40"></a>注釈付きスキーマのセキュリティに関する注意点 (SQLXML 4.0)
  次に、注釈付きスキーマを使用する場合のセキュリティに関するガイドラインを示します。  
  
-   マッピング スキーマでは既定のマッピングを使用しないようにしてください。 既定のマッピングでは、要素名がテーブル名にマップされ、属性名が列名にマップされるため、結果の XML ドキュメントではデータベース情報 (テーブル名と列名) が公開されることになります。 データベースのテーブルと列の情報には XML ドキュメントを表示できるユーザーであればだれでもアクセスできるので、これにより、セキュリティが脅かされる可能性があります。 この危険を避けるため、スキーマで任意の要素名と属性名を指定し、注釈を使用してそれらを明示的にテーブルと列にマップするようにしてください。 詳細については、XSD スキーマを作成するときに既定のマッピングを使用して、次を参照してください。[既定のマッピングの XSD 要素および属性からテーブルと列&#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)します。  
  
-   注釈を使用して指定する明示的なマッピングでは、データベース情報 (テーブル名、列名など) が公開されます。 このため、これらのスキーマはだれもがアクセスできる場所に置かないことをお勧めします。  
  
-   `max-depth` 注釈が大きな値に設定されており、再帰が行われるマッピング スキーマに対するクエリなど、実行に時間がかかるクエリがあります。 必要に応じて、秒単位でのコマンド タイムアウト プロパティを設定してタイムアウト制限を指定することができます。 以下に例を示します。  
  
    ```  
    cn.Open "Provider=SQLOLEDB;Server=localhost;Database=tempdb;Integrated Security=SSPI;Command Properties='Command Time Out=50';"  
    ```  
  
## <a name="see-also"></a>参照  
 [SQLXML 4.0 の注釈付き XSD スキーマ](../../sqlxml/annotated-xsd-schemas/annotated-xsd-schemas-in-sqlxml-4-0.md)  
  
  
