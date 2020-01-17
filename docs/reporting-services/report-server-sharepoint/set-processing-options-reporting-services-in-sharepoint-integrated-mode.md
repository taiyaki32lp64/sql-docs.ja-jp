---
title: 処理オプションの設定 (Reporting Services の SharePoint 統合モード) | Microsoft Docs
ms.date: 10/05/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 986ae6e89727b0cef59e4d6b3bf7e5d92bd5342b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580546"
---
# <a name="set-processing-options-reporting-services-in-sharepoint-integrated-mode"></a>処理オプションの設定 (Reporting Services の SharePoint 統合モード)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Reporting Services レポートの処理オプションを設定することにより、データ処理のタイミングを決定することができます。 また、レポート処理のタイムアウト値や、現在のレポートでレポート履歴を有効にするかどうかを決定するオプションも設定できます。  
  
-   レポートが予定外に (たとえば、スケジュールされたバックアップ中に) 実行されないように、レポートをレポート スナップショットとして実行することができます。 レポート スナップショットは、通常はスケジュールに従って作成され、その後更新されます。これによって、正確な時間でレポートとデータ処理を行うことができます。 レポートが実行に長時間かかるクエリに基づいている場合や、クエリに使用されているデータのデータ ソースが、ある一定時間の間アクセスを避けたいものである場合は、レポートをスナップショットとして実行してください。  
  
-   レポート サーバーでは、処理済みレポートのコピーをキャッシュして、ユーザーがレポートを開いたときにそのコピーを返すことができます。 キャッシュは、パフォーマンスを向上させる技法です。 レポートのサイズが大きい場合やレポートへのアクセスが頻繁に行われる場合、キャッシュを行うことでレポートの取得にかかる時間を短縮できます。  
  
-   レポート履歴は、以前実行したレポートの一連のコピーです。 レポート履歴を使用すると、長期にわたりレポートの記録を管理できます。 秘密情報または個人データを含むレポートは、レポート履歴の対象ではありません。 このため、レポート履歴に含めることができるのは、レポートを実行するすべてのユーザーが使用できる資格情報 (格納された資格情報、または自動的にレポートを実行するために使用する資格情報のいずれか) でデータ ソースへのクエリを行うレポートのみです。  

    Reporting Services の統合では、SharePoint のコンテンツのチェックアウトおよびチェックイン管理機能を使用して、Reporting Services のコンテンツの種類への更新を保存します。 これには、レポート スナップショットの作成が含まれます。 したがって、ドキュメント ライブラリでのバージョン管理を有効にしている場合は、新しいレポート履歴スナップショットが作成されたときに、レポート バージョンが更新されます。 この動作は、スナップショットの更新による副作用です。 スナップショットが更新されると、レポートの LastExecution プロパティが変更され、それによってレポートのバージョンが変更されます。  

-   タイムアウト値を指定して、システム リソースの使用に制限を設定できます。  

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。

## <a name="set-data-refresh-options"></a>データ更新オプションの設定
  
1.  ライブラリ内のレポートをポイントします。  
  
2.  下矢印をクリックし、 **[処理の管理のオプション]** をクリックします。  
  
3.  **[データ更新オプション]** で、 **[スナップショット データを使用する]** をクリックします。 "データ ソースの資格情報が保存されていないため、このレポートをスナップショットから実行できません。" と表示される場合は、レポートが自動実行されるように構成されていないため、このオプションを設定する前に、保存されている資格情報が使用されるようにデータ ソースを変更する必要があります。  
  
4.  **[データ スナップショットのオプション]** で、 **[データ処理をスケジュールする]** を選択します。  
  
5.  使用できる既存の共有スケジュールがあれば、 **[次の共有スケジュールで実行する]** をクリックします。それ以外の場合は、 **[カスタム スケジュールで実行する]** をクリックし、 **[構成]** をクリックします。  
  
6.  頻度、スケジュール、および開始日と終了日を選択し、 **[OK]** をクリックします。  
  
7.  スケジュールされたデータ処理の実行を待たずに、直ちにスナップショット データを作成してレポートに使用する必要がある場合は、 **[データ スナップショットのオプション]** で **[このページを保存するときにスナップショットを作成または更新する]** を選択します。  
  
## <a name="set-report-caching-options"></a>レポートのキャッシュ オプションの設定
  
1.  ライブラリ内のレポートをポイントします。  
  
2.  下矢印をクリックし、 **[処理の管理のオプション]** をクリックします。  
  
3.  **[データ更新オプション]** で、 **[キャッシュ データを使用する]** をクリックします。 "1 つ以上のデータ ソース資格情報が保存されていないため、このレポートをキャッシュできません。" と表示される場合は、レポートが自動実行されるように構成されていないため、このオプションを設定する前に、保存されている資格情報が使用されるようにデータ ソースを変更する必要があります。  
  
4.  **[キャッシュ オプション]** で、キャッシュの有効期限を次のように指定します。  
  
    -   キャッシュの有効期限が切れるまでの時間を分単位で入力します。  
  
    -   スケジュールで指定した時刻にキャッシュを消去するには、共有スケジュールを使用します。  
  
    -   指定した時刻にキャッシュを消去するには、カスタム スケジュールを作成します。  
  
## <a name="set-processing-time-out-values"></a>処理のタイムアウト値の設定
  
1.  ライブラリ内のレポートをポイントします。  
  
2.  下矢印をクリックし、 **[処理の管理のオプション]** をクリックします。  
  
3.  レポート サーバー レベルで指定された値を使用する必要がある場合は、 **[処理のタイムアウト]** で **[サイトの既定の設定を使用する]** をクリックします。 タイムアウトなしにするか、別のタイムアウト値にオーバーライドする必要がある場合は、 **[レポート処理をタイムアウトしない]** または **[レポート処理を次の時間 (秒) に制限する]** を選択します。  
  
## <a name="set-report-history-options-and-limits"></a>レポート履歴のオプションと制限数の設定
  
1.  ライブラリ内のレポートをポイントします。  
  
2.  下矢印をクリックし、 **[処理の管理のオプション]** をクリックします。  
  
3.  **[履歴スナップショットのオプション]** で、データ処理を実行して保存する方法とタイミングを指定します。  
  
4.  レポート サーバー レベルで指定された値を使用する場合は、 **[履歴スナップショットの制限]** で **[サイトの既定の設定を使用する]** をクリックします。 それ以外の場合は、 **[スナップショット数を制限しない]** を選択するか、 **[スナップショットを次の数に制限する]** でカスタム値を指定します。  
  
## <a name="set-database-timeout"></a>データベースのタイムアウトを設定する
  
*  Windows PowerShell を使用すると、SharePoint レポート サーバーのデータベースのタイムアウト値を設定できます。 詳細については、「[Reporting Services SharePoint モード用の PowerShell コマンドレット](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)」の「Reporting Service アプリケーション データベースのプロパティの取得と設定」セクションを参照してください。  
  
## <a name="next-steps"></a>次の手順

 [レポート処理プロパティの設定](../../reporting-services/report-server/set-report-processing-properties.md)   
 [レポートのキャッシュ](../../reporting-services/report-server/caching-reports-ssrs.md)   
 [レポートおよび共有データセット処理のタイムアウト値の設定](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
