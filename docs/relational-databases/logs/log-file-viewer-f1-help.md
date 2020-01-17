---
title: '[ログ ファイルの表示] の F1 ヘルプ | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
f1_keywords:
- sql13.swb.configurelogs.errorlog.f1
helpviewer_keywords:
- Log File Viewer
ms.assetid: 2243845c-4880-4aa0-9ee8-0a97a128996b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a507bd5425686e7a33a8bbf49e6c8669effed031
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084093"
---
# <a name="log-file-viewer-f1-help"></a>[ログ ファイルの表示] の F1 ヘルプ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [ログ ファイルの表示] には、さまざまなコンポーネントのログ情報が表示されます。 [ログ ファイルの表示] が開いているときに **[ログの選択]** ペインを使用して、表示するログを選択します。 各ログには、そのログの種類に適した列が表示されます。  
  
 表示できるログ ファイルは、[ログ ファイルの表示] を開いたときの状況に応じて変わります。 詳細については、「 [[ログ ファイルの表示] を開く](../../relational-databases/logs/open-log-file-viewer.md)」を参照してください。  
  
 監査ログの表示行数は、 **[ツール] メニューから開く [オプション]** ダイアログ ボックスの **[SQL Server オブジェクト エクスプローラー]/[コマンド]** ページで構成できます。 監査ログの表示列の詳細については、「[sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)」を参照してください。  
  
## <a name="options"></a>オプション  
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
 この情報パネルには、ログ ファイルのフィルター選択の概要が表示されます。 ファイルがフィルター選択されない場合、 **"フィルターが適用されていません"** と表示されます。 ログにフィルターが適用されている場合、"**ログ エントリのフィルター条件:** \<filter criteria>" と表示されます。  
  
 **[選択した行の詳細]**  
 行を選択すると、選択されたイベント行の詳細情報がページの下部に表示されます。 列をグリッド内の別の場所にドラッグすることで、列を並べ替えることができます。 グリッドのヘッダーで列のセパレーター バーを左右にドラッグすると、列の幅を変更できます。 グリッドのヘッダーで列のセパレーター バーをダブルクリックすると、内容の長さに合わせて自動的に列の幅が調整されます。  
  
 **インスタンス**  
 イベントが発生したインスタンスの名前です。 これは、 *computer name*\\*instance name*と表示されます。  
  
## <a name="frequently-displayed-columns"></a>表示頻度の高い列  
 **[日付]**  
 イベントの日付が表示されます。  
  
 **ソース**  
 サービスの名前 (たとえば MSSQLSERVER) など、イベントの作成元のソース機能が表示されます。 ログの種類によっては表示されません。  
  
 **メッセージ**  
 イベントに関連付けられているメッセージがすべて表示されます。  
  
 **[ログの種類]**  
 イベントが属するログの種類が表示されます。 [ログ ファイルの概要] ウィンドウには、選択したログがすべて表示されます。  
  
 **[ログ ソース]**  
 イベントがキャプチャされているソース ログの説明が表示されます。  
  
## <a name="permissions"></a>アクセス許可  
 オンラインの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのログ ファイルにアクセスするには、securityadmin 固定サーバー ロールのメンバーシップが必要です。  
  
 オフラインの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのログ ファイルにアクセスするには、 **Root\Microsoft\SqlServer\ComputerManagement10** WMI 名前空間、およびログ ファイルの保存されているフォルダーの両方に対する読み取りアクセス権が必要です。 詳細については、「 [オフライン ログ ファイルの表示](../../relational-databases/logs/view-offline-log-files.md)」トピックの「セキュリティ」セクションを参照してください。  
  
## <a name="see-also"></a>参照  
 [ログ ファイルの表示](../../relational-databases/logs/log-file-viewer.md)   
 [[ログ ファイルの表示] を開く](../../relational-databases/logs/open-log-file-viewer.md)   
 [オフライン ログ ファイルの表示](../../relational-databases/logs/view-offline-log-files.md)  
  
  
