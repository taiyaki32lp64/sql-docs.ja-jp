---
title: OLE DB プロバイダー (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 6e0488c3-934d-4976-99dc-65c580dc7a3c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7e86375639d875f5cfec21705af47c005afd901e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924754"
---
# <a name="ole-db-providers-ado"></a>OLE DB プロバイダー (ADO)
OLE DB では、統一されたアクセス権を持つアプリケーションをさまざまな情報ソースに格納されているデータを提供する COM インターフェイスのセットを定義します。 これにより、データ ソースのデータ ソースに適した DBMS 機能をサポートするインターフェイスを通じてデータを共有することができます。 仕様では、OLE DB のパフォーマンスの高いアーキテクチャは柔軟なコンポーネント ベースのサービス モデルの使用に基づきます。 アプリケーションとデータの間の中間層の数を指定するのではなく、OLE DB に必要な数のコンポーネントは、特定のタスクを実行するときにのみが必要です。  
  
 たとえば、ユーザーがクエリを実行するとします。 次に、例をいくつか示します。  
  
-   現在存在する、ODBC ドライバーがないネイティブ OLE DB プロバイダー、リレーショナル データベース内に存在するデータ。アプリケーションでは、ADO を使用して、OLE DB Provider for ODBC、適切な ODBC ドライバーが読み込まれますと通信します。 ドライバーは、DBMS では、データを取得する SQL ステートメントを渡します。  
  
-   ネイティブ OLE DB プロバイダーが存在する Microsoft SQL Server にデータが存在します。アプリケーションでは、ADO を使用して、Microsoft SQL Server の OLE DB プロバイダーに直接通信します。 中継ぎ局は必要ありません。  
  
-   Microsoft Exchange Server では、OLE DB プロバイダーが SQL クエリを処理するエンジン公開しないに存在するデータ。アプリケーションでは、ADO、OLE DB Provider for Microsoft Exchange との対話を使用して、処理クエリを実行するために OLE DB のクエリ プロセッサ コンポーネントに呼び出します。  
  
-   ドキュメントの形式で Microsoft の NTFS ファイル システム内に存在するデータ。データは、効率的なコンテンツの検索を有効にするファイル システム内のコンテンツとドキュメントのプロパティのインデックスを作成する Microsoft インテックス サービス、経由でネイティブ OLE DB プロバイダーを使用してアクセスします。  
  
 上記のすべての例では、アプリケーションが、データを照会できます。 コンポーネントの最小数と、ユーザーのニーズが満たされています。 各ケースで必要な場合にのみ、その他のコンポーネントが使用され、必要なコンポーネントのみが呼び出されます。 OLE DB を使用する場合、再利用と共有可能なコンポーネントのオンデマンドの読み込みは、このは高パフォーマンスに大きく貢献します。  
  
 プロバイダーは、2 つのカテゴリに分類されます。 データとサービスを提供するものを提供するものです。 データ プロバイダーは、独自のデータを所有しているし、表形式で、アプリケーションに公開します。 サービス プロバイダーは、ADO アプリケーションで機能を強化場合の作成や、データの利用によって、サービスをカプセル化します。 その他のサービス プロバイダーまたはコンポーネントと連携して動作する必要があります、サービスのコンポーネントとして、サービス プロバイダーはさらに定義こともできます。  
  
 ADO は、一貫性のある、さまざまな OLE DB プロバイダーに高レベルのインターフェイス。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [データ プロバイダー](../../../ado/guide/data/data-providers.md)  
  
-   [サービス プロバイダーとコンポーネント](../../../ado/guide/data/service-providers-and-components.md)
