---
title: SqlXmlCommand オブジェクト (SQLXML)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- void ExecuteNonQuery() method
- namespaces property
- Stream ExecuteStream() method
- CommandType property
- RootTag property
- OutputEncoding property
- XmlReader ExecuteXmlReader() method
- Managed Classes [SQLXML], SqlXmlCommand object
- SQLXML Managed Classes, SqlXmlCommand object
- Base Path property
- void ClearParameters() method
- public void ExecuteToStream(Stream outputStream) method
- SqlXmlCommand object
- CommandText property
- XslPath property
- SchemaPath property
- SqlXmlParameter CreateParameter() method
- ClientSideXML property
- CommandStream property
ms.assetid: c1f9e0bb-a89d-4d6a-a96e-289ef516a3a6
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: eb307599c48c72697f696e78eb7ed988dc03ca37
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75252653"
---
# <a name="sqlxml-managed-classes---sqlxmlcommand-object"></a>SQLXML マネージド クラス - SqlXmlCommand オブジェクト
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  SqlXmlCommand オブジェクトのコンストラクターを次に示します。  
  
```  
public SqlXmlCommand(string cnString)  
```  
  
 ここ`cnString`で、は、サーバー、データベース、およびログイン情報を識別する ADO または OLEDB の接続文字列です`Provider=SQLOLEDB; Server=(local); database=AdventureWorks; Integrated Security=SSPI"`(例:)。  
  
 接続文字列では、`Provider` に SQLOLEDB を指定する必要があります。プロバイダーの文字列に `Data Provider` は使用できません。  
  
 実際のサンプルについては、「 [SQL クエリの実行 &#40;SQLXML マネージクラス&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-sqlxml-managed-classes.md)」を参照してください。  
  
## <a name="methods"></a>メソッド  
 コマンドを実行するための次のメソッドを含む、複数のメソッドがサポートされています。  
  
 void ExecuteNonQuery ()  
 コマンドを実行しますが、何も返しません。 このメソッドは、クエリ以外のコマンド (何も返さないコマンド) を実行する場合に便利です。 たとえば、アップデートグラムや DiffGram でレコードを更新し、何も返さない場合に使用できます。  
  
 Stream ExecuteStream ()  
 新しいストリームオブジェクトを返します。 このメソッドは、クエリ結果を新しいストリームで返す場合に便利です。 実際のサンプルについては、「 [SQL クエリの実行 &#40;SQLXML マネージクラス&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-sqlxml-managed-classes.md)」を参照してください。  
  
 public void ExecuteToStream (Stream outputStream)  
 クエリ結果を既存のストリームに書き込みます。 このメソッドは、結果を追加する必要があるストリームがある場合に便利です (たとえば、クエリ結果が Httpresponse.cache に書き込まれるようにする場合など)。 実際のサンプルについては、「 [SQL クエリの実行 &#40;SQLXML マネージクラス&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-sqlxml-managed-classes.md)」を参照してください。  
  
 XmlReader ExecuteXmlReader ()  
 XmlReader オブジェクトを返します。 このメソッドを使用すると、XmlReader オブジェクトのデータを直接操作したり、System.xml の chainable アーキテクチャにプラグインしたりすることができます。 詳細については、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework のドキュメントを参照してください。 実際のサンプルについては、「 [ExecuteXMLReader メソッドを使用した SQL クエリの実行](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-by-using-the-executexmlreader-method.md)」を参照してください。  
  
 また、次の追加メソッドもサポートしています。  
  
 SqlXmlParameter CreateParameter ()  
 SqlXmlParameter オブジェクトを作成します。 このオブジェクトの*名前*と*値*のパラメーターの値を設定できます。 このメソッドは、コマンドにパラメーターを渡す場合に便利です。 実際のサンプルについては、「 [SQL クエリの実行 &#40;SQLXML マネージクラス&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-sqlxml-managed-classes.md)」を参照してください。  
  
 void ClearParameters ()  
 指定したコマンド オブジェクトに作成されたパラメーターを消去します。 このメソッドは、同一のコマンド オブジェクトで複数のクエリを実行する場合に便利です。  
  
## <a name="properties"></a>プロパティ  
 SqlXmlCommand オブジェクトは、次のプロパティもサポートしています。  
  
 ClientSideXml  
 True に設定すると、サーバーではなくクライアント側で、行セットが XML に変換されます。 このプロパティは、パフォーマンスの負荷を中間層に移す場合に便利です。 このプロパティを使用すると、既存のストアド プロシージャを FOR XML でラップして XML に出力することもできます。  
  
 SchemaPath  
 マッピング スキーマの名前とディレクトリ パス (C:\x\y\MySchema.xml など) を指定します。 このプロパティは、XPath クエリにマッピング スキーマを指定するときに便利です。 パスは、相対パスまたは絶対パスで指定できます。 パスが相対パスの場合は、ベースパスに指定されているベースパスを使用して相対パスが解決されます。 基本パスが指定されていない場合、相対パスは現在のディレクトリからのパスになります。 実際のサンプルについては、「 [.Net 環境での SQLXML 機能へのアクセス](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md)」を参照してください。  
  
 XslPath  
 XSL ファイルの名前とディレクトリ パスを指定します。 パスは、相対パスまたは絶対パスで指定できます。 パスが相対パスの場合は、ベースパスに指定されているベースパスを使用して相対パスが解決されます。 基本パスが指定されていない場合、相対パスは現在のディレクトリからのパスになります。 実際のサンプルについては、「 [&#40;SQLXML マネージクラス&#41;の XSL 変換の適用](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/applying-an-xsl-transformation-sqlxml-managed-classes.md)」を参照してください。  
  
 基本パス  
 基本パス (ディレクトリ パス) を指定します。 このプロパティは、(XslPath プロパティを使用して) XSL ファイルに指定されている相対パス、マッピングスキーマファイル (SchemaPath プロパティを使用)、または XML テンプレート内の外部スキーマ参照 (**マッピングスキーマ**属性を使用して指定) を解決するのに役立ちます。  
  
 OutputEncoding  
 コマンドを実行したときに返されるストリームのエンコードを指定します。 このプロパティは、返されるストリームに特定のエンコードを要求する場合に便利です。 一般的に使用されるエンコードには、UTF-8、ANSI、Unicode などがあります。 既定のエンコードは UTF-8 です。  
  
 名前空間  
 名前空間を使用する XPath クエリの実行を有効にします。 名前空間を使用した XPath クエリの詳細については、「[名前空間を使用した Xpath クエリの実行 &#40;SQLXML マネージクラス&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-xpath-queries-with-namespaces-sqlxml-managed-classes.md)」を参照してください。 実際のサンプルについては、「 [&#40;SQLXML マネージクラス&#41;の XPath クエリの実行](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-xpath-queries-sqlxml-managed-classes.md)」を参照してください。  
  
 RootTag  
 コマンドを実行して生成される XML の、単一のルート要素を指定します。 有効な XML ドキュメントには、単一のルートレベルのタグが必要です。 このプロパティでは、コマンドを実行して単一の最上位要素のない XML フラグメントが生成された場合に、返される XML のルート要素を指定できます。 実際のサンプルについては、「 [&#40;SQLXML マネージクラス&#41;の XSL 変換の適用](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/applying-an-xsl-transformation-sqlxml-managed-classes.md)」を参照してください。  
  
 CommandText  
 コマンドのテキストを指定します。 このプロパティは、実行するコマンドのテキストを指定するときに使用します。 実際のサンプルについては、「 [SQL クエリの実行 &#40;SQLXML マネージクラス&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-sqlxml-managed-classes.md)」を参照してください。  
  
 CommandStream  
 コマンド ストリームを指定します。 このプロパティは、XML テンプレートなどのファイルからコマンドを実行する場合に便利です。 CommandStream を使用している場合は、 **"Template"**、 **"アップデートグラム"** 、および **"DiffGram" の CommandType**値のみがサポートされます。 実際のサンプルについては、「 [CommandStream プロパティを使用したテンプレートファイルの実行](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-template-files-by-using-the-commandstream-property.md)」を参照してください。  
  
 CommandType  
 コマンドの種類を指定します。 このプロパティは、実行するコマンドの種類を指定するときに使用します。 コマンドの種類の値を、次の表に示します。 実際のサンプルについては、「 [.Net 環境での SQLXML 機能へのアクセス](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md)」を参照してください。  
  
|値|説明|  
|-----------|-----------------|  
|SqlXmlCommandType .Sql|SQL コマンド (`SELECT * FROM Employees FOR XML AUTO` など) を実行します。|  
|SqlXmlCommandType. XPath|XPath コマンド (`Employees[@EmployeeID=1]` など) を実行します。|  
|SqlXmlCommandType. テンプレート|XML テンプレートを実行します。|  
|SqlXmlCommandType. TemplateFile|指定したパスにあるテンプレート ファイルを実行します。|  
|SqlXmlCommandType. アップデートグラム|アップデートグラムを実行します。|  
|SqlXmlCommandType. Diffgram|DiffGram を実行します。|  
  
## <a name="see-also"></a>参照  
 [SqlXmlParameter オブジェクト &#40;SQLXML マネージクラス&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmlparameter-object.md)   
 [SqlXmlAdapter オブジェクト &#40;SQLXML マネージクラス&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmladapter-object.md)  
  
  
