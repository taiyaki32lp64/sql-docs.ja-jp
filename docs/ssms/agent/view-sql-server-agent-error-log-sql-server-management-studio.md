---
title: SQL Server エージェントのエラー ログの表示 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- viewing SQL Server Agent error logs
- displaying SQL Server Agent error logs
- SQL Server Agent, errors
- errors [SQL Server Agent]
ms.assetid: de920425-fa44-469f-b83d-49e3f97e97f4
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 08ddb38c46c565e45f4112718d5c7ca48d340aa4
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69552111"
---
# <a name="view-sql-server-agent-error-log-sql-server-management-studio"></a>View SQL Server Agent Error Log (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]エージェントのエラー ログを表示する方法について説明します。  
  
[ログ ファイルの表示] には、さまざまなコンポーネントのログ情報が表示されます。 [ログ ファイルの表示] が開いているときに **[ログの選択]** ペインを使用して、表示するログを選択します。 各ログには、そのログの種類に適した列が表示されます。 表示できるログ ファイルは、[ログ ファイルの表示] を開いたときの状況に応じて変わります。  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Restrictions"></a>制限事項と制約事項  
オブジェクト エクスプローラーに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ノードが表示されるのは、このノードの使用権限がある場合に限られます。  
  
### <a name="Security"></a>セキュリティ  
  
#### <a name="Permissions"></a>アクセス許可  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの機能を実行するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]固定サーバー ロールの **sysadmin** のメンバーであるアカウントの資格情報を使用するように構成する必要があります。 このアカウントには、次の Windows 権限が必要です。  
  
-   サービスとしてログオン (SeServiceLogonRight)  
  
-   プロセス レベル トークンを置き換える (SeAssignPrimaryTokenPrivilege)  
  
-   スキャン チェックを行わない (SeChangeNotifyPrivilege)  
  
-   プロセスに対してメモリ クォータを調整する (SeIncreaseQuotaPrivilege)  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントに必要な Windows 権限の詳細については、「 [SQL Server エージェント サービスのアカウントの選択](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) 」および「 [Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」を参照してください。  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio の使用  
  
#### <a name="to-view-the-includessnoversionincludesssnoversion-mdmd-agent-error-log"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのエラー ログを表示するには  
  
1.  **オブジェクト エクスプローラー**で、表示する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント エラー ログを含むサーバーをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[SQL Server エージェント]** を展開します。  
  
3.  プラス記号をクリックして **[エラー ログ]** フォルダーを展開します。  
  
4.  表示するエラー ログを右クリックし、 **[エージェント ログの表示]** を選択します。  
  
    **[ログ ファイルの表示 -** _サーバー名_] ダイアログ ボックスでは、次のオプションを使用できます。  
  
    **[ログの読み込み]**  
    読み込むログ ファイルを指定できるダイアログ ボックスが開きます。  
  
    **[エクスポート]**  
    **[ログ ファイルの概要]** グリッドに表示されている情報をテキスト ファイルとしてエクスポートするためのダイアログ ボックスが開きます。  
  
    **[更新]**  
    選択されたログの表示を更新します。 **[更新]** ボタンをクリックすると、選択したログがターゲット サーバーから再度読み込まれ、それと同時にすべてのフィルター設定が適用されます。  
  
    **[フィルター]**  
    **[接続]** や **[日付]** などの **[全般]** フィルター基準を含め、ログ ファイルのフィルター選択に使用する設定を指定できるダイアログ ボックスが開きます。  
  
    **検索**  
    ログ ファイル内で特定のテキストを検索します。 ワイルドカード文字を使用した検索はサポートされません。  
  
    **[停止]**  
    ログ ファイル エントリの読み込みを停止します。 たとえば、最新のエントリのみを表示したい場合に、リモートまたはオフラインのログ ファイルの読み込みに長い時間がかかるときは、このオプションを使用することをお勧めします。  
  
    **[ログ ファイルの概要]**  
    この情報パネルには、ログ ファイルのフィルター選択の概要が表示されます。 ファイルがフィルター選択されない場合、 **"フィルターが適用されていません"** と表示されます。 ログにフィルターが適用されている場合、" **ログ エントリのフィルター条件:** <filter criteria>" と表示されます。  
  
    **[選択した行の詳細]**  
    行を選択すると、選択されたイベント行の詳細情報がページの下部に表示されます。 列をグリッド内の別の場所にドラッグすることで、列を並べ替えることができます。 グリッドのヘッダーで列のセパレーター バーを左右にドラッグすると、列の幅を変更できます。 グリッドのヘッダーで列のセパレーター バーをダブルクリックすると、内容の長さに合わせて自動的に列の幅が調整されます。  
  
    **インスタンス**  
    イベントが発生したインスタンスの名前です。 これは、 *computer name*\\*instance name*と表示されます。  
  
    **Date**  
    イベントの日付が表示されます。  
  
    **ソース**  
    サービスの名前 (たとえば MSSQLSERVER) など、イベントの作成元のソース機能が表示されます。 ログの種類によっては表示されません。  
  
    **メッセージ**  
    イベントに関連付けられているメッセージがすべて表示されます。  
  
    **[ログの種類]**  
    イベントが属するログの種類が表示されます。 [ログ ファイルの概要] ウィンドウには、選択したログがすべて表示されます。  
  
    **[ログ ソース]**  
    イベントがキャプチャされているソース ログの説明が表示されます。  
  
5.  完了したら、 **[閉じる]** をクリックします。  
  
