---
title: '[データベースのバックアップ] ([全般] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.backupdatabase.general.f1
ms.assetid: 5c344dfd-1ad3-41cc-98cd-732973b4a162
caps.latest.revision: 59
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 025d5eac30815b6d9110dcca7214e7e88412a23d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37290958"
---
# <a name="back-up-database-general-page"></a>[データベースのバックアップ] \([全般] ページ)
  **[データベースのバックアップ]** ダイアログ ボックスの **[全般]** ページでは、データベースのバックアップ操作の設定を表示または変更できます。  
  
 バックアップの基本的な概念については、「[バックアップの概要 &#40;SQL Server&#41;](backup-overview-sql-server.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用してバックアップ タスクを指定する場合、 [!INCLUDE[tsql](../../includes/tsql-md.md)][[スクリプト]](/sql/t-sql/statements/backup-transact-sql) ボタンをクリックしてスクリプトの保存先を選択することにより、対応する **BACKUP** スクリプトを生成できます。  
  
 **SQL Server Management Studio を使用してバックアップを作成するには**  
  
-   [データベースの完全バックアップの作成 &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [データベースの差分バックアップの作成 &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
    > [!IMPORTANT]  
    >  データベース メンテナンス プランを定義して、データベース バックアップを作成できます。 詳細については、 [オンライン ブックの「](http://msdn.microsoft.com/library/ms187658.aspx) メンテナンス プラン [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 」を参照してください。  
  
 **部分バックアップを作成するには**  
  
-   部分バックアップを作成するには、 [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](/sql/t-sql/statements/backup-transact-sql) ステートメントで PARTIAL オプションを使用する必要があります。  
  
## <a name="options"></a>および  
  
### <a name="source"></a>Source  
 **[ソース]** パネルのオプションでは、データベースを特定し、バックアップ操作のバックアップの種類とコンポーネントを指定します。  
  
 **[データベース]**  
 バックアップするデータベースを選択します。  
  
 **復旧モデル**  
 選択したデータベースで表示される復旧モデル (SIMPLE、FULL、または BULK_LOGGED) を表示します。  
  
 **[バックアップの種類]**  
 指定したデータベースで実行するバックアップの種類を選択します。  
  
|[バックアップの種類]|適用対象|制限|  
|-----------------|-------------------|------------------|  
|[完全]|データベース、ファイル、ファイル グループ|**master** データベースでは、完全バックアップのみ可能です。<br /><br /> SIMPLE (単純) 復旧モデルの場合、ファイルおよびファイル グループのバックアップは読み取り専用ファイル グループについてのみ実行できます。|  
|[差分]|データベース、ファイル、ファイル グループ|SIMPLE (単純) 復旧モデルの場合、ファイルおよびファイル グループのバックアップは読み取り専用ファイル グループについてのみ実行できます。|  
|トランザクション ログ|トランザクション ログ|トランザクション ログ バックアップは、単純復旧モデルでは使用できません。|  
  
 **[バックアップのみコピーする]**  
 コピーのみのバックアップを作成する場合に選択します。 *コピーのみのバックアップ*は、従来の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップのシーケンスから独立した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップです。 詳細については、「[コピーのみのバックアップ &#40;SQL Server&#41;](copy-only-backups-sql-server.md)」を参照してください。  
  
> [!NOTE]  
>  **[差分]** オプションが選択されている場合、コピーのみのバックアップは作成できません。  
  
 **[バックアップ コンポーネント]**  
 バックアップするデータベース コンポーネントを選択します。 **[バックアップの種類]** ボックスの一覧で **[トランザクション ログ]** を選択した場合は、このオプションを設定できません。  
  
 次のいずれかのオプション ボタンをクリックします。  
  
|||  
|-|-|  
|**[データベース]**|データベース全体がバックアップされるように指定します。|  
|**[ファイルおよびファイル グループ]**|指定したファイルやファイル グループがバックアップされるように指定します。<br /><br /> このオプションをクリックすると、 **[ファイルおよびファイル グループの選択]** ダイアログ ボックスが表示されます。 バックアップするファイル グループまたはファイルを選択して **[OK]** をクリックすると、選択した項目が **[ファイルおよびファイル グループ]** ボックスに表示されます。|  
  
### <a name="destination"></a>[Destination]  
 **[バックアップ先]** パネルのオプションでは、バックアップ操作で使用するバックアップ デバイスの種類を指定して、既存の論理バックアップ デバイスまたは物理バックアップ デバイスを検索できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップ デバイスの詳細については、「[バックアップ デバイス &#40;SQL Server&#41;](backup-devices-sql-server.md)」を参照してください。  
  
 **[バックアップ先]**  
 バックアップ先のメディアの種類を、次の中から 1 つ選択します。 選択したバックアップ先が、 **[バックアップ先]** 一覧に表示されます。  
  
|||  
|-|-|  
|**[ディスク]**|ディスクにバックアップします。 データベース用に作成されたシステム ファイルやディスク ベースの論理バックアップ デバイスを指定する場合もあります。 現在選択されているディスクが、 **[バックアップ先]** 一覧に表示されます。 バックアップ操作には最大 64 台のディスク デバイスを選択できます。|  
|**Tape**|テープにバックアップします。 データベース用に作成されたローカル テープ ドライブやテープ ベースの論理バックアップ デバイスを指定する場合もあります。 現在選択されているテープが、 **[バックアップ先]** リストに表示されます。 最大数は 64 です。 サーバーにテープ デバイスが接続されていない場合、このオプションは無効になります。 選択したテープが **[バックアップ先]** 一覧に表示されます。<br /><br /> 注: テープ バックアップ デバイスは、将来のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でサポートされなくなる予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。|  
|**URL**|Windows Azure BLOB ストレージにバックアップします。|  
  
 次に示すオプションの表示は、選択したバックアップ先の種類によって異なります。 [ディスク] または [テープ] を選択すると、次のオプションが表示されます。  
  
 **[追加]**  
 ファイルまたはデバイスを **[バックアップ先]** 一覧に追加します。 ローカル ディスクまたはリモート ディスクの最大 64 個のデバイスで同時にバックアップできます。 リモート ディスクのファイルを指定するには、完全修飾の汎用名前付け規則 (UNC) 名を使用してください。 詳細については、「 [バックアップ デバイス &#40;SQL Server&#41;](backup-devices-sql-server.md))。  
  
 **[削除]**  
 **[バックアップ先]** 一覧から、現在選択されているデバイスを削除します。  
  
 **目次**  
 選択したデバイスのメディア コンテンツを表示します。  
  
 バックアップ先として [URL] を選択すると、次のオプションが表示されます。  
  
 **[ファイル名]**  
 バックアップ ファイルの名前を指定します。  
  
 **SQL 資格情報**  
 Windows Azure ストレージへの認証に使用する SQL 資格情報を選択します。 使用できる既存の SQL 資格情報がない場合は、 **[作成]** ボタンをクリックして新しい SQL 資格情報を作成します。  
  
> [!IMPORTANT]  
>  **[作成]** をクリックすると開くダイアログでは、サブスクリプションの管理証明書または公開プロファイルが求められます。 管理証明書または公開プロファイルにアクセスできない場合は、Transact-SQL または SQL Server Management Studio を使用してストレージ アカウント名とアクセス キーの情報を指定し、SQL 資格情報を作成することができます。 サンプル コードを参照してくださいで、[資格情報を作成する](../security/authentication-access/create-a-credential.md#Credential)Transact SQL を使用して資格情報を作成するトピック。 または SQL Server Management Studio を使用して、データベース エンジン インスタンスから、 **[セキュリティ]** を右クリックし、 **[新規作成]**、 **[資格情報]** の順にクリックします。 **[ID]** にストレージ アカウント名、 **[パスワード]** にアクセス キーを指定します。  
  
 **[Azure ストレージ コンテナー]**  
 Windows Azure ストレージ コンテナーの名前を指定します。  
  
 **[URL プレフィックス]**  
 これは、SQL 資格情報に格納されているストレージ アカウント情報と、指定した Azure ストレージ コンテナー名に基づいて自動的に生成されます。 **\<storage account>.blob.core.windows.net** 以外の形式を使ったドメインを使用している場合を除き、このフィールドの情報は編集しないことをお勧めします。  
  
## <a name="see-also"></a>参照  
 [トランザクション ログのバックアップ &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)   
 [ファイルおよびファイル グループのバックアップ &#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)   
 [ディスク ファイルの論理バックアップ デバイスの定義 &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [テープ ドライブの論理バックアップ デバイスの定義 &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [復旧モデル &#40;SQL Server&#41;](recovery-models-sql-server.md)  
  
  