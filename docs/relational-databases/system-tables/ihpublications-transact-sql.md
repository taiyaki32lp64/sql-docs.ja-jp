---
title: IHpublications (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublications_TSQL
- IHpublications
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublications system table
ms.assetid: b519a101-fa53-44be-bd55-6ea79245b5d1
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5a94299b1411cdb53a47c773330773ce7209fbf2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990335"
---
# <a name="ihpublications-transact-sql"></a>IHpublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublications**システム テーブルには、現在のディストリビューターを使用して SQL Server 以外のパブリケーションごとに 1 つの行が含まれています。 このテーブルは、ディストリビューション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**pubid**|**int**|パブリケーションの一意の ID を提供する id 列です。|  
|**name**|**sysname**|パブリケーションに関連付けられている一意の名前。|  
|**repl_freq**|**tinyint**|レプリケーションの頻度:<br /><br /> **0** = トランザクション ベースします。<br /><br /> **1** = テーブルの定期更新します。|  
|**status**|**tinyint**|パブリケーションで、次のいずれかの状態です。<br /><br /> **0** = 非アクティブです。<br /><br /> **1** = アクティブ。|  
|**sync_method**|**tinyint**|同期方法:<br /><br /> **1** = キャラクター一括コピーします。<br /><br /> **4** = Concurrent_c 文字一括コピーが使用されますが、テーブルは、スナップショット時にロックされません。|  
|**snapshot_jobid**|**[バイナリ]**|スケジュールされたタスク id。|  
|**enabled_for_internet**|**bit**|パブリケーションの同期ファイルが FTP やその他のサービスを介してインターネットに公開されるかどうかを示します、 **1**インターネットからアクセスできることを意味します。|  
|**immediate_sync_ready**|**bit**|かどうか、同期ファイルが利用できることを示します**1**が使用できることを意味します。 *非 SQL パブリッシャーに対してサポートされていません。*|  
|**allow_queued_tran**|**bit**|変更をパブリッシャーで適用できるようになるまで、サブスクライバーで変更をキューに保持するかどうかを示します。 場合**1**、サブスクライバーの変更はキューに登録します。 *非 SQL パブリッシャーに対してサポートされていません。*|  
|**allow_sync_tran**|**bit**|パブリケーションに対してサブスクリプションの即時更新を許可するかどうかを指定します。 **1**即時更新サブスクリプションを許可することを意味します。 *非 SQL パブリッシャーに対してサポートされていません。*|  
|**autogen_sync_procs**|**bit**|同期はストアド プロシージャの即時更新であるかどうかを指定します。 サブスクリプションがパブリッシャーで生成します。 **1**パブリッシャー側で生成されることを意味します。 *非 SQL パブリッシャーに対してサポートされていません。*|  
|**snapshot_in_defaultfolder**|**bit**|既定のフォルダーに、スナップショット ファイルが格納されているかどうかを指定します。 場合**0**、スナップショット ファイルがで指定された代替位置に格納されている*alternate_snapshot_folder*します。 場合**1**、スナップショット ファイルは既定のフォルダーにあります。|  
|**alt_snapshot_folder**|**nvarchar(510)**|スナップショットの代替フォルダーの場所を指定します。|  
|**pre_snapshot_script**|**nvarchar(510)**|ポインターを指定します、 **.sql**ファイルの場所。 ディストリビューション エージェントは、サブスクライバー側でスナップショットを適用するとき、レプリケートされたオブジェクト スクリプトより前に、プリスナップショット スクリプトを実行します。|  
|**post_snapshot_script**|**nvarchar(510)**|ポインターを指定します、 **.sql**ファイルの場所。 ディストリビューション エージェントは、他のすべてのレプリケートされたオブジェクト スクリプトとデータが、初期同期中に適用された後に、ポスト スナップ ショット スクリプトを実行します。|  
|**compress_snapshot**|**bit**|指定に書き込まれたスナップショット、 *alt_snapshot_folder*の場所を圧縮するには、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 形式です。 **0**スナップショットを圧縮しないことを指定します。|  
|**ftp_address**|**sysname**|ディストリビューター用 FTP サービスのネットワーク アドレス。 ディストリビューション エージェントが受け取るパブリケーション スナップショット ファイルの場所を示します。|  
|**ftp_port**|**int**|ディストリビューター用 FTP サービスのポート番号。 パブリケーションのスナップショット ファイルが取得するため、ディストリビューション エージェントの存在を指定します。|  
|**ftp_subdirectory**|**nvarchar(510)**|パブリケーションが FTP を使用してスナップショットの配布をサポートしている場合にディストリビューション エージェントはスナップショット ファイルを指定します。|  
|**ftp_login**|**nvarchar (256)**|FTP サービスへの接続に使用するユーザー名。|  
|**ftp_password**|**nvarchar(1048)**|FTP サービスへの接続に使用されるユーザー パスワード。|  
|**allow_dts**|**bit**|パブリケーションでデータを変換できるかどうかを指定します。 **1** DTS 変換が許可されることを指定します。 *非 SQL パブリッシャーに対してサポートされていません。*|  
|**allow_anonymous**|**bit**|パブリケーションに対して匿名サブスクリプションを許可するかどうかを示す、 **1**が許可されていることを意味します。|  
|**centralized_conflicts**|**bit**|競合レコードがパブリッシャーに格納されるかどうかを示します。<br /><br /> **0** = 競合レコードはパブリッシャー側の両方と、競合の原因となったサブスクライバーで格納されます。<br /><br /> **1** = 競合レコードはパブリッシャーに格納されます。<br /><br /> *非 SQL パブリッシャーに対してサポートされていません。*|  
|**conflict_retention**|**int**|競合の保有期間を日数で指定します。 *非 SQL パブリッシャーに対してサポートされていません。*|  
|**conflict_policy**|**int**|キュー更新サブスクライバー オプションを使用する場合の後に、競合解決ポリシーを指定します。 これらの値のいずれかを指定できます。<br /><br /> **1** = パブリッシャー優先します。<br /><br /> **2** = サブスクライバー優先します。<br /><br /> **3** = サブスクリプションを再初期化します。<br /><br /> *非 SQL パブリッシャーに対してサポートされていません。*|  
|**queue_type**|**int**|使用されるキューの種類。 これらの値のいずれかを指定できます。<br /><br /> **1** 、msmq を =[!INCLUDE[msCoName](../../includes/msconame-md.md)]メッセージ キューがトランザクションを格納します。<br /><br /> **2** = を使用して、sql[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]トランザクションを格納します。<br /><br /> この列は、以外では使用されません[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーです。<br /><br /> 注:使用して[!INCLUDE[msCoName](../../includes/msconame-md.md)]メッセージ キューは非推奨し、現在サポートされていません。<br /><br /> *このコラムでは、非 SQL パブリッシャーに対してはサポートされていません。*|  
|**ad_guidname**|**sysname**|パブリケーションが [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory にパブリッシュされるかどうかを示します。 有効なグローバル一意識別子 (GUID) は、パブリケーションがパブリッシュされることを指定します、[!INCLUDE[msCoName](../../includes/msconame-md.md)]が対応する Active Directory パブリケーション オブジェクトの Active Directory、および GUID **objectGUID**します。 パブリケーションがパブリッシュされません NULL の場合、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory。 *非 SQL パブリッシャーに対してサポートされていません。*|  
|**backward_comp_level**|**int**|データベースの互換性レベル。次のいずれかの値になります。<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].<br /><br /> *非 SQL パブリッシャーに対してサポートされていません。*|  
|**description**|**nvarchar (255)**|パブリケーションの説明エントリします。|  
|**independent_agent**|**bit**|このパブリケーションに対して、スタンドアロンのディストリビューション エージェントがあるかどうかを示します。<br /><br /> **0** = パブリケーションは共有ディストリビューション エージェントを使用して、パブリッシャー データベース/サブスクライバー データベースの各ペアが 1 つの共有エージェント。<br /><br /> **1** = このパブリケーション用のスタンドアロン ディストリビューション エージェントが存在します。|  
|**immediate_sync**|**bit**|同期ファイルが作成またはスナップショット エージェントを実行するたびに再作成するかどうかを示します、 **1**エージェントを実行するたびに、それらが作成されることを意味します。|  
|**allow_push**|**bit**|パブリケーションに対してプッシュ サブスクリプションを許可するかどうかを示す、 **1**が許可されていることを意味します。|  
|**allow_pull**|**bit**|パブリケーションに対してプル サブスクリプションを許可するかどうかを示す、 **1**が許可されていることを意味します。|  
|**retention**|**int**|指定したパブリケーションに対して保存する時間の変更の量。|  
|**allow_subscription_copy**|**bit**|パブリケーションにサブスクライブするサブスクリプション データベースをコピーする機能が有効かどうかを示します。 **1**コピーが許可されていることを意味します。|  
|**allow_initialize_from_backup**|**bit**|サブスクライバーでは、最初のスナップショットではなくバックアップから、このパブリケーションへのサブスクリプションを初期化できるかどうかを示します。 **1** 、バックアップからサブスクリプションを初期化できることを意味し、 **0**できないことを意味します。 詳細については、「[スナップショットを使用しないトランザクション サブスクリプションの初期化](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)」を参照してください。 *非 SQL パブリッシャーに対してサポートされていません。*|  
|**min_autonosync_lsn**|**binary(1)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**replicate_ddl**|**int**|パブリケーションに対してスキーマ レプリケーションがサポートされているかどうかを示します。 **1** 、パブリッシャー側で実行される DDL ステートメントがレプリケートされることを示しますと**0** DDL ステートメントがレプリケートされないことを示します。 詳細については、「[パブリケーション データベースでのスキーマの変更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)」を参照してください。 *非 SQL パブリッシャーに対してサポートされていません。*|  
|**options**|**int**|ビットごとのオプションの値が、追加のパブリッシング オプションを指定するビットマップ。<br /><br /> **0x1** - ピア ツー ピア レプリケーションに対して有効です。<br /><br /> **0x2** -ローカル変更のみをパブリッシュします。<br /><br /> **0x4** - SQL Server 以外のサブスクライバーに対して有効です。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [syspublications&#40;システム ビュー&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/syspublications-system-view-transact-sql.md)   
 [syspublications &#40;Transact-SQL&#41;](../../relational-databases/system-tables/syspublications-transact-sql.md)  
  
  
