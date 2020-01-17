---
title: SQLXML 4.0 での xml データ型のサポート
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, xml data type support
- xml data type [SQL Server], SQLXML
ms.assetid: 9a6f5ad8-4a8f-4de7-ac17-81d5ccf78459
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4c56efd6c79b7ce7d74af621963f4b12e734d5f9
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75252169"
---
# <a name="xml-data-type-support-in-sqlxml-40"></a>SQLXML 4.0 での xml データ型のサポート
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  以降で[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]は[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、xml データ型を使用**した xml**型のデータがサポートされています。 このトピックでは、SQLXML 4.0 が**xml**データ型のインスタンスを認識し、それらのインスタンスのサポートを実装する方法について説明します。  
  
## <a name="working-with-xml-data-types"></a>xml データ型の使用  
 **Xml**データ型の列を実装する SQL テーブルを操作する方法の詳細については、次の例を参照してください。  
  
|タスク|例|トピック|  
|----------|-------------|-----------|  
|Xml ビューに**xml**列をマップして含める方法|"XML 要素を XML データ型の列にマップする"|[テーブルおよび列への XSD 要素と属性の既定のマッピング &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)|  
|アップデートグラムを使用して**xml**列にデータを挿入する方法|"XML データ型列にデータを挿入する"|[XML アップデートグラムを使用したデータの挿入 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)|  
|**Xml 列へ**の xml データの一括読み込み|"xml データ型の列に一括読み込みを行う"|[XML 一括読み込みの例 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)|  
  
## <a name="guidelines-and-limitations"></a>ガイドラインと制限  
  
-   **xsd: 任意の>を xml データ型を含む列にマップすることはできません。 \<** **** このシナリオの SQLXML でのサポートは、 **sql: overflow フィールド**注釈を通じて提供されます。 もう1つの回避策は、 **xml**データ型のフィールドを**xsd: anyType**の要素としてマップすることです。 この方法は、上の表の例 "XML 要素を XML データ型の列にマップする" に示されています。  
  
-   **Xml**データ型の列の内容に対する XPath クエリはサポートされていません。  
  
-   サポートされていない**xml**データ型の列 ( **sql: relationship**や**sql: key フィールド**など) を使用すると、SQLXML 4.0 を実装[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]する中間層コンポーネントによってトラップされないエラーが発生します。 これは、SQLXML で SQL 型の情報が必要とされないためです。 この動作は、BLOB やバイナリ型などその他のデータ型に対する SQLXML の動作と同様です。  
  
-   **Xml**列のマッピングは、XSD スキーマでのみサポートされています。 XDR スキーマでは、 **xml**列のマッピングはサポートされていません。  
  
-   SQLXML 4.0 は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で提供される XML 解析サポートに依存しています。 **Xml**列は、型指定された xml または型指定されていない xml としてマップできます。 どちらの場合も、SQLXML 4.0 で入力 XML は検証されません。  入力 XML が有効でないか、適切な形式でない場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から SQLXML にそのことがレポートされ、サーバーによって返された関連エラー情報がある場合はユーザーに伝達されます。  
  
-   SQLXML 4.0 は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で提供される DTD の制限付きサポートに依存しています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**xml**データ型のデータで内部 DTD を使用できるようにします。これを使用すると、既定値を指定したり、エンティティ参照を展開されたコンテンツに置き換えたりすることができます。 SQLXML では、サーバーに XML データが "そのまま" (内部 DTD を含めて) 渡されます。 ここで、サード パーティのツールを使用して DTD を XML スキーマ (XSD) ドキュメントに変換し、データをインライン XSD スキーマと共にデータベースに読み込むことができます。  
  
-   SQLXML 4.0 では、の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]動作に基づいて、XML 宣言の処理命令 (たとえば、) は保持されません。 Xml 宣言は xml パーサーへ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のディレクティブとして扱われ、その属性 (バージョン、エンコーディング、およびスタンドアロン) はデータが**xml**データ型に変換された後に失われます。 XML データは内部的に UCS-2 として保存されます。 XML インスタンス内のその他の処理命令はすべて保持されます。これらは**xml**列で許可され、SQLXML でサポートできます。  
  
## <a name="see-also"></a>参照  
 [XML データ &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
