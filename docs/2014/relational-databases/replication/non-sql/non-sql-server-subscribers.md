---
title: SQL Server 以外のサブスクライバー | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], non-SQL Server Subscribers
- heterogeneous data sources, non-SQL Server Subscribers
- heterogeneous data sources
- heterogeneous database replication, non-SQL Server Subscribers
- non-SQL Server Subscribers, about non-SQL Server Subscribers
- heterogeneous Subscribers
- heterogeneous Subscribers, about heterogeneous Subscribers
- Subscribers [SQL Server replication], non-SQL Server Subscribers
- non-SQL Server Subscribers
ms.assetid: 831e7586-2949-4b9b-a2f3-7b0b699b23ff
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8e5b7592ba97f779d3c1aeb83f34317ef7c6833d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63022247"
---
# <a name="non-sql-server-subscribers"></a>Non-SQL Server Subscribers
  以下の[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーでは、プッシュ サブスクリプションを使用することで、スナップショット パブリケーションおよびトランザクション パブリケーションにサブスクライブできます。 以下に示す 2 つのデータベースの最新バージョンでは、OLE DB プロバイダーを使用したサブスクリプションがサポートされています。  
  
 SQL Server 以外のサブスクライバーへの異種レプリケーションは非推奨とされます。 Oracle パブリッシングは非推奨とされます。 データを移動するには、変更データ キャプチャと [!INCLUDE[ssIS](../../../includes/ssis-md.md)]を使用してソリューションを作成します。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
|[データベース]|オペレーティング システム|プロバイダー|  
|--------------|----------------------|--------------|  
|Oracle|Oracle がサポートするすべてのプラットフォーム|Oracle OLE DB プロバイダー (Oracle によって提供されます)|  
|IBM DB2|MVS、AS400、Unix、Linux、Windows (9.x を除く)|Microsoft Host Integration Server (HIS) OLE DB プロバイダー|  
  
 Oracle および IBM DB2, にサブスクリプションを作成する方法の詳細については、「 [Oracle Subscribers](oracle-subscribers.md) 」および「 [IBM DB2 Subscribers](ibm-db2-subscribers.md)を使用してソリューションを作成します。  
  
## <a name="considerations-for-non-sql-server-subscribers"></a>SQL Server 以外のサブスクライバーに関する注意点  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーにレプリケートする場合は、以下の点に留意してください。  
  
### <a name="general-considerations"></a>全般的な注意点  
  
-   レプリケーションでは、テーブルとインデックス付きビューをテーブルとして[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーにパブリッシュする処理をサポートしています (インデックス付きビューは、インデックス付きビューとしてレプリケートすることはできません)。  
  
-   パブリケーションの新規作成ウィザードでパブリケーションを作成し、[パブリケーションのプロパティ] ダイアログ ボックスを使用して、このパブリケーションを SQL Server 以外のサブスクライバーに対して有効化する場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーに、サブスクリプション データベース内の全オブジェクトの所有者は指定されません。一方、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、パブリケーション データベース内の対応するオブジェクトの所有者が指定されます。  
  
-   パブリケーションに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サブスクライバーと[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーが含まれる場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サブスクライバーのサブスクリプションを作成する前に、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーに対してパブリケーションを有効化する必要があります。  
  
-   既定では、スナップショット エージェントが[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーに対して生成したスクリプトには、CREATE TABLE 構文に引用符なしの識別子が使用されます。 したがって、「test」という名前でパブリッシュされたテーブルは「TEST」としてレプリケートされます。 大文字/小文字の指定をパブリケーション データベース内のテーブルと同一にするには、ディストリビューション エージェントの **-QuotedIdentifier** パラメーターを使用します。 パブリッシュされたオブジェクトの名前 (テーブル、列、制約など) に、スペースや、 **以外のサブスクライバーのデータベースのバージョンでの予約語が含まれている場合は、** -QuotedIdentifier[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] パラメーターも使用する必要があります。 このパラメーターの詳細については、「 [Replication Distribution Agent](../agents/replication-distribution-agent.md)」を参照してください。  
  
-   ディストリビューション エージェントを実行するアカウントには、OLE DB プロバイダーのインストール ディレクトリに対する読み取りアクセス権が必要です。  
  
-   既定では、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーの場合、ディストリビューション エージェントは、サブスクリプション データベースに対して **-SubscriberDB** パラメーターで [(default destination)] の値を使用します。  
  
    -   Oracle の場合、1 つのサーバーに 1 つのデータベースしか作成できないため、データベースを指定する必要はありません。  
  
    -   IBM DB2 の場合、DB2 接続文字列によってデータベースを指定します。 詳細については、「 [SQL Server 以外のサブスクライバーのサブスクリプションの作成](../create-a-subscription-for-a-non-sql-server-subscriber.md)」を参照してください。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターが 64 ビット プラットフォームで実行されている場合、該当する OLE DB プロバイダーの 64 ビット バージョンを使用する必要があります。  
  
-   レプリケーションでは、パブリッシャーおよびサブスクライバーで使用される照合順序やコード ページにかかわらず、データが Unicode 形式に変換されます。 パブリッシャーとサブスクライバーの間でレプリケートを行う場合は、互換性のある照合順序やコード ページを使用することをお勧めします。  
  
-   アーティクルをパブリケーションに追加または削除する場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーのサブスクリプションは再初期化する必要があります。  
  
-   すべての [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーでサポートされる制約は、NULL および NOT NULL のみです。 主キーの制約は一意なインデックスとしてレプリケートされます。  
  
-   NULL 値の扱いはデータベースによって異なり、空白値、空の文字列、および NULL の表示方法に影響します。 また、UNIQUE 制約が定義されている列に値を挿入する際の動作にも影響します。 たとえば、Oracle では一意な列に複数の NULL 値を挿入できますが、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では一意な列に 1 つの NULL 値しか挿入できません。  
  
     他にも注意が必要なのは、列に対して NOT NULL が定義されている場合、NULL 値、空の文字列、および空白値がどのように扱われるかという点です。 Oracle サブスクライバーでのこの問題の対処方法の詳細については、「 [Oracle Subscribers](oracle-subscribers.md)」を参照してください。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーからサブスクリプションが削除されても、レプリケーション関連のメタデータ (トランザクション シーケンス テーブル) は削除されません。  
  
### <a name="conforming-to-the-requirements-of-the-subscriber-database"></a>サブスクライバー データベースの要件への準拠  
  
-   パブリッシュされたスキーマおよびデータは、サブスクライバーのデータベース要件に準拠する必要があります。 たとえば、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のデータベースの最大行サイズが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]よりも小さい場合、パブリッシュされるスキーマおよびデータがこのサイズを超えないようにする必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーにレプリケートされたテーブルには、サブスクライバーのデータベースのテーブル名前付け規則が採用されます。  
  
-   DDL は、SQL Server 以外のサブスクライバーに対してはサポートされていません。 スキーマ変更の詳細については、「[パブリケーション データベースでのスキーマの変更](../publish/make-schema-changes-on-publication-databases.md)」を参照してください。  
  
### <a name="replication-feature-support"></a>レプリケーション機能のサポート  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、プッシュおよびプルの 2 種類のサブスクリプションがオファーされています。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーはプッシュ サブスクリプションを使用する必要があります。このサブスクリプションでは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターでディストリビューション エージェントが実行されます。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、ネイティブ bcp モードとキャラクター モードの 2 種類のスナップショット形式が用意されています。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーでは、キャラクター モードのスナップショットを使用する必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーは、即時更新サブスクリプションおよびキュー更新サブスクリプションを使用できません。また、ピア ツー ピア トポロジのノードになることもできません。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーをバックアップから自動的に初期化することはできません。  
  
## <a name="see-also"></a>参照  
 [異種データベース レプリケーション](heterogeneous-database-replication.md)   
 [パブリケーションのサブスクライブ](../subscribe-to-publications.md)  
  
  
