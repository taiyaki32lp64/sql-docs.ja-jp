---
title: Oracle パブリッシングの用語 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], glossary
ms.assetid: e21dfa4b-6144-4be7-9cbf-ca2709b2bd9f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fa1959a4f0fa6a2afa2fdf585d0c82d1238a019b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63022391"
---
# <a name="glossary-of-terms-for-oracle-publishing"></a>Oracle パブリッシングの用語
  Oracle パブリッシングの構成および管理を行う場合には、以下に示す Oracle の用語を理解している必要があります。 Oracle の用語の完全な一覧については、Oracle のオンライン マニュアルを参照してください。  
  
 索引構成表 (IOT)  
 データがディスク上でインデックス順に物理的に並べ替えられたテーブルです。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のクラスター化インデックス付きテーブルに似ています。 IOT はクラスター化インデックス付きテーブルとしてサブスクライバーにレプリケートされます。  
  
 Instance  
 Oracle データベースはインスタンスに関連付けられています。 このインスタンスは、メモリ、およびデータベースをサポートするバックグラウンド プロセスから構成されます。 Oracle のインスタンスは常に単一のデータベースにマッピングされます。一方、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスには複数のデータベースを格納できます。 状況によっては、1 つの Oracle データベースに複数のインスタンスを持たせることもできます。  
  
 Oracle リスナー  
 Oracle データベース インスタンスの受信ネットワーク トラフィックを処理します。 Oracle データベースへのネットワーク接続を構成する場合、トラフィックの送信に使用するプロトコルと、リスナーがトラフィックを受信待ちするポートを指定します。 通常の構成ではリスナーは Oracle データベースのインスタンスと同一のコンピューター上で実行されます。リスナーは 1 つ以上のインスタンスに対し機能するように構成できます。  
  
 ROWID  
 データベースの特定の行の位置を示すポインターです。 テーブル スキャンやインデックスよりも ROWID を使用する方が行を高速に取得できるため、レプリケーションではパブリッシュされたテーブルの変更を処理する際、一時的に ROWID が使用されます。  
  
 Sequence  
 一意の数値を生成するためのデータベース オブジェクトです。 レプリケーションではシーケンスを使用して、パブリッシュされたテーブルへの変更を順序付けします。  
  
 SQL\*Plus  
 Oracle データベースへのアクセスおよび照会に使用されるアプリケーションです。 このアプリケーションは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **sqlcmd**に似ています。  
  
 シノニム  
 オブジェクトの別名です。 Oracle パブリッシャーを構成すると、特別なパブリック シノニム **MSSQLSERVERDISTRIBUTOR** が自動的に作成されます。 このシノニムは **HREPL_Distributor** テーブルを参照して、パブリッシャーにサービスを提供する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターへの論理ポインターを示します。  
  
 Oracle データベースがパブリッシュされた後で、別の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターを使用するようにパブリッシャーを構成することはできません。これは、パブリッシャーにサービスを提供するように既に構成されている特定のディストリビューターが、このパブリック シノニムによって識別されるためです。  
  
 テーブルスペース  
 データベース領域の単位で、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のファイル グループにほぼ等しい意味です。  
  
 TNS サービス名  
 TNS (Transparent Network Substrate) とは、Oracle データベースが使用する通信層です。 TNS サービス名は、ネットワーク上での Oracle データベース インスタンスの名前です。 TNS サービス名は、Oracle データベースへの接続を構成するときに割り当てます。 レプリケーションでは TNS サービス名を使用してパブリッシャーを識別し、接続を確立します。  
  
 ユーザー スキーマ  
 ユーザー スキーマは、特定のデータベース オブジェクトのセットを所有するデータベース ユーザーとして考えることができます。 レプリケーションの管理ユーザー スキーマは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のレプリケーション処理により Oracle データベース内で作成されたすべてのオブジェクトを所有します。ただし、パブリック シノニム **MSSQLSERVERDISTRIBUTOR** は除きます。  
  
## <a name="see-also"></a>参照  
 [Oracle パブリッシャーの構成](configure-an-oracle-publisher.md)   
 [Oracle パブリッシャー上で作成されたオブジェクト](objects-created-on-the-oracle-publisher.md)   
 [SQL Server 以外のパブリッシャー](non-sql-server-publishers.md)   
 [Oracle Publishing Overview](oracle-publishing-overview.md)  
  
  
