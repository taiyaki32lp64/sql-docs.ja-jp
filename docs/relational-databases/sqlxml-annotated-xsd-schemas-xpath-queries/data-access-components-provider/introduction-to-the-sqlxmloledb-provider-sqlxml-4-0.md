---
title: SQLXMLOLEDB プロバイダーの概要 (SQLXML)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXMLOLEDB Provider, properties
- adExecuteStream flag
- SQLXMLOLEDB Provider, about SQLXMLOLEDB Provider
ms.assetid: 2e3f3817-4209-4bf4-9f46-248c95bc6f1b
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7f94cf5002f0f587332df9ccc9a77e24010b8824
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246684"
---
# <a name="introduction-to-the-sqlxmloledb-provider-sqlxml-40"></a>SQLXMLOLEDB プロバイダーの概要 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  SQLXMLOLEDB プロバイダーは、ActiveX Data Objects (ADO) を介して [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 機能へのアクセスを提供する OLE DB プロバイダーです。 ただし、このプロバイダーでは、ADO の "出力ストリームへの書き込み" モードでのみコマンドを実行できます。 SQLXMLOLEDB プロバイダーは行セット プロバイダーではありません。 コマンドを実行するときは、adExecuteStream フラグを指定する必要があります。これにより、ADO は、指定した出力ストリームを使用するように指示されます。  
  
 次の例は、adExecuteStream フラグが指定されている Execute コマンドの構文を示しています。  
  
```  
Dim oTestCommand As New ADODB.Command  
...  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Execute , , adExecuteStream  
...  
```  
  
## <a name="sqlxmloledb-provider-specific-properties"></a>SQLXMLOLEDB プロバイダー固有のプロパティ  
 SQLXMLOLEDB プロバイダーでは、次のプロバイダー固有の接続プロパティへのアクセスが提供されます。  
  
|接続<br /><br /> property|既定<br /><br /> (ある場合)|説明|  
|-----------------------------|----------------------------|-----------------|  
|データ プロバイダー||OLE DB プロバイダーの PROGID を提供します。SQLXMLOLEDB ではこれを介してコマンドが実行されます。 SQLXML 4.0 および [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降、このプロバイダーは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 内に含まれているため、このプロパティ値は "SQLNCLI11" に制限されます。 詳細については、「 [SQL Server Native Client プログラミング](../../../relational-databases/native-client/sql-server-native-client-programming.md)」を参照してください。|  
  
 SQLXMLOLEDB プロバイダーでは、次のプロバイダー固有のコマンド プロパティへのアクセスが提供されます。  
  
|コマンド<br /><br /> property|既定<br /><br /> (ある場合)|説明|  
|--------------------------|----------------------------|-----------------|  
|基本パス|""|基本ファイル パスを指定します。 基本ファイル パスは、XML Stylesheet Language (XSL) の場所またはマッピング スキーマ ファイルを指定するときに使用します。 基本ファイルパスは、xsl またはマッピングスキーマのプロパティで指定されている XSL またはマッピングスキーマファイルの相対パスを解決するためにも使用されます。<br /><br /> このプロパティを使用する例については、「 [SQLXMLOLEDB Provider&#41;&#40;XPath クエリの実行](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-xpath-queries-sqlxmloledb-provider.md)」を参照してください。|  
|ClientSideXML|False|行セットを XML に変換する処理をサーバーではなくクライアントで行う場合は、このプロパティを True に設定します。 これはパフォーマンスの負荷を中間層に移す場合に便利です。<br /><br /> このプロパティを使用する例については、「 [Sql クエリの実行 &#40;SQLXMLOLEDB provider&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-sql-queries-sqlxmloledb-provider.md) 」または「 [Sql クエリを含むテンプレートの実行」 &#40;SQLXMLOLEDB provider&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-templates-that-contain-sql-queries-sqlxmloledb-provider.md)を参照してください。|  
|コンテンツの種類||出力コンテンツの種類を返します。 これは READ ONLY プロパティです。<br /><br /> このプロパティは、コンテンツの種類 (TEXT/XML、TEXT/HTML、image/jpeg など) に関する情報をブラウザーに提供します。 このプロパティの値は、HTTP ヘッダーの一部としてブラウザーに送信される**content-type**フィールドになります。このフィールドには、本文として送信されるドキュメントの MIME の種類 (Multipurpose Internet Mail Extensions) が格納されます。|  
|マッピング スキーマ|NULL|クライアント アプリケーションでマッピング スキーマ (XDR または XSD) に対して XPath クエリを実行する場合、このプロパティを使用してマッピング スキーマの名前を指定します。<br /><br /> パスは相対 (xyz/abc/MySchema.xml) または絶対 (C:\MyFolder\abc\MySchema.xml) パスで指定できます。<br /><br /> 相対パスが指定されている場合、ベースパスプロパティによって指定されるベースパスは、相対パスを解決するために使用されます。 "ベースパス" プロパティにパスが指定されていない場合、相対パスは現在のディレクトリに対する相対パスになります。<br /><br /> [マッピングスキーマ] プロパティの値を指定するときに、ローカルディレクトリのパスまたは URL (https://...) を指定できます。URL を指定する場合は、プロキシサーバー経由で HTTP および HTTPS サーバーにアクセスするように WinHTTP を構成する必要があります。 これには、Proxycfg.exe ユーティリティを実行します。 詳細については、MSDN ライブラリの「Using the WinHTTP Proxy Configuration Utility」(英語) を参照してください。<br /><br /> このプロパティを使用する例については、「 [SQLXMLOLEDB Provider&#41;&#40;XPath クエリの実行](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-xpath-queries-sqlxmloledb-provider.md)」を参照してください。|  
|namespaces||名前空間を使用する XPath クエリを実行できるようにします。 このプロパティを使用する例については、「 [SQLXMLOLEDB Provider&#41;&#40;名前空間を使用した XPath クエリの実行](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-xpath-queries-with-namespaces-sqlxmloledb-provider.md)」を参照してください。|  
|ss Stream Flags||特定の種類のセキュリティ制限を指定するときに使用します。 たとえば、外部サイトなどで、ファイルへの URL 参照やファイルへの絶対パスを許可しない場合や、 テンプレートでクエリを許可しない場合に使用できます。<br /><br /> このプロパティには次の値を割り当てることができます。<br /><br /> 1 = STREAM_FLAGS_DISALLOW_URL 2 = STREAM_FLAGS_DISALLOW_ABSOLUTE_PATH 4 = STREAM_FLAGS_DISALLOW_QUERY 8 = STREAM_FLAGS_ &#xA0;&#xA0;&#xA0;&#xA0;&#xA0;&#xA0;DONTCACHEMAPPINGSCHEMA 16 = STREAM_FLAGS_DONTCACHETEMPLATE 32 = STREAM_FLAGS_DONTCACHEXSL<br /><br /> これらの値の詳細については、次の表に示します。|  
|xml root||結果の XML のルート タグを定義するときに使用します。 たとえば、データベースに対して SQL クエリを実行し、結果の XML ドキュメントに単一のルート要素がない場合は、このプロパティの値を使用して、ドキュメント内に単一のルート要素が追加されます。<br /><br /> このプロパティを使用する例については、「 [SQL クエリの実行 &#40;SQLXMLOLEDB Provider&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-sql-queries-sqlxmloledb-provider.md)」を参照してください。|  
|xsl||クエリで返された XML ドキュメントに XSL 変換を適用する場合に、XSL ファイルを指定するときに使用します。<br /><br /> パスは相対 (xyz/abc/MyXSL.xsl) または絶対 (C:\MyFolder\abc\MyXSL.xsl) パスで指定できます。<br /><br /> 相対パスが指定されている場合、ベースパスプロパティによって指定されるベースパスは、相対パスを解決するために使用されます。 "ベースパス" プロパティにパスが指定されていない場合、相対パスは現在のディレクトリに対する相対パスになります。<br /><br /> このプロパティを使用する例については、「XSL 変換の適用 (SQLXMLOLEDB Provider)」を参照してください。|  
  
 次の表に、ss ストリームフラグのプロパティ値の説明を示します。  
  
|プロパティ値|説明|  
|--------------------|-----------------|  
|STREAM_FLAGS_DISALLOW_URL|マッピング スキーマまたは XSL に URL は指定できません。|  
|STREAM_FLAGS_DISALLOW_ABSOLTE_PATH|マッピング スキーマまたは XSL に指定するパスは、テンプレート自身の基本パスに対して相対的である必要があります。|  
|STREAM_FLAGS_DISALLOW_QUERY|テンプレートでクエリは許可されません。|  
|STREAM_FLAGS_DONTCACHEMAPPINGSCHEMA|マッピング スキーマはキャッシュされません。 このプロパティ値は、データベースが開発段階で、データベース スキーマが変更される可能性のあるときに便利です。|  
|STREAM_FLAGS_DONTCACHETEMPLATE|テンプレートはキャッシュされません。|  
|STREAM_FLAGS_DONTCACHEXSL|XSL はキャッシュされません。|  
  
  
