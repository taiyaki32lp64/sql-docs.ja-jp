---
title: サブスクリプションと配信 (Reporting Services) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], report distribution
- reports [Reporting Services], distributing
- distributing reports [Reporting Services]
- published reports [Reporting Services], distributing
- sending reports
- sharing reports
- delivering reports [Reporting Services]
- distributing reports [Reporting Services], subscriptions
- subscriptions [Reporting Services], about subscriptions
- subscriptions [Reporting Services]
ms.assetid: be7ec052-28e2-4558-bc09-8479e5082926
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: fd9288a630dd24dd8d79deef184cfc4c4fabcd9f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65578039"
---
# <a name="subscriptions-and-delivery-reporting-services"></a>サブスクリプションと配信 (Reporting Services)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サブスクリプションは、特定の時刻で、またはイベントへの応答として、指定されたファイル形式でレポートを配信する構成です。 たとえば、毎週水曜日に、MonthlySales.rdl レポートを Microsoft Word 文書としてファイル共有に保存します。 サブスクリプションを使用して、レポート配信のスケジュールや自動化を設定したり、レポート パラメーターの特定の値セットを指定したりすることができます。  
  
 1 つのレポートに複数のサブスクリプションを作成して、サブスクリプションのオプションを変更することができます。たとえば、異なるパラメーター値を指定して、西部地域の売上レポート、東部地域の売上レポート、全地域の売上レポートのように、3 つのバージョンのレポートを作成できます。  
  
 ![ssrs サブスクリプション フローの例](../../reporting-services/subscriptions/media/ssrs-subscription-example-flow.png "ssrs サブスクリプション フローの例")  
  
 サブスクリプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各エディションでサポートされる機能の一覧については、「[SQL Server 2017 の各エディションとサポートされている機能](../../sql-server/editions-and-components-of-sql-server-2017.md)」をご覧ください。  
  
 **このトピックの内容:**  
  
-   [サブスクリプションおよび配信のシナリオ](#bkmk_subscription_scenarios)  
  
-   [標準のサブスクリプションとデータ ドリブン サブスクリプション](#bkmk_standard_and_datadriven)  
  
-   [サブスクリプションの要件](#bkmk_subscription_requirements)  
  
-   [配信拡張機能](#bkmk_delivery_extensions)  
  
-   [サブスクリプションの要素](#bkmk_parts_of_subscription)  
  
-   [サブスクリプションの処理方法](#bkmk_subscription_processing)  
  
-   [サブスクリプションのプログラムによる制御](#bkmk_code)  
  
 **このセクションのトピック:**  
  
-   [Reporting Services の電子メール配信](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md) 。レポート サーバーのファイル共有の配信操作および構成について説明します。  
  
-   [ネイティブ モード レポート サーバーのサブスクリプションの作成と管理](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md) ネイティブ モードのレポート サーバーでサブスクリプションを作成するための詳細な手順です。  
  
-   [SharePoint モード レポート サーバーのサブスクリプションの作成と管理](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md) SharePoint モードのレポート サーバーでサブスクリプションを作成するための詳細な手順です。  
  
-   [File Share Delivery in Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md) レポート サーバーのファイル共有の配信操作および構成について説明します。  
  
-   [Disable or Pause Report and Subscription Processing](../../reporting-services/subscriptions/disable-or-pause-report-and-subscription-processing.md)。  
  
-   [SharePoint Library Delivery in Reporting Services](../../reporting-services/subscriptions/sharepoint-library-delivery-in-reporting-services.md) SharePoint ライブラリへのサブスクリプションの配信について説明します。  
  
-   [データ ドリブン サブスクリプション](../../reporting-services/subscriptions/data-driven-subscriptions.md) 実行時にレポート出力をカスタマイズする際のデータ ドリブン サブスクリプションの使用に関する情報を記載しています。  
  
-   [Reporting Services のサブスクリプションを監視する](../../reporting-services/subscriptions/monitor-reporting-services-subscriptions.md)  
  
-   [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
  
##  <a name="bkmk_subscription_scenarios"></a> サブスクリプションおよび配信のシナリオ  
 サブスクリプションごとに配信オプションを構成し、使用可能なオプションは選択する配信拡張機能によって決まります。 配信拡張機能は、いくつかの配信方法をサポートするモジュールです。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には複数の配信拡張機能が含まれており、配信拡張機能はサード パーティ ベンダーから利用できる可能性があります。  
  
 開発者は、その他のシナリオをサポートするために、カスタムの配信拡張機能を作成できます。 詳しくは、「 [Implementing a Delivery Extension](../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)」をご覧ください。  
  
 一般的な [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サブスクリプションのシナリオを、以下の表に示します。  
  
|シナリオ|[説明]|  
|--------------|-----------------|  
|電子メールでレポートを送信する|個々のユーザーおよびグループにレポートを電子メールで送信します。 サブスクリプションを作成し、配布するレポートを受信するグループの別名または電子メールの別名を指定します。 実行時に [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] によってサブスクリプション データが決定されるようにすることができます。 変化するメンバーの一覧を持っているグループに同じレポートを送信する場合は、クエリを使用して、実行時にサブスクリプションの一覧を取得できます。|  
|オフラインでレポートを表示する|ユーザーは、サブスクリプション出力の形式として次のいずれかを選択できます。<br /><br /> - レポート データが含まれている XML ファイル<br />- CSV (コンマ区切り)<br />- PDF<br />- MHTML (Web アーカイブ)<br />- Microsoft Excel<br />- TIFF ファイル<br />- Microsoft Word<br /><br /> アーカイブするレポートは、夜間スケジュールでバックアップされる共有フォルダーに直接送信できます。 ブラウザーに読み込むには時間がかかりすぎる、サイズが大きなレポートは、デスクトップ アプリケーションで表示できる形式で共有フォルダーに送信できます。|  
|キャッシュを事前に読み込む|パラメーター化されたレポートの複数のインスタンスがあったり、レポートを表示するレポート ユーザーが多数存在したりする場合は、レポートをキャッシュに事前に読み込むことで、レポートの表示に必要な処理時間を短縮できます。|  
|レポートをデータ ドリブンにする|データ ドリブン サブスクリプションを使用して、実行時にレポート出力、配信オプション、およびレポート パラメーター設定をカスタマイズします。 サブスクリプションでは、クエリを使用して、実行時にデータ ソースから入力値を取得します。 データ ドリブン サブスクリプションを使用すると、サブスクリプションの処理時に決定されるサブスクライバーの一覧にレポートを送信する、文書の差し込み操作を実行できます。|  
  
##  <a name="bkmk_standard_and_datadriven"></a> 標準のサブスクリプションとデータ ドリブン サブスクリプション  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は、 **標準** および **データ ドリブン**の 2 種類のサブスクリプションをサポートします。 標準のサブスクリプションは、各ユーザーが作成して管理します。 標準のサブスクリプションは、サブスクリプションの処理中には変化しない静的な値で構成されます。 標準のサブスクリプションごとに、レポート表示オプション、配信オプション、およびレポート パラメーターのセットが 1 つ用意されます。  
  
 データ ドリブン サブスクリプションでは、外部のデータ ソースをクエリすることによって、サブスクリプション情報が実行時に取得されます。受信者、レポート パラメーター、またはアプリケーション形式を指定する値は、この外部のデータ ソースが提供します。 データ ドリブン サブスクリプションは、受信者の一覧が非常に大きい場合、または受信者ごとにレポートの出力を変更する場合に使用できます。 データ ドリブン サブスクリプションを使用するには、クエリの作成に関する専門知識を持っていて、パラメーターの使用方法を理解していることが必要です。 通常、レポート サーバー管理者が、これらのサブスクリプションを作成して管理します。 詳細については、以下を参照してください。  
  
-   [データ ドリブン サブスクリプション](../../reporting-services/subscriptions/data-driven-subscriptions.md)  
  
-   [データ ドリブン サブスクリプションの作成 &#40;SSRS チュートリアル&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
  
##  <a name="bkmk_subscription_requirements"></a> サブスクリプションの要件  
 レポートに対するサブスクリプションを作成する前に、以下の必要条件を満たす必要があります。  
  
|要件|[説明]|  
|-----------------|-----------------|  
|アクセス許可|レポートへのアクセス権は必須です。 レポートをサブスクライブするには、レポートを表示する権限が必要です。<br /><br /> ネイティブ モードのレポート サーバーでは、次のロールの割り当てがサブスクリプションに影響します。<br /><br /> -   "個別のサブスクリプションを管理" タスクでは、ユーザーが特定のレポートのサブスクリプションを作成、変更、および削除できます。 定義済みのロールである閲覧者ロールとレポート ビルダー ロールには、このタスクが含まれています。 このタスクを含むロールの割り当てを使用すると、ユーザーは自分が作成するサブスクリプションのみを管理できます。<br />-   "すべてのサブスクリプションを管理" タスクでは、ユーザーがすべてのサブスクリプションにアクセスしてそれらを変更できます。 このタスクは、データ ドリブン サブスクリプションを作成する場合に必要です。 定義済みのロールでは、コンテンツ マネージャー ロールにのみ、このタスクが含まれます。|  
|格納された資格情報|サブスクリプションを作成するには、レポートが保存された資格情報を使用するか、または実行時にデータを取得するために資格情報を使用しないことが必要です。 現在のユーザーの資格情報の権限借用や委任を使用して外部データ ソースに接続するように構成されているレポートは、サブスクライブすることはできません。 保存された資格情報は、Windows アカウントまたはデータベース ユーザー アカウントのいずれかです。 詳細については、「 [レポート データ ソースに関する資格情報と接続情報を指定する](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)」を参照してください。<br /><br /> レポートを閲覧するための権限のほか、各サブスクリプションを作成するための権限を所有していることが必要です。 レポート サーバーでは、 **[定期的なイベントおよびレポート配信]** が有効になっている必要があります。 詳細については、「 [ネイティブ モード レポート サーバーのサブスクリプションの作成と管理](https://msdn.microsoft.com/7f46cbdb-5102-4941-bca2-5e0ff9012c6b)」を参照してください。|  
|レポート内のユーザー依存の値|標準的なサブスクリプションに限り、ユーザー アカウント情報をフィルターに組み込んだレポートや、レポートに表示されるテキストとしてのレポートのサブスクリプションを作成できます。 レポートでは、現在のユーザーとして解釈される **User!UserID** 式を使用して、ユーザー アカウント名を指定します。 サブスクリプションを作成する時点では、サブスクリプションを作成するユーザーが現在のユーザーとして想定されます。|  
|モデル アイテム セキュリティは無効|モデルにモデル アイテム セキュリティの設定が含まれている場合、データ ソースとしてモデルを使用するレポート ビルダー レポートをサブスクライブすることはできません。 この制限は、モデル アイテム セキュリティを使用するレポートのみが対象となります。|  
|パラメーターの値|レポートでパラメーターを使用する場合、レポート自体または定義するサブスクリプションでパラメーター値を指定する必要があります。 レポートで既定値が定義されている場合は、パラメーター値でその既定値を使用するように設定できます。|  
  
##  <a name="bkmk_delivery_extensions"></a> 配信拡張機能  
 サブスクリプションは、レポート サーバーに展開された配信拡張機能を使用して、サーバーで処理されます。 既定では、共有フォルダーまたは電子メール アドレスにレポートを送信するサブスクリプションを作成できます。 レポート サーバーが SharePoint 統合モード用に構成されている場合は、レポートを SharePoint ライブラリに送信することもできます。  
  
 ユーザーがサブスクリプションを作成するとき、レポートの配信方法を決定するために、利用可能な配信拡張機能の 1 つを選択できます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、次の配信拡張機能があります。  
  
|配信拡張機能|[説明]|  
|------------------------|-----------------|  
|Windows ファイル共有|レポートを静的なアプリケーション ファイルとして、ネットワーク上の共有フォルダーに配信します。|  
|電子メール|通知またはレポートを、電子メールの添付ファイルまたは URL リンクとして配信します。|  
|SharePoint ライブラリ|SharePoint サイトからアクセスできる SharePoint ライブラリに対し、レポートを静的なアプリケーション ファイルとして配信します。 このサイトは、SharePoint 統合モードで実行されたレポート サーバーと統合されている必要があります。|  
|[Null]|NULL 配信プロバイダーは、特殊な用途向けの配信拡張機能です。表示する準備が整った、パラメーター化されたレポートを事前にキャッシュする場合に使用されます。ユーザーが個別のサブスクリプションでこの方法を使用することはできません。 NULL 配信は、データ ドリブン サブスクリプションで、事前にデータをキャッシュすることによってレポート サーバーのパフォーマンスを向上させるために管理者が使用します。|  
  
> [!NOTE]  
>  レポート配信は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アーキテクチャの拡張可能な部分です。 サード パーティ ベンダーが作成したカスタム配信拡張機能を使用して、レポートを別の場所やデバイスに送信することができます。 カスタム配信拡張機能の詳細については、「 [Implementing a Delivery Extension](../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)」を参照してください。  
  
##  <a name="bkmk_parts_of_subscription"></a> サブスクリプションの要素  
 サブスクリプション定義は、以下の要素で構成されています。  
  
-   自動的に実行できるレポート (つまり、格納された資格情報を使用するか、資格情報を使用しないレポート) へのポインター。  
  
-   配信方法 (たとえば電子メール) および配信モード (たとえば電子メール アドレス) の設定。  
  
-   特定の形式でレポートを表示する表示拡張機能。  
  
-   サブスクリプションを処理する条件。この条件は、イベントとして示されます。  
  
     通常、レポートを実行する条件は時間ベースです。 たとえば、特定のレポートを火曜日の午後 3:00 (UTC) に実行できます。 (UTC)。 ただし、レポートをスナップショットとして実行している場合は、スナップショットが更新されたときに常に実行するようにサブスクリプションを指定できます。  
  
-   レポートの実行時に使用するパラメーター。  
  
     パラメーターは省略可能で、パラメーター値を許可するレポートにのみ指定されます。 通常、サブスクリプションはユーザーが所有しているので、指定されるパラメーター値はサブスクリプションごとに異なります。 たとえば、異なる部門の営業部長は、それぞれ所属する部門のデータを返すパラメーターを使用します。 すべてのパラメーターで値が明示的に定義されているか、有効な既定値が定義されている必要があります。  
  
 サブスクリプション情報は、個別のレポートと共にレポート サーバー データベースに格納されます。 サブスクリプションが関連付けられているレポートから切り離して、サブスクリプションを管理することはできません。 説明やその他のカスタム テキスト、またはその他の要素を含むようにサブスクリプションを拡張することはできない点に注意してください。 サブスクリプションには、以前に一覧表示したアイテムのみを含めることができます。  
  
##  <a name="bkmk_subscription_processing"></a> サブスクリプションの処理方法  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、レポートのスケジュールを設定してユーザーに配信するための機能を提供する、スケジュールおよび配信のプロセッサ機能が含まれています。 レポート サーバーでは常時イベントが監視され、イベントに応答しています。 サブスクリプションに定義されている条件を満たすイベントが発生すると、サブスクリプションが読み取られ、レポートの処理方法と配信方法が決定されます。 レポート サーバーは、サブスクリプションに指定されている配信拡張機能を要求します。 配信拡張機能を実行すると、サブスクリプションから配信情報が抽出され、処理を行うため配信拡張機能に渡されます。  
  
 サブスクリプションに定義されている形式に従ってレポートが生成され、指定した送信先にレポートまたは通知が配信されます。 レポートを配信できない場合、レポート サーバーのログ ファイルにエントリが記録されます。 再試行の操作を実行できるようにする場合、最初の配信が失敗したときにもう一度配信を試みるようにレポート サーバーを構成できます。  
  
### <a name="processing-a-standard-subscription"></a>標準のサブスクリプション処理  
 標準のサブスクリプションからは、レポートのインスタンスが 1 つ生成されます。 レポートの配信先は、単一の共有フォルダーか、サブスクリプションに指定されている複数の電子メール アドレスになります。 レポートのレイアウトおよびデータは変わりません。 パラメーターを使用する場合、標準のサブスクリプション処理ではレポートのパラメーターごとに 1 つの値が使用されます。  
  
### <a name="processing-a-data-driven-subscription"></a>データ ドリブン サブスクリプションの処理  
 データ ドリブン サブスクリプションからは、レポートのインスタンスが複数生成され、インスタンスを複数の送信先に配信できます。 サブスクライバーの結果セットからパラメーター値が渡された場合、レポートのレイアウトは変わりませんが、レポートのデータが変わる場合があります。 行セットから値が渡された場合にも、レポートをどう表示するか、およびレポートを電子メールにアタッチするのか、リンクするのかを決定する配信オプションがサブスクライバーごとに異なることがあります。  
  
 データ ドリブン サブスクリプションからは、多数の配信が生成されることがあります。 サブスクリプション クエリから返された行セットの 1 行ごとに 1 件の配信が生成されます。  
  
### <a name="report-delivery-characteristics"></a>レポート配信の特性  
 標準のサブスクリプションにより配信されるレポートは、通常は静的なレポートとして表示されます。 それらのレポートは、直前のレポート実行スナップショットを基にするか、配信を完了するための静的なレポートとして生成されます。 要求時に実行されるレポートに対してサブスクリプションの **[リンクを含める]** オプションが選択されている場合、ハイパーリンクをクリックするとレポート サーバー側でレポートが実行されます。  
  
> [!NOTE]  
>  URL として配信されるレポートはレポート サーバーに接続された状態で、表示している間に更新や削除が行われる場合があります。 サブスクリプションに対して選択する配信オプションによって、レポートを URL として配信するか、電子メール メッセージの本文に埋め込むか、または添付ファイルとして送信するかを決定します。  
  
 データ ドリブン サブスクリプションによって配信されるレポートは、サブスクリプションが処理されている間に再生成される場合があります。 レポート サーバーは、データ ドリブン サブスクリプションを完了するために、レポートまたはレポートのデータセットの特定のインスタンスをロックしません。 サブスクリプションでサブスクライバーごとに異なるパラメーターの値を使用した場合、それぞれに合わせた出力を生成するためにレポートが再生成されます。 最初のレポートのコピーが作成および配信された後で基になるデータが更新された場合、それ以後にそのレポートを受け取ったユーザーには、異なる結果セットを基にしたデータが表示されることがあります。 スナップショットとして実行されるレポートを使用すると、すべてのサブスクライバーに同じレポートのインスタンスが確実に配信されます。 ただし、スケジュールに設定されているスナップショットの更新がサブスクリプションの処理中に行われた場合、受け取るレポートのデータがユーザー間で異なることがあります。  
  
### <a name="triggering-subscription-processing"></a>サブスクリプション処理の開始  
 レポート サーバーでは、スケジュールで指定されたタイム ドリブン イベントまたはスナップショット更新イベントの 2 種類のイベントを使用して、サブスクリプション処理を開始します。  
  
 タイム ドリブン トリガーは、レポート固有のスケジュールまたは共有スケジュールを使用し、サブスクリプションが実行される日時を指定します。 要求時レポートおよびキャッシュされたレポートでは、スケジュールはトリガー オプションのみです。  
  
 スナップショット更新イベントは、レポート スナップショットのスケジュールされた更新を使用して、サブスクリプションを開始します。 レポートに設定されているレポート実行プロパティを基に、レポートが新しいデータに更新されるたびに開始されるサブスクリプションを定義できます。  
  
##  <a name="bkmk_code"></a> サブスクリプションのプログラムによる制御  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] オブジェクト モデルでは、プログラムを使用してサブスクリプションとサブスクリプションの処理を監査および制御できます。  次の例と開始方法をご覧ください。  
  
-   [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
  
-   PowerShell を使用してサブスクリプションを有効および無効にする方法の例については、「 [Disable or Pause Report and Subscription Processing](../../reporting-services/subscriptions/disable-or-pause-report-and-subscription-processing.md)」を参照してください。  
  
-   <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  
  
-   **ファイル共有アカウント**を使用するよう構成されている [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のサブスクリプションをすべて列挙する PowerShell スクリプトの例については、「[サブスクリプション設定とファイル共有アカウント &#40;構成マネージャー&#41;](../../reporting-services/install-windows/subscription-settings-and-a-file-share-account-configuration-manager.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データ ドリブン サブスクリプションの作成 &#40;SSRS チュートリアル&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)   
 [[スケジュール]](../../reporting-services/subscriptions/schedules.md)   
 [Reporting Services レポート サーバー (ネイティブ モード)](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Reporting Services のサブスクリプションを監視する](../../reporting-services/subscriptions/monitor-reporting-services-subscriptions.md)  
  
  
