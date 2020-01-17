---
title: SQL Server エージェントのエラー ログの表示 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3835f83efff9e720f7f8631d527b9547e3b4239a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63245605"
---
# <a name="view-sql-server-agent-error-log-sql-server-management-studio"></a>SQL Server エージェントのエラー ログの表示 (SQL Server Management Studio)
  このトピックでは、  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]エージェントのエラー ログを表示する方法について説明します。  
  
 [ログ ファイルの表示] には、さまざまなコンポーネントのログ情報が表示されます。 [ログ ファイルの表示] が開いているときに **[ログの選択]** ペインを使用して、表示するログを選択します。 各ログには、そのログの種類に適した列が表示されます。 表示できるログ ファイルは、[ログ ファイルの表示] を開いたときの状況に応じて変わります。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   [SQL Server Management Studio を使用して SQL Server エージェントのエラー ログを表示するには](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 オブジェクト エクスプローラーに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ノードが表示されるのは、このノードの使用権限がある場合に限られます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの機能を実行するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]固定サーバー ロールの **sysadmin** のメンバーであるアカウントの資格情報を使用するように構成する必要があります。 このアカウントには、次の Windows 権限が必要です。  
  
-   サービスとしてログオン (SeServiceLogonRight)  
  
-   プロセス レベル トークンを置き換える (SeAssignPrimaryTokenPrivilege)  
  
-   スキャン チェックを行わない (SeChangeNotifyPrivilege)  
  
-   プロセスに対してメモリ クォータを調整する (SeIncreaseQuotaPrivilege)  
  
 必要な Windows 権限の詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント サービス アカウントを参照してください[のアカウント、SQL Server エージェント サービスの選択](select-an-account-for-the-sql-server-agent-service.md)と[Windows サービス アカウントの構成とアクセス許可](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)します。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
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
     選択されたログの表示を更新します。 **[更新]** ボタンをクリックすると、選択したログが対象サーバーから再度読み込まれ、それと同時にすべてのフィルター設定が適用されます。  
  
     **[フィルター]**  
     **[接続]** や **[日付]** などの **[全般]** フィルター基準を含め、ログ ファイルのフィルター選択に使用する設定を指定できるダイアログ ボックスが開きます。  
  
     **検索**  
     ログ ファイル内で特定のテキストを検索します。 ワイルドカード文字を使用した検索はサポートされません。  
  
     **[停止]**  
     ログ ファイル エントリの読み込みを停止します。 たとえば、最新のエントリのみを表示したい場合に、リモートまたはオフラインのログ ファイルの読み込みに長い時間がかかるときは、このオプションを使用することをお勧めします。  
  
     **[ログ ファイルの概要]**  
     この情報パネルには、ログ ファイルのフィルター選択の概要が表示されます。 ファイルがフィルター選択されない場合、 **"フィルターが適用されていません"** と表示されます。 ログにフィルターが適用されている場合、"**ログ エントリのフィルター条件:** \<filter criteria>" と表示されます。  
  
     **[選択した行の詳細]**  
     行を選択すると、選択されたイベント行の詳細情報がページの下部に表示されます。 列をグリッド内の別の場所にドラッグすることで、列を並べ替えることができます。 グリッドのヘッダーで列のセパレーター バーを左右にドラッグすると、列の幅を変更できます。 グリッドのヘッダーで列のセパレーター バーをダブルクリックすると、内容の長さに合わせて自動的に列の幅が調整されます。  
  
     **インスタンス**  
     イベントが発生したインスタンスの名前です。 これは、 *computer name*\\*instance name*と表示されます。  
  
     **Date**  
     イベントの日付が表示されます。  
  
     **Source**  
     サービスの名前 (たとえば MSSQLSERVER) など、イベントの作成元のソース機能が表示されます。 ログの種類によっては表示されません。  
  
     **メッセージ**  
     イベントに関連付けられているメッセージがすべて表示されます。  
  
     **[ログの種類]**  
     イベントが属するログの種類が表示されます。 [ログ ファイルの概要] ウィンドウには、選択したログがすべて表示されます。  
  
     **[ログ ソース]**  
     イベントがキャプチャされているソース ログの説明が表示されます。  
  
5.  完了したら、 **[閉じる]** をクリックします。  
  
  
