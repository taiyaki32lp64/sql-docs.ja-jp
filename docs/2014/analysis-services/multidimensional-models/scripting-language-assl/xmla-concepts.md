---
title: XMLA の概念 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XMLA, concepts
ms.assetid: 816183a7-d2f7-4e14-8e5b-2a4c1798fbc1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0da9467d293c0081309accd99fb46d7589fb4b8b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62736576"
---
# <a name="xmla-concepts"></a>XMLA の概念
  XML for Analysis (XMLA) オープン スタンダードでは、World Wide Web 上に存在するデータ ソースへのアクセスがサポートされています。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] XMLA 1.1 仕様に準拠した、XMLA を実装します。  
  
 XML for Analysis (XMLA) は Simple Object Access Protocol (SOAP) ベースの XML プロトコルで、Web 上に存在するあらゆる標準的な多次元データ ソースへの汎用データ アクセスを提供することを目的に特別に設計されています。 XMLA はコンポーネント オブジェクト モデル (COM) を公開するクライアント コンポーネントをデプロイする必要もなくなりますまたは[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework のインターフェイスします。 インターネット環境では、サーバーとのやり取りに多くの時間とリソースが費やされ、データへの状態を保持する接続によってサーバーへのユーザー接続が制限されることがありますが、XMLA はそのようなインターネット環境のために最適化されています。  
  
 XMLA は、ネイティブ プロトコルは、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]、クライアント アプリケーションとのインスタンス間のすべての対話のために使用される[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]します。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] は XML for Analysis 1.1 を完全にサポートし、さらには、メタデータ管理、セッション管理、およびロック機能をサポートする拡張機能を提供します。 分析管理オブジェクト (AMO) と ADOMD.NET はいずれも、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] インスタンスとの通信に XMLA プロトコルを使用します。  
  
## <a name="handling-xmla-communications"></a>XMLA 通信の処理  
 XMLA オープン スタンダードでは、2 つの汎用メソッド `Discover` および `Execute` を記述しています。 これらのメソッドは、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] インスタンス上で送受信される情報を処理するために、XML がサポートする疎結合のクライアント/サーバー アーキテクチャを使用します。  
  
 `Discover` メソッドは Web サービスから情報とメタデータを取得します。 この情報には、使用可能なデータ ソースの一覧、任意のデータ ソース プロバイダーに関する情報などが含まれます。 データ ソースから取得されるデータは、プロパティによって定義および成形されます。 `Discover` メソッドは、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] インスタンス上のデータ ソースに対してクライアント アプリケーションが要求するさまざまな種類の情報を定義するための共通メソッドです。 プロパティと汎用インターフェイスを使用すれば、クライアント アプリケーション内の既存の機能を書き直さなくても拡張機能を利用できます。  
  
 `Execute` メソッドを使用すると、アプリケーションはプロバイダー固有のコマンドを XMLA データ ソースに対して実行できます。  
  
 XMLA プロトコルは Web アプリケーション用に最適化されていますが、LAN 指向のアプリケーションでもこれを利用できます。 次のようなアプリケーションは、この XML ベースの API の利点を活用できます。  
  
-   クライアント/サーバー間の柔軟な通信テクノロジを必要とするクライアント/サーバー アプリケーション  
  
-   複数のオペレーティング システムを扱うことを想定したクライアント/サーバー アプリケーション  
  
-   サーバー容量を増やすために大きなステートを要求しないクライアント  
  
## <a name="xmla-and-the-unified-dimensional-model"></a>XMLA と統合ディメンショナル モデル  
 XMLA は、統合ディメンショナル モデル (UDM) の手法を採用しているビジネス インテリジェンス アプリケーションによって使用されるプロトコルです。  
  
  
