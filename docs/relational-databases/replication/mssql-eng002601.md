---
title: MSSQL_ENG002601 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG002601 error
ms.assetid: 657c3ae6-9e4b-4c60-becc-4caf7435c1dc
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 4384164d7baa79559d8810114494473435894f8c
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770511"
---
# <a name="mssqleng002601"></a>MSSQL_ENG002601
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|2601|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名|なし|  
|メッセージ テキスト|一意インデックス '%.\*ls' を含むオブジェクト '%.*ls' には重複するキー行を挿入できません。|  
  
## <a name="explanation"></a>説明  
 このエラーは、データベースがレプリケートされたかどうかにかかわらず発生する一般エラーです。 レプリケートされたデータベースでは、このエラーは、一般に主キーがトポロジ間で適切に管理されなかった場合に発生します。 分散環境では、主キー列などの一意の列に複数のノードで同じ値が挿入されないようにすることが不可欠です。 以下のような原因が考えられます。  
  
-   行の挿入と更新が複数のノードで行われた。 マージ レプリケーションとトランザクション レプリケーションの更新可能なサブスクリプションには、どちらも競合を検出して解決する機能がありますが、それでも行を 1 つのノード上だけで挿入または更新することが推奨されます。 ピア ツー ピアのトランザクション レプリケーションでは、競合を検出し解決する機能はありません。挿入と更新をパーティション分割する必要があります。  
  
-   読み取り専用のサブスクライバーで行が挿入された。 更新可能なサブスクリプションまたはピア ツー ピアのトランザクション レプリケーションを使用していない場合、スナップショット パブリケーションのサブスクライバーは、トランザクション パブリケーションのサブスクライバーと同様に、読み取り専用として扱われる必要があります。  
  
-   ID 列を持つテーブルが使用されているが、列が正しく管理されていない。  
  
-   マージ レプリケーションでは、システム テーブル **MSmerge_contents** への挿入時にこのエラーが発生することもあり、次のようなエラーが表示されます。一意インデックス 'ucl1SycContents' を含むオブジェクト 'MSmerge_contents' には重複するキー行を挿入できません。  
  
## <a name="user-action"></a>ユーザーの操作  
 必要なアクションは、エラーが発生した原因によって異なります。  
  
-   行の挿入と更新が複数のノードで行われた。  
  
     使用するレプリケーションの種類にかかわらず、できる限り挿入と更新をパーティション分割することをお勧めします。これにより、競合の検出と対処に必要な処理を減らすことができます。 ピア ツー ピアのトランザクション レプリケーションの場合は、挿入と更新のパーティション分割は必須です。 詳細については、「 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)」を参照してください。  
  
-   読み取り専用のサブスクライバーで行が挿入された。  
  
     マージ レプリケーション、更新可能なサブスクリプションを使用したトランザクション レプリケーション、またはピア ツー ピアのトランザクション レプリケーションを使用していない場合は、サブスクライバーで行を挿入または更新しないでください。  
  
-   ID 列を持つテーブルが使用されているが、列が正しく管理されていない。  
  
     マージ レプリケーションおよび更新可能なサブスクリプションを使用したトランザクション レプリケーションの場合は、ID 列はレプリケーションで自動的に管理してください。 ピア ツー ピアのトランザクション レプリケーションの場合は、手動で管理する必要があります。 詳細については、「[Replicate Identity Columns](../../relational-databases/replication/publish/replicate-identity-columns.md)」 (ID 列のレプリケート) を参照してください。  
  
-   システム テーブル **MSmerge_contents**への挿入時にエラーが発生する。  
  
     このエラーは、結合フィルター プロパティ **join_unique_key**の値が不適切なために発生します。 このプロパティは、親テーブルの結合列が一意である場合にのみ、TRUE に設定する必要があります。 このプロパティが TRUE に設定されているにもかかわらず、結合列が一意でない場合は、このエラーが発生します。 このプロパティの設定の詳細については、「 [マージ アーティクル間の結合フィルターの定義および変更](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
