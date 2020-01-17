---
title: PowerPivot の認証と承認 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 48230cc0-4037-4f99-8360-dadf4bc169bd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3f567da3318c7b8fff799475c638c1086613f45b
ms.sourcegitcommit: e366f702c49d184df15a9b93c2c6a610e88fa0fe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2019
ms.locfileid: "67826335"
---
# <a name="powerpivot-authentication-and-authorization"></a>PowerPivot の認証および承認
  SharePoint 2010 ファーム内で実行される PowerPivot for SharePoint の配置では、SharePoint サーバーによって提供される認証サブシステムと承認モデルを使用します。 PowerPivot 関連のすべてのコンテンツは SharePoint コンテンツ データベースに格納され、PowerPivot 関連のすべての操作はファーム内の PowerPivot 共有サービスによって実行されるので、SharePoint のセキュリティ インフラストラクチャは PowerPivot のコンテンツや操作にまで及ぶことになります。 PowerPivot データが含まれているブックを要求するユーザーは、Windows ユーザー ID に基づく SharePoint ユーザー ID を使用して認証されます。 この要求が許可されるか拒否されるかは、ブックに対する表示権限によって決まります。  
  
 セルフサービス型のデータ分析には Excel Services との統合が必要となるため、PowerPivot サーバーをセキュリティで保護する場合、Excel Services のセキュリティについても理解している必要があります。 PowerPivot データへのデータ接続があるピボットテーブルに対してユーザーがクエリを実行すると、データ接続要求が Excel Services からファームの PowerPivot サーバーに転送され、データが読み込まれます。 サーバー間のこの連携では、両方のサーバーのセキュリティ設定を構成する方法を理解している必要があります。  
  
 このトピックの特定のセクションを参照するには、次のリンクをクリックしてください。  
  
 [クラシック モード サインインを使用した Windows 認証の要件](power-pivot-authentication-and-authorization.md#bkmk_auth)  
  
 [ユーザーの承認を必要とする PowerPivot の操作](#UserConnections)  
  
 [PowerPivot データ アクセスに対する SharePoint 権限](#Permissions)  
  
 [Excel Services の PowerPivot ブックのセキュリティに関する考慮事項](#excel)  
  
##  <a name="bkmk_auth"></a> クラシック モード サインインを使用した Windows 認証の要件  
 PowerPivot for SharePoint では、SharePoint で使用できる認証オプションを縮小したオプション セットがサポートされています。 使用可能な認証オプションのうち、PowerPivot for SharePoint の配置では Windows 認証のみがサポートされます。 さらに、サインインに使用する Web アプリケーションでクラシック モードが構成されている必要があります。  
  
 Windows 認証が必要なのは、PowerPivot for SharePoint の配置の Analysis Services データ エンジンで Windows 認証のみがサポートされているためです。 Excel Services は、MSOLAP OLE DB プロバイダーを介して、NTLM または Kerberos プロトコルによって認証された Windows ユーザー ID を使用して、Analysis Services への接続を確立します。  
  
 2 番目の要件である、Web アプリケーションでのクラシック モードの認証は、PowerPivot Web サービスを確実に運用できるようにするために必要です。 Web サービスは、Web フロント エンドで実行されるコンポーネントで、ファーム内の PowerPivot for SharePoint サーバーへの HTTP リダイレクトを可能にします。 Web サービスは、サービス間の通信の要求に対応しますが、ファーム内の PowerPivot 共有サービスに自らがルーティングするデータ接続要求には対応しません。 PowerPivot データを読み込む要求は、Windows ID を使用した IIS からの認証接続でのみサポートされます。 Web アプリケーションでクラシック モードでサインインすることにより、PowerPivot Web サービスからファーム内の PowerPivot 共有サービスに接続することができます。  
  
 より一般的なデータ アクセスのシナリオ (PowerPivot データを、そのデータを表示する同じ Excel ブックから抽出する場合) にはクラシック モードのサインインは必要ありませんが、他の認証プロバイダーを使用するように構成された SharePoint Web アプリケーションでは、PowerPivot for SharePoint を使用しないでください。 使用した場合、外部データ ソースとして PowerPivot ブックにユーザーが接続しようとすると、必ず接続エラーになります。  
  
 クラシック モードのサインインを使用しないと、PowerPivot Web サービスによって処理される次の種類の要求は失敗します。  
  
-   PowerPivot データに対するファーム外からの要求 (たとえば、データ ソースが PowerPivot ブックへの SharePoint URL であるレポートをレポート デザイナーまたはレポート ビルダーで作成する場合)  
  
-   PowerPivot ブックを外部データ ソースとして使用するファーム内のクライアント アプリケーションまたはレポートからの要求 (たとえば、PowerPivot データを格納する 2 番目に公開された Excel ブックをデータ ソースとして使用し、Excel デスクトップ アプリケーションでブックを作成する場合)  
  
### <a name="how-to-check-the-authentication-provider-for-your-application"></a>アプリケーションの認証プロバイダーを確認する方法  
 新しい Web アプリケーションを作成する場合は、[新しい Web アプリケーションの作成] ページで **[クラシック モード認証]** オプションを選択する必要があります。  
  
 既存の Web アプリケーションの場合は、次の手順に従って、Windows 認証を使用するように Web アプリケーションが構成されていることを確認します。  
  
1.  サーバーの全体管理で、[アプリケーション構成の管理] の **[Web アプリケーションの管理]** をクリックします。  
  
2.  Web アプリケーションを選択します。  
  
3.  **[認証プロバイダー]** をクリックします。  
  
4.  各ゾーンに 1 つのプロバイダーがあり、既定のゾーンが Windows に設定されていることを確認します。  
  
##  <a name="UserConnections"></a> ユーザーの承認を必要とする PowerPivot の操作  
 SharePoint の承認は、PowerPivot クエリおよび PowerPivot データ処理に対するすべてのレベルのアクセスに排他的に使用されます。  
  
 Analysis Services のロールベースの承認モデルはサポートされていません。 セル、行、テーブル レベルの PowerPivot データのロールベースの承認はありません。 ブックのさまざまな部分をセキュリティで保護することによって、ブック内にある機密データへのアクセスを特定のユーザーについて許可したり、拒否したりすることはできません。 SharePoint ライブラリの Excel ブックに対する表示権限を持つユーザーは、埋め込まれた PowerPivot データをすべて使用できます。  
  
 PowerPivot for SharePoint は、次の場合に SharePoint のユーザーの権限を借用します。  
  
-   PowerPivot データベースへのデータ接続があるピボットテーブルまたはピボットグラフへのクエリ。PowerPivot サービス アプリケーションは、データを処理する PowerPivot 共有サービス インスタンスに対して、ユーザーに代わって接続を確立します。  
  
-   キャッシュまたはライブラリからの PowerPivot データの読み込み (それ以外の方法ではデータを利用できない場合)。 システムにまだ読み込まれていない PowerPivot データに対してデータ接続要求が行われた場合、[!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] インスタンスでは、SharePoint ユーザー ID を使用して、データ ソースをコンテンツ ライブラリから取得し、メモリに読み込みます。  
  
-   データ ソースの更新されたコピーをコンテンツ ライブラリのブックに保存するデータ更新操作。 この場合、実際のログオン操作は、Secure Store Service の対象アプリケーションから取得したユーザー名とパスワードを使用して実行されます。 資格情報には、PowerPivot 自動データ更新アカウント、またはデータ更新スケジュールの作成時に一緒に保存された資格情報を使用できます。 詳細については、次を参照してください[格納されている資格情報の構成の PowerPivot データ更新&#40;PowerPivot for SharePoint&#41; ](../configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)と[PowerPivot 自動データ更新アカウントを構成する&#40;。PowerPivot for SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)します。  
  
##  <a name="Permissions"></a> PowerPivot データ アクセスに対する SharePoint 権限  
 PowerPivot ブックのパブリッシュ、管理、およびセキュリティでの保護は、SharePoint 統合を通じてのみサポートされます。 SharePoint サーバーは、データへの正当なアクセスを確保する認証サブシステムと承認サブシステムを提供します。 SharePoint ファーム外に PowerPivot ブックを安全に配置するシナリオはサポートされていません。  
  
 サーバー上では、PowerPivot データへの表示権限以上のユーザー アクセスは、読み取り専用です。 投稿権限では、ファイルを追加および編集できます。 PowerPivot データを変更するには、PowerPivot for Excel がインストールされている Excel デスクトップ アプリケーションにブックをダウンロードする必要があります。 ファイルに対する投稿権限があるかどうかにより、ユーザーがファイルをローカル コンピューターにダウンロードして、変更内容を再び SharePoint に保存することができるかどうかが決まります。  
  
 つまり、投稿および表示のみのレベルの権限によって、PowerPivot データへのユーザー アクセスに対する有効な権限セットが定義されます。 その他の権限レベルは、その権限レベルに投稿および表示のみと同じ権限がある場合にその範囲内で機能します (たとえば、読み取り権限には表示のみ権限が含まれるので、読み取りに割り当てられているユーザーは表示のみと同じアクセス レベルを持ちます)。  
  
 次の表に、PowerPivot データやサーバー操作へのアクセスを決定する権限レベルを要約します。  
  
|権限レベル|許可されるタスク|  
|----------------------|------------------------|  
|ファームまたはサービス管理者|サービスおよびアプリケーションをインストール、有効化、および構成します。<br /><br /> PowerPivot 管理ダッシュボードを使用し、管理レポートを表示します。|  
|フル コントロール|サイト コレクション レベルで PowerPivot 機能統合をアクティブ化します。<br /><br /> PowerPivot ギャラリー ライブラリを作成します。<br /><br /> データ フィード ライブラリを作成します。|  
|投稿|PowerPivot ブックを追加、編集、削除、およびダウンロードします。<br /><br /> データ更新を構成します。<br /><br /> SharePoint サイトで PowerPivot ブックに基づいて新しいブックやレポートを作成します。<br /><br /> データ フィード ライブラリにデータ サービス ドキュメントを作成します。|  
|Read|ブックの URL は (たとえば、Excel のデータ接続ウィザード) での接続 ダイアログ ボックスで明示的に入力されている、外部データ ソースとして PowerPivot ブックにアクセスします。|  
|表示のみ|PowerPivot ブックを表示します。<br /><br /> データ更新履歴を表示します。<br /><br /> ローカル ブックを SharePoint サイト上の PowerPivot ブックに接続し、そのデータの用途を変更します。<br /><br /> ブックのスナップショットをダウンロードします。 スナップショットは、スライサー、フィルター、式、またはデータ接続を含まない、データの静的なコピーです。 スナップショットの内容は、ブラウザー ウィンドウからのセル値のコピーに似ています。|  
  
##  <a name="excel"></a> Excel Services の PowerPivot ブックのセキュリティに関する考慮事項  
 PowerPivot のサーバー側クエリ処理は、Excel サービスと密接に結び付いています。 製品の統合は、ドキュメント レベルで開始されます。PowerPivot ブックは、PowerPivot データを含んでいるか、参照している Excel ブック (.xlsx) ファイルです。 PowerPivot ブック用の個別のファイル拡張子はありません。  
  
 PowerPivot ブックを SharePoint サイトで開くと、Excel Services は PowerPivot の埋め込みデータ接続文字列を読み取り、要求をローカルの SQL Server Analysis Services OLE DB プロバイダーに転送します。 プロバイダーは、この接続情報をファーム内の PowerPivot サーバーに渡します。 要求が 2 つのサーバー間でシームレスに流れるには、PowerPivot for SharePoint により要求される設定を使用するように Excel Services を構成する必要があります。  
  
 Excel Services では、セキュリティ関連の構成設定は信頼できる場所、信頼できるデータ プロバイダー、および信頼できるデータ接続ライブラリで指定します。 次の表に、PowerPivot データ アクセスを有効化または拡張する設定の説明を示します。 ここに記載されていない設定は、PowerPivot サーバー接続には影響しません。 これらのステップ バイ ステップの設定を指定する方法についてで「Excel Services 有効にする」セクションを参照してください[初期構成&#40;PowerPivot for SharePoint&#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)します。  
  
> [!NOTE]  
>  ほとんどのセキュリティ関連の設定は、信頼できる場所に適用されます。 既定値を保持するか、サイトごとに異なる値を使用する場合は、PowerPivot データを含むサイト用に信頼できる場所を追加作成し、そのサイトにのみ以下の設定を構成できます。 詳細については、「 [サーバーの全体管理での PowerPivot サイト用の信頼できる場所の作成](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)」を参照してください。  
  
|領域|設定|説明|  
|----------|-------------|-----------------|  
|[Web アプリケーション]|Windows 認証プロバイダー|PowerPivot は、Excel Services から取得した要求トークンを Windows ユーザー ID に変換します。 Excel Services をリソースとして使用する Web アプリケーションは、Windows 認証プロバイダーを使用するように構成されている必要があります。|  
|信頼できる場所|場所の種類|この値は、 **[Microsoft SharePoint Foundation]** に設定されている必要があります。 PowerPivot サーバーは、.xlsx ファイルのコピーを取得して、それをファーム内の Analysis Services サーバーに読み込みます。 このサーバーはコンテンツ ライブラリから .xlsx ファイルのみを取得できます。|  
||外部データの許可|この値は、 **[信頼できるデータ接続ライブラリと、埋め込まれている接続]** に設定されている必要があります。 PowerPivot データ接続は、ブックに埋め込まれています。 埋め込み接続を禁止した場合、ユーザーは、ピボットテーブル キャッシュは表示できますが、PowerPivot データを操作することはできなくなります。|  
||更新時の警告|PowerPivot ギャラリーを使用してブックやレポートを格納している場合は、この値を無効にする必要があります。 PowerPivot ギャラリーには、[開くときに更新する] と [更新時の警告] の両方がオフになっているときに最適に動作するドキュメント プレビュー機能が含まれています。|  
|信頼できるデータ プロバイダー|MSOLAP.4<br /><br /> MSOLAP.5|既定では MSOLAP.4 が含まれますが、PowerPivot データ アクセスでは、MSOLAP.4 プロバイダーが SQL Server 2008 R2 バージョンである必要があります。<br /><br /> MSOLAP.5 は、PowerPivot for SharePoint の [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンと共にインストールされます。<br /><br /> これらのプロバイダーは、信頼できるデータ プロバイダー一覧から削除しないでください。 場合によっては、ファーム内の別の SharePoint サーバーにもこのプロバイダーの追加のコピーをインストールすることが必要になることもあります。 「 [SharePoint サーバーへの Analysis Services OLE DB プロバイダーのインストール](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)」を参照してください。|  
|信頼できるデータ接続ライブラリ|任意。|PowerPivot ブックでは、Office データ接続 (.odc) ファイルを使用できます。 .odc ファイルを使用してローカル PowerPivot ブックに接続情報を提供する場合、同じ .odc ファイルをこのライブラリに追加できます。|  
|ユーザー定義関数アセンブリ|該当なし。|PowerPivot for SharePoint では、Excel Services 用にビルドおよび配置するユーザー定義関数アセンブリは無視されます。 特定の動作についてユーザー定義アセンブリに依存する場合、作成したユーザー定義関数は PowerPivot クエリ処理では使用されないことに留意してください。|  
  
## <a name="see-also"></a>関連項目  
 [PowerPivot サービス アカウントを構成します。](configure-power-pivot-service-accounts.md)   
 [構成、PowerPivot 自動データ更新アカウント&#40;PowerPivot for SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)   
 [サーバーの全体管理で PowerPivot サイト用の信頼できる場所を作成します。](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)   
 [PowerPivot セキュリティ アーキテクチャ](https://go.microsoft.com/fwlink/?linkID=220970)  
  
  
