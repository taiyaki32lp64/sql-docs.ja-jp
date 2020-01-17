---
title: Oracle パブリッシャーの設計上の注意点および制限 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], design considerations and limitations
ms.assetid: 8d9dcc59-3de8-4d36-a61f-bc3ca96516b6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 043bf26fb17a3433e59623b5b3bfddaaea8bc89f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63022515"
---
# <a name="design-considerations-and-limitations-for-oracle-publishers"></a>Oracle パブリッシャーの設計上の注意点および制限
  Oracle データベースからのパブリッシュは、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースからのパブリッシュとほぼ同じように機能するように設計されています。 ただし、以下の制限および問題に注意してください。  
  
-   [Oracle (ゲートウェイ)] を選択すると、[Oracle (完全)] より高いパフォーマンスが得られますが、このオプションは、複数のトランザクション パブリケーションで同じテーブルをパブリッシュする場合は使用できません。 テーブルを表示できるのは、最大で 1 つのトランザクション パブリケーションと、任意の数のスナップショット パブリケーションになります。 複数のトランザクション パブリケーションで同じテーブルをパブリッシュする必要がある場合は、[Oracle (完全)] を選択します。  
  
-   レプリケーションでは、テーブル、インデックス、および具体化されたビューのパブリッシュをサポートしています。 その他のオブジェクトはレプリケートされません。  
  
-   Oracle と [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のデータベースのデータの保存および処理には、レプリケーションに影響を与える小さな違いがいくつかあります。  
  
-   Oracle パブリッシャーを使用する場合に、トランザクション レプリケーション機能をサポートする方法にはさまざまな違いがあります。  
  
## <a name="support-for-publishing-objects-from-oracle"></a>Oracle からのオブジェクトのパブリッシュのサポート  
 レプリケーションでは、Oracle データベースからの以下のオブジェクトのレプリケートをサポートしています。  
  
-   テーブル  
  
-   索引構成表  
  
-   インデックス  
  
-   具体化されたビュー (テーブルとしてレプリケート)  
  
 以下については、パブリッシュされたテーブルに存在する可能性はありますが、レプリケートされません。  
  
-   ドメイン ベースのインデックス  
  
-   関数ベースのインデックス  
  
-   既定値  
  
-   CHECK 制約  
  
-   外部キー  
  
-   ストレージのオプション (テーブルスペース、クラスターなど)  
  
 以下のオブジェクトはレプリケートできません。  
  
-   入れ子になったテーブル  
  
-   Views  
  
-   パッケージ、パッケージ本体、プロシージャ、およびトリガー  
  
-   キュー  
  
-   シーケンス  
  
-   シノニム  
  
 サポートされるデータ型の詳細については、「 [Data Type Mapping for Oracle Publishers](data-type-mapping-for-oracle-publishers.md)」を参照してください。  
  
## <a name="differences-between-oracle-and-sql-server"></a>Oracle と SQL Server の違い  
  
-   Oracle では、一部のオブジェクトに対する最大サイズ制限が異なります。 Oracle パブリケーション データベースで作成されたオブジェクトは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の対応するオブジェクトの最大サイズ制限に従う必要があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の制限について詳しくは、「[SQL Server の最大容量仕様](../../../sql-server/maximum-capacity-specifications-for-sql-server.md)」をご覧ください。  
  
-   既定では、Oracle のオブジェクト名は大文字で作成されます。 Oracle オブジェクトの名前が Oracle データベースで大文字となっている場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターでこれらをパブリッシュするときは、名前が大文字になっているかどうかを確認してください。 大文字および小文字を正しく指定しないと、オブジェクトが見つからないことを示すエラー メッセージが表示される可能性があります。  
  
-   Oracle の SQL 言語仕様は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]と若干異なります。行フィルターは、Oracle 準拠の構文で記述する必要があります。  
  
### <a name="considerations-for-large-objects"></a>ラージ オブジェクトに関する注意点  
 ラージ オブジェクト (LOB) データは、アーティクルのログ テーブルに格納されません。LOB データへの更新は、常に、パブリッシュされたテーブルから直接取得します。 更新がトランザクション パブリケーションでレプリケートされるのは、LOB に影響を与える操作により、レプリケートされたテーブルでレプリケーション トリガーが起動される場合に限られます。 Oracle トリガーは、LOB を含む行が挿入または削除されると起動されますが、LOB の列への更新の場合には、トリガーは起動されません。 LOB の列への更新が直ちにレプリケートされるのは、同じ行の LOB ではない列も同じ Oracle トランザクションで更新される場合に限られます。 更新されない場合、LOB の列は、同じ行の LOB ではない列への更新が次回に発生したときに、サブスクライバーで更新されます。 アプリケーションでこの動作を許容できることを確認してください。  
  
 トランザクション パブリケーションで LOB の列への更新をレプリケートするには、アプリケーションを記述するときに、次のいずれかの方法を検討してください。  
  
-   行を更新せず、トランザクションで行を削除および再挿入します。行を再挿入するときは、新しい LOB を指定します。 削除と挿入の両方でトリガーを起動するため、行はレプリケートされます。  
  
-   LOB の列に加え、LOB ではない列を行の更新に含めるか、同じ Oracle トランザクションの一部として、その行の LOB ではない列を更新します。 どちらの場合でも、LOB ではない列の更新により、トリガーが起動します。  
  
 LOB の詳細については、「 [Data Type Mapping for Oracle Publishers](data-type-mapping-for-oracle-publishers.md)」を参照してください。  
  
### <a name="unique-indexes-and-constraints"></a>一意インデックスと制約  
 スナップショット レプリケーションとトランザクション レプリケーションの両方において、一意のインデックスおよび制約 (主キー制約を含む) に含まれる列は、特定の制限事項に従う必要があります。 これらの制限に従わない場合、制約またはインデックスはレプリケートされません。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインデックスに許容される最大列数は 16 です。  
  
-   一意の制約に含まれるすべての列は、サポートされているデータ型である必要があります。 データ型の詳細については、「 [Data Type Mapping for Oracle Publishers](data-type-mapping-for-oracle-publishers.md)」をご覧ください。  
  
-   一意の制約に含まれるすべての列は、パブリッシュする必要があります (フィルター選択はできません)。  
  
-   一意の制約またはインデックスに関係する列には NULL 値を設定できません。  
  
 以下の問題についても考慮に入れてください。  
  
-   Oracle および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は NULL の扱いが異なります。Oracle では、NULL を許容する列に NULL 値が指定された複数の行を許可し、一意の制約またはインデックスに含めることができます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では一意性が強制され、同じ列に NULL 値のある行は 1 行だけ許可されます。 NULL を許容する一意の制約またはインデックスをパブリッシュすることはできません。パブリッシュされたテーブルで、インデックスまたは制約に含まれる列に NULL 値のある行が複数含まれる場合、サブスクライバーで制約違反が発生します。  
  
-   一意性をテストする場合、フィールドの後続の空白は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では無視されますが、Oracle では無視されません。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のトランザクション レプリケーションと同様、Oracle のトランザクション パブリケーションのテーブルには主キーが必要です。主キーは上記のルールに基づき、一意である必要があります。 主キーが前の項目で示したルールに従わない場合、トランザクション レプリケーションに対し、テーブルをパブリッシュすることはできません。  
  
## <a name="differences-between-oracle-publishing-and-standard-transactional-replication"></a>Oracle パブリッシングと標準的なトランザクション レプリケーションの違い  
  
-   Oracle パブリッシャーは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューター、そのディストリビューターを使用する任意の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] パブリッシャー、またはパブリケーションを受信する任意のサブスクライバーと同じ名前にすることはできません。 同じディストリビューターによって処理される各パブリケーションには、一意の名前を付ける必要があります。  
  
-   Oracle パブリケーションでパブリッシュされたテーブルは、レプリケートされたデータを受信することはできません。 したがって Oracle パブリッシングでは、即時更新サブスクリプションまたはキュー更新サブスクリプションを使用したパブリケーション、およびピア ツー ピア レプリケーションや双方向レプリケーションなど、パブリケーション テーブルがサブスクリプション テーブルとしても機能するトポロジはサポートしていません。  
  
-   Oracle データベースでの主キーから外部キーのリレーションシップは、サブスクライバーにレプリケートされません。 ただし、変更が配信されると、リレーションシップはデータに保持されます。  
  
-   標準的なトランザクション パブリケーションは、最大 1000 列のテーブルをサポートします。 Oracle のトランザクション パブリケーションがサポートするのは 995 列です (レプリケーションにより、パブリッシュされた各テーブルに 5 列が追加されます)。  
  
-   COLLATE 句は、CREATE TABLE ステートメントに追加され、大文字と小文字を区別する比較を有効にします。この比較は、主キーおよび一意の制約にとって重要です。 この動作はスキーマ オプション 0x1000 で制御されます。このオプションは、[sp_addarticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) の **@schema_option** パラメーターで指定します。  
  
-   ストアド プロシージャを使用して Oracle パブリッシャーを構成またはメンテナンスする場合、プロシージャを明示的なトランザクションに入れないでください。 これは Oracle パブリッシャーへの接続に使用するリンク サーバーではサポートされていません。  
  
-   ウィザードにより Oracle パブリケーションに対するプル サブスクリプションを作成する場合は、 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降で提供されたサブスクリプションの新規作成ウィザードを使用する必要があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]より古いバージョンの場合でも、ストアド プロシージャおよび SQL-DMO インターフェイスを使用して、Oracle パブリケーションに対するプル サブスクリプションを設定できます。  
  
-   ストアド プロシージャを使用して、サブスクライバーに変更を反映する場合 (既定)、MCALL 構文はサポートされていても、Oracle パブリッシャーからのパブリケーションである場合は、異なる動作をすることに注意してください。 通常、MCALL では、パブリッシャーで更新された列を示すビットマップを提供します。 Oracle パブリケーションの場合、ビットマップは常にすべての列が更新されたことを示しています。 ストアド プロシージャの使用に関する詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。  
  
### <a name="transactional-replication-feature-support"></a>トランザクション レプリケーション機能のサポート  
  
-   Oracle パブリケーションでは、SQL Server パブリケーションがサポートする一部のスキーマ オプションがサポートされていません。 スキーマ オプションの詳細については、「[sp_addarticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)」を参照してください。  
  
-   Oracle パブリケーションに対するサブスクライバーは、即時更新サブスクリプションまたはキュー更新サブスクリプションを使用できません。また、ピア ツー ピア トポロジまたは双方向トポロジでノードになることもできません。  
  
-   Oracle パブリケーションに対するサブスクライバーは、バックアップから自動的に初期化することはできません。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、バイナリと行数の 2 種類の検証をサポートしています。 Oracle パブリッシャーでは、行数検証をサポートしています。 詳細については、「[Validate Replicated Data](../validate-data-at-the-subscriber.md)」 (レプリケートされたデータの検証) を参照してください。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、ネイティブ bcp モードとキャラクター モードの 2 種類のスナップショット形式が用意されています。 Oracle パブリッシャーでは、キャラクター モード スナップショットをサポートしています。  
  
-   パブリッシュされた Oracle テーブルへのスキーマ変更はサポートされていません。 スキーマ変更を行うには、まずパブリケーションを削除し、変更を行ってから、パブリケーションおよびサブスクリプションを再作成します。  
  
    > [!NOTE]  
    >  パブリッシュされたテーブルが利用されていないときに、スキーマ変更とその後のパブリケーションおよびサブスクリプションの削除、再作成を一度に行う場合、サブスクリプションに対して [レプリケーションのサポートのみ] オプションを指定できます。 これにより、各サブスクライバーにスナップショットをコピーすることなく、サブスクリプションを同期させることができます。 詳細については、「[スナップショットを使用しないトランザクション サブスクリプションの初期化](../initialize-a-transactional-subscription-without-a-snapshot.md)」を参照してください。  
  
### <a name="replication-security-model"></a>レプリケーションのセキュリティ モデル  
 Oracle のパブリッシングのセキュリティ モデルは、標準的なトランザクション レプリケーションのセキュリティ モデルと同じですが、以下の点が異なります。  
  
-   スナップショット エージェントおよびログ リーダー エージェントがディストリビューターからパブリッシャーへの接続に使用するアカウントは、次のいずれかの方法で指定されます。  
  
    -   [sp_adddistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql) の **@security_mode** パラメーター (Oracle 認証が使用される場合、 **@login** と **@password** にも値を指定します)  
  
    -   SQL Server Management Studio の **[サーバーへの接続]** ダイアログ ボックス。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターで Oracle パブリッシャーを構成するときに、これを使用します。  
  
     標準的なトランザクション レプリケーションでは、[sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql) と [sp_addlogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql) でアカウントが指定されます。  
  
-   スナップショット エージェントおよびログ リーダー エージェントが接続に使用するアカウントは、[sp_changedistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql) またはプロパティ シートで変更することはできませんが、パスワードは変更できます。  
  
-   [sp_adddistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql) の **@security_mode** パラメーターに 1 (Windows 統合認証) の値を指定する場合は、次のとおりです。  
  
    -   スナップショット エージェントとログ リーダー エージェントの両方で使用するプロセス アカウントおよびパスワード ([sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql) および [sp_addlogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql) の **@job_login** および **@job_password** パラメーター) は、Oracle パブリッシャーへの接続に使用するアカウントおよびパスワードと同じにする必要があります。  
  
    -   [sp_changepublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql) または [sp_changelogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql) から **@job_login** パラメーターを変更することはできませんが、パスワードは変更できます。  
  
 レプリケーション セキュリティの詳細については、次を参照してください。 [SQL Server レプリケーションのセキュリティ](../security/view-and-modify-replication-security-settings.md)します。  
  
## <a name="see-also"></a>参照  
 [Oracle パブリッシャーの管理上の注意点](administrative-considerations-for-oracle-publishers.md)   
 [Oracle パブリッシャーの構成](configure-an-oracle-publisher.md)   
 [Oracle パブリッシングの概要](oracle-publishing-overview.md)  
  
  
