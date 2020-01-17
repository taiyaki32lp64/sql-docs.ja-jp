---
title: SQLXML 4.0 のプログラミング概念
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, about SQLXML
- SQLXML
ms.assetid: 5a11cda2-b8a3-4453-848f-641afdaa7024
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ff9785d18d46e9aaca26c768d1069c32d3d2e8b6
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75242619"
---
# <a name="sqlxml-40-programming-concepts"></a>SQLXML 4.0 のプログラミング概念
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  クライアント側の XML 機能を追加し既存の機能を拡張するため、SQLXML 3.0 が Web リリースとして提供されました。この機能には、注釈付き XSD スキーマ、XML 一括読み込み、Web サービス (SOAP) サポート、アップデートグラムなどが含まれます。  
  
 
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] では SQLXML 4.0 が導入され、SQLXML 3.0 と同じ機能に加えて、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] の新機能に対応するための追加の更新が提供されました。  
  
 ここでは、SQLXML 4.0 に関する情報を提供します。  
  
 [SQL Server で SQLXML がインストールされない](../../relational-databases/sqlxml/sqlxml-is-not-installed-in-sql-server.md)  
 SQLXML 4.0 をインストールする方法を説明します。  
  
 [SQLXML 4.0 SP1 の新機能](../../relational-databases/sqlxml/what-s-new-in-sqlxml-4-0-sp1.md)  
 SQLXML 4.0 での更新と機能拡張について説明し、このドキュメント内の関連項目へのリンクを提供します。  
  
 [ADO を使用した、SQLXML 4.0 クエリの実行](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)  
 SQLXML クエリに対する ADO の使用方法について説明します。 以前のバージョンに比べて SQLXML 4.0 では ADO がさらに重要になっています。  
  
 [SQLXML 4.0 での xml データ型のサポート](../../relational-databases/sqlxml/xml-data-type-support-in-sqlxml-4-0.md)  
 SQLXML 4.0 で追加された xml データ型のサポートについて説明します。  
  
 [SQLXML のサンプル実行のための必要条件](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)  
 提供される SQLXML の例から実際のサンプルを作成するための要件について説明します。  
  
 [SQLXML 4.0&#41;のクライアント側およびサーバー側の書式設定 &#40;](../../relational-databases/sqlxml/formatting/client-side-and-server-side-formatting-sqlxml-4-0.md)  
 クライアント側とサーバー側の書式設定について情報を提供し、これらを比較します。XML ドキュメントを構築する FOR XML コマンドに関する情報も提供します。  
  
 [SQLXML 4.0 における注釈付き XSD スキーマ](../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xsd-schemas-in-sqlxml-4-0.md)  
 SQLXML 4.0 での注釈付き XSD スキーマの使用について情報を提供します。 レガシ アプリケーションで注釈付き XDR スキーマを使用する場合の情報も提供します。  
  
 [SQLXML 4.0 での XPath クエリの使用](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/using-xpath-queries-in-sqlxml-4-0.md)  
 XPath 言語のサブセットを使用して、注釈付き XSD スキーマにより作成された XML ビューに対してクエリを実行する方法を説明し、例を示します。  
  
 [SQLXML 4.0 での、アップデートグラムを使用したデータ変更](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/using-updategrams-to-modify-data-in-sqlxml-4-0.md)  
 XSD (または XDR) の注釈付きスキーマによって提供される XML ビューを操作し、データベース内のデータを変更するアップデートグラムについて、情報を提供します。  
  
 [XML データの一括読み込みを実行する &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)  
 SQLXML 4.0 で XML の一括読み込みを行う方法について説明します。  
  
 [SQLXML 4.0 のデータ アクセス コンポーネント](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/sqlxml-4-0-data-access-components-sqlxmloledb-provider.md)  
 SQLXMLOLEDB プロバイダーについて説明し、その他の SQLXML 4.0 データ アクセス コンポーネントへのリンクを提供します。  
  
 [SQLXML 4.0 の .NET Framework サポート](https://msdn.microsoft.com/library/c18cf801-f893-4fbc-8e2b-c563f6108acf)  
 .NET Framework に対する SQLXML 4.0 のサポートについて説明します。  
  
 [SQLXML 4.0&#41;&#40;のテンプレート、XSL、およびスキーマのキャッシュ](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/caching-templates-xsl-and-schemas-sqlxml-4-0.md)  
 パフォーマンス向上のため SQLXML で提供されるキャッシュ機能について説明します。  
  
 [SQLXML 4.0 のセキュリティに関する注意点](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/sqlxml-4-0-security-considerations.md)  
 SQLXML 4.0 に関連するセキュリティ問題について説明します。  
  
 [SQLXML 4.0 のガイドラインと制限](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/guidelines-and-limitations-of-sqlxml-4-0.md)  
 SQLXML 4.0 で作業するときに注意すべき問題の一覧を提供します。  
  
## <a name="see-also"></a>参照  
 [XML データ &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
