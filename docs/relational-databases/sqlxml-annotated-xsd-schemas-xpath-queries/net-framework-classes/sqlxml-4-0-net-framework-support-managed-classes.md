---
title: SQLXML マネージド クラス
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- .NET Framework [SQLXML], Managed Classes
- SQL Server .NET Data Provider
- Managed Classes [SQLXML], about managed classes
- providers [SQLXML], SQL Server .NET Data Provider
- data providers [SQLXML], SQL Server .NET Data Provider
- Managed Classes [SQLXML]
- XML [SQLXML]
- SQLXML Managed Classes
- providers [SQLXML], SQLXML Managed Classes
- data providers [SQLXML], SQLXML Managed Classes
- SQLXML, Managed Classes
ms.assetid: 73a5faeb-dabf-4895-acb5-a9651b646065
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7511dc12bea8a83544ddb39ff427b6400128294e
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246917"
---
# <a name="sqlxml-40-net-framework-support---managed-classes"></a>SQLXML 4.0 の .NET Framework サポート - マネージド クラス
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 では、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスから XML データへのアクセス、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 環境へのデータの移動、データの処理、および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] への更新の適用を行うアプリケーションを作成するための機能がサポートされています。 
  
  
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML マネージド クラスでは、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 内で SQLXML 4.0 の機能へのアクセスが提供されます。 SQLXML マネージド クラスを使用すると、C# アプリケーションを作成して、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスから XML データにアクセスしたり、.NET Framework 環境にデータを取り込んだり、データを処理したり、変更を DiffGram として [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に送信し適用することができます。 SQL マネージド クラスを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースに更新を適用するときには、マッピング スキーマを使用する必要があります。 実際のサンプルについては、「 [.Net 環境での SQLXML 機能へのアクセス](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md)」を参照してください。  
  
 SQLXML 4.0 で SQLXML マネージド クラスを使用するには、Microsoft Visual Studio をインストールする必要があります。  
  
> [!NOTE]  
>  .NET Framework には [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .NET データ プロバイダーが含まれています。 このプロバイダーは .NET 環境から [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] へのアクセスに使用できますが、扱えるのは従来の SQL クエリ (FOR XML クエリ以外のリレーショナル データベース クエリ) だけです。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で XML テンプレートやサーバー側の XPath クエリを実行することはできません。  

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .NET Framework 内のデータへのアクセスと変更、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)]および diffgram を使用したテーブルの[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データの更新の詳細については、「 [.net 環境での SQLXML 機能へのアクセス](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md)」を参照してください。  
  
> [!NOTE]  
>  XML 一括読み込みを使用して XML ドキュメントの一括読み込みを行う [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio アプリケーションを作成することもできます。 詳細については、「 [XML データの一括読み込みの実行 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)」を参照してください。 作成するアプリケーションには、XML 一括読み込みの DLL (Xblkld4.dll) への参照を追加する必要があります。 これは COM DLL で、Visual Studio .NET ではこのラッパー ライブラリが自動的に作成されます。  
  
  このセクションでは、SQLXML マネージクラスの[!INCLUDE[msCoName](../../../includes/msconame-md.md)]使用方法を示すサンプルアプリケーションについて説明します。  
 [SQLXML マネージクラス &#40;の SQL クエリの実行&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-sqlxml-managed-classes.md)  
  [ExecuteXMLReader メソッドを使用した、SQL クエリの実行](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-by-using-the-executexmlreader-method.md)  
  [クライアント側での XML の処理 &#40;SQLXML マネージクラス&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/processing-xml-on-the-client-side-sqlxml-managed-classes.md)  
  [SQLXML マネージクラス &#40;の XPath クエリの実行&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-xpath-queries-sqlxml-managed-classes.md)  
  [SQLXML マネージクラス &#40;名前空間を使用した XPath クエリの実行&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-xpath-queries-with-namespaces-sqlxml-managed-classes.md)  
  [CommandText プロパティを使用した、テンプレート ファイルの実行](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-template-files-by-using-the-commandtext-property.md)  
  [CommandStream プロパティを使用した、テンプレート ファイルの実行](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-template-files-by-using-the-commandstream-property.md)  
  [SQLXML マネージクラス &#40;の XSL 変換の適用&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/applying-an-xsl-transformation-sqlxml-managed-classes.md)  
  

  
  
