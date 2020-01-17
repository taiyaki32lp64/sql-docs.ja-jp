---
title: クライアント側とサーバー側の XML 書式設定 (SQLXML 4.0) のアーキテクチャ |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- providers [SQLXML], XML formatting architecture
- SQLOLEDB provider
- client-side XML formatting
- data providers [SQLXML], XML formatting architecture
- SQLNCLI, XML
- server-side XML formatting
- SQL Server Native Client, XML
- SQLXMLOLEDB Provider, XML formatting architecture
ms.assetid: 52440d9e-89fd-4c15-a008-a1ea99f41387
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 03601c4d36a3e11de4df35bc32237ac554ca93fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014440"
---
# <a name="architecture-of-client-side-and-server-side-xml-formatting-sqlxml-40"></a>クライアント側とサーバー側の XML 書式設定のアーキテクチャ (SQLXML 4.0)
  次の図は、サーバー側の XML 書式設定のアーキテクチャです。  
  
 ![サーバー側での XML 書式設定のアーキテクチャです。](../../../database-engine/dev-guide/media/serversidexml.gif "サーバー側でのアーキテクチャの XML 書式設定します。")  
  
 この例では、クライアント側で指定されたコマンドがサーバーに送信されます。 サーバーでは XML ドキュメントが生成され、それがクライアントに返されます。 この場合、サーバーがのインスタンスを持つ[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]します。 サーバー側の XML 書式設定では、SQLXMLOLEDB プロバイダーまたは SQLOLEDB プロバイダーのいずれかを使用できます。  SQLXMLOLEDB プロバイダーでは Sqlxml4.dll が使用されますが、これは SQLXML 4.0 に含まれています。 SQLOLEDB プロバイダーを使用する場合、既定では Sqlxmlx.dll により SQLXML の機能が提供されます。この dll は [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows または Microsoft Data Access Components (MDAC) 2.6 以降に含まれています。 SQLOLEDB で Sqlxml4.dll を使用するには、SQLOLEDB 接続オブジェクトで SQLXML Version プロパティを"SQLXML.4.0"を設定する必要があります。 いずれの場合も、サーバーでは XML ドキュメントが生成され、それがクライアントに送信されます。  
  
> [!NOTE]  
>  XPath クエリとアップデートグラムはクライアントで解析されます。 SQLXML 4.0 の XPath テンプレートまたはアップデートグラム機能を使用するには、Sqlxml4.dll を使用します。  
  
 次の図は、クライアント側の XML 書式設定のアーキテクチャです。  
  
 ![クライアント側での XML 書式設定のアーキテクチャです。](../../../database-engine/dev-guide/media/clientsidexml.gif "クライアント側でのアーキテクチャの XML 書式設定します。")  
  
 この例では、クライアントで SQLXMLOLEDB プロバイダーが使用されます。 接続文字列に SQLOLEDB にデータ プロバイダーのプロパティを設定する必要があります。 (これは、SQLXML 4.0 で唯一の値です)。クライアントで実行されるコマンドは、サーバーに送信されます。 サーバーで生成された行セットがクライアントに送信されます。 クライアントでは、行セットから XML ドキュメントの書式が設定されます。  
  
 SQLXML 4.0 では、データ プロバイダーとして [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) または SQLOLEDB プロバイダーを使用できます。 これらのプロバイダーでは、どのデータ ソースにもアクセスできます。 クエリで単一の行セットが返される限り、XML 変換はクライアント側で適用できます。  
  
  
