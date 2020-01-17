---
title: SqlXmlCommand オブジェクト (SQLXML マネージ クラス) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: d002208a83b58a4c8547bc6ce85db073ced70974
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010743"
---
# <a name="sqlxmlcommand-object-sqlxml-managed-classes"></a>SqlXmlCommand オブジェクト (SQLXML マネージド クラス)
  SqlXmlCommand オブジェクトのコンス トラクターです。  
  
```  
public SqlXmlCommand(string cnString)  
```  
  
 場所`cnString`は、サーバー、データベース、およびログイン情報を識別する ADO または OLEDB 接続文字列-たとえば、 `Provider=SQLOLEDB; Server=(local); database=AdventureWorks; Integrated Security=SSPI"`。  
  
 接続文字列では、`Provider` に SQLOLEDB を指定する必要があります。プロバイダーの文字列に `Data Provider` は使用できません。  
  
 実際のサンプルでは、次を参照してください。 [SQL クエリの実行&#40;SQLXML マネージ クラス&#41;](sqlxml-4-0-net-framework-support-managed-classes.md)します。  
  
## <a name="methods"></a>メソッド  
 TheSqlXmlCommand オブジェクトには、次のコマンドを実行する方法を含め、いくつかの方法がサポートされています。  
  
 void ExecuteNonQuery()  
 コマンドを実行しますが、何も返しません。 このメソッドは、クエリ以外のコマンド (何も返さないコマンド) を実行する場合に便利です。 たとえば、アップデートグラムや DiffGram でレコードを更新し、何も返さない場合に使用できます。  
  
 Stream ExecuteStream()  
 新しい Stream オブジェクトを返します。 このメソッドは、クエリ結果を新しいストリームで返す場合に便利です。 実際のサンプルでは、次を参照してください。 [SQL クエリの実行&#40;SQLXML マネージ クラス&#41;](sqlxml-4-0-net-framework-support-managed-classes.md)します。  
  
 public void ExecuteToStream (Stream outputStream)  
 クエリ結果を既存のストリームに書き込みます。 このメソッドは、結果を (たとえば、クエリ結果が、System.Web.HttpResponse.OutputStream に書き込まれます) を追加する必要があるストリームがある場合に便利です。 実際のサンプルでは、次を参照してください。 [SQL クエリの実行&#40;SQLXML マネージ クラス&#41;](sqlxml-4-0-net-framework-support-managed-classes.md)します。  
  
 XmlReader ExecuteXmlReader()  
 XmlReader オブジェクトを返します。 このメソッドは、XmlReader オブジェクト内のデータを直接操作するか、System.Xml のチェーン可能なアーキテクチャ、プラグインを使用できます。 詳細については、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework のドキュメントを参照してください。 実際のサンプルでは、次を参照してください。 [ExecuteXMLReader メソッドを使用して SQL クエリを実行する](executing-sql-queries-by-using-the-executexmlreader-method.md)します。  
  
 TheSqlXmlCommand オブジェクトには、これらの追加メソッドもサポートしています。  
  
 SqlXmlParameter CreateParameter()  
 SqlXmlParameter オブジェクトを作成します。 値を設定することができます、*名前*と*値*このオブジェクトのパラメーター。 このメソッドは、コマンドにパラメーターを渡す場合に便利です。 実際のサンプルでは、次を参照してください。 [SQL クエリの実行&#40;SQLXML マネージ クラス&#41;](sqlxml-4-0-net-framework-support-managed-classes.md)します。  
  
 void ClearParameters()  
 指定したコマンド オブジェクトに作成されたパラメーターを消去します。 このメソッドは、同一のコマンド オブジェクトで複数のクエリを実行する場合に便利です。  
  
## <a name="properties"></a>プロパティ  
 SqlXmlCommand オブジェクトには、これらのプロパティもサポートしています。  
  
 ClientSideXml  
 True に設定すると、サーバーではなくクライアント側で、行セットが XML に変換されます。 このプロパティは、パフォーマンスの負荷を中間層に移す場合に便利です。 このプロパティを使用すると、既存のストアド プロシージャを FOR XML でラップして XML に出力することもできます。  
  
 SchemaPath  
 マッピング スキーマの名前とディレクトリ パス (C:\x\y\MySchema.xml など) を指定します。 このプロパティは、XPath クエリにマッピング スキーマを指定するときに便利です。 パスは、相対パスまたは絶対パスで指定できます。 パスが相対の場合は、相対パスを解決するのには基本パスで指定されている基本パスが使用します。 基本パスが指定されていない場合、相対パスは現在のディレクトリからのパスになります。 実際のサンプルでは、次を参照してください。 [.NET 環境での SQLXML 機能へのアクセス](accessing-sqlxml-functionality-in-the-net-environment.md)します。  
  
 XslPath  
 XSL ファイルの名前とディレクトリ パスを指定します。 パスは、相対パスまたは絶対パスで指定できます。 パスが相対の場合は、相対パスを解決するのには基本パスで指定されている基本パスが使用します。 基本パスが指定されていない場合、相対パスは現在のディレクトリからのパスになります。 実際のサンプルでは、次を参照してください。 [XSL 変換の適用&#40;SQLXML マネージ クラス&#41;](applying-an-xsl-transformation-sqlxml-managed-classes.md)します。  
  
 基本パス  
 基本パス (ディレクトリ パス) を指定します。 このプロパティは XSL ファイル (XslPath プロパティを使用) して、マッピング スキーマ ファイル (を SchemaPath プロパティを使用)、または XML テンプレートで、外部スキーマ参照が指定されている相対パスを解決するために役立ちます (を使用して指定された、 `mapping-schema`属性の場合)。  
  
 OutputEncoding  
 コマンドを実行したときに返されるストリームのエンコードを指定します。 このプロパティは、返されるストリームに特定のエンコードを要求する場合に便利です。 一般的に使用されるエンコードには、UTF-8、ANSI、Unicode などがあります。 既定のエンコードは UTF-8 です。  
  
 名前空間  
 名前空間を使用する XPath クエリを実行できるようにします。 名前空間を使用した XPath クエリの詳細については、次を参照してください。[名前空間を持つ XPath クエリを実行する&#40;SQLXML マネージ クラス&#41;](executing-xpath-queries-with-namespaces-sqlxml-managed-classes.md)します。 実際のサンプルでは、次を参照してください。 [XPath クエリの実行&#40;SQLXML マネージ クラス&#41;](executing-xpath-queries-sqlxml-managed-classes.md)します。  
  
 RootTag  
 コマンドを実行して生成される XML の、単一のルート要素を指定します。 有効な XML ドキュメントには、単一のルートレベルのタグが必要です。 このプロパティでは、コマンドを実行して単一の最上位要素のない XML フラグメントが生成された場合に、返される XML のルート要素を指定できます。 実際のサンプルでは、次を参照してください。 [XSL 変換の適用&#40;SQLXML マネージ クラス&#41;](applying-an-xsl-transformation-sqlxml-managed-classes.md)します。  
  
 CommandText  
 コマンドのテキストを指定します。 このプロパティは、実行するコマンドのテキストを指定するときに使用します。 実際のサンプルでは、次を参照してください。 [SQL クエリの実行&#40;SQLXML マネージ クラス&#41;](sqlxml-4-0-net-framework-support-managed-classes.md)します。  
  
 CommandStream  
 コマンド ストリームを指定します。 このプロパティは、XML テンプレートなどのファイルからコマンドを実行する場合に便利です。 CommandStream、のみを使用する場合 **"Template"** 、 **"UpdateGram"** と **"DiffGram"CommandType**値がサポートされています。 実際のサンプルでは、次を参照してください。 [CommandStream プロパティを使用してテンプレート ファイルを実行する](executing-template-files-by-using-the-commandstream-property.md)します。  
  
 CommandType  
 コマンドの種類を指定します。 このプロパティは、実行するコマンドの種類を指定するときに使用します。 コマンドの種類の値を、次の表に示します。 実際のサンプルでは、次を参照してください。 [.NET 環境での SQLXML 機能へのアクセス](accessing-sqlxml-functionality-in-the-net-environment.md)します。  
  
|値|説明|  
|-----------|-----------------|  
|SqlXmlCommandType.Sql|SQL コマンド (`SELECT * FROM Employees FOR XML AUTO` など) を実行します。|  
|SqlXmlCommandType.XPath|XPath コマンド (`Employees[@EmployeeID=1]` など) を実行します。|  
|SqlXmlCommandType.Template|XML テンプレートを実行します。|  
|SqlXmlCommandType.TemplateFile|指定したパスにあるテンプレート ファイルを実行します。|  
|SqlXmlCommandType.UpdateGram|アップデート グラムを実行します。|  
|SqlXmlCommandType.Diffgram|DiffGram を実行します。|  
  
## <a name="see-also"></a>参照  
 [SqlXmlParameter オブジェクト&#40;SQLXML マネージ クラス&#41;](sqlxml-managed-classes-sqlxmlparameter-object.md)   
 [SqlXmlAdapter オブジェクト&#40;SQLXML マネージ クラス&#41;](sqlxml-managed-classes-sqlxmladapter-object.md)  
  
  
