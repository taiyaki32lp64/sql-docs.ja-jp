---
title: 接続文字列プロパティ (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 29a00a41-5b0d-44b2-8a86-1b16fe507768
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9b6516c427f15c960c6bfb459c4fc375e798b798
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "67046674"
---
# <a name="connection-string-properties-analysis-services"></a>接続文字列プロパティ (Analysis Services)
  このトピックでは、接続文字列プロパティについて説明します。接続文字列プロパティは、いずれかのデザイナー ツールまたは管理ツールで設定できます。また、Analysis Services データに接続および照会するクライアント アプリケーションによって作成された接続文字に表示されることもあります。 そのため、使用できるプロパティのサブセットについてのみ説明します。 完全な一覧には、多くのサーバー プロパティおよびデータベース プロパティが含まれます。それらを使用すると、サーバーでインスタンスまたはデータベースを構成している方法に関係なく、特定のアプリケーションの接続をカスタマイズできます。  
  
 アプリケーション コードでカスタム接続文字列を作成する開発者は、ADOMD.NET クライアントの API ドキュメントを参照して、詳しい一覧「 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>  
  
 このトピックで説明するプロパティは、Analysis Services クライアント ライブラリ、ADOMD.NET、AMO、および OLE DB Provider for Analysis Services で使用されます。 接続文字列プロパティの大部分は、3 つすべてのクライアント ライブラリで使用できます。 例外については、説明に記載しています。  
  
 このトピックのセクションは次のとおりです。  
  
 [よく使用される接続パラメーター](#bkmk_common)  
  
 [認証およびセキュリティ](#bkmk_auth)  
  
 [特別な用途のパラメーター](#bkmk_special)  
  
 [予約済み](#bkmk_reserved)  
  
 [接続文字列の例](#bkmk_examples)  
  
 [Analysis Services で使用される接続文字列の形式](#bkmk_supportedstrings)  
  
 [接続文字列の暗号化](#bkmk_encrypt)  
  
> [!NOTE]  
>  プロパティを設定する際に、誤って同じプロパティを 2 回設定した場合は、接続文字列内の最後のプロパティが使用されます。  
  
 既存の Microsoft アプリケーションで Analysis Services 接続を指定する方法の詳細については、「[クライアント アプリケーションからの接続 &#40;Analysis Services&#41;](connect-from-client-applications-analysis-services.md)」をご覧ください。  
  
##  <a name="bkmk_common"></a> よく使用される接続パラメーター  
 次の表では、接続文字列を作成する際に最もよく使用されるプロパティについて説明します。  
  
|プロパティ|説明|例|  
|--------------|-----------------|-------------|  
|`Data Source` または `DataSource`|サーバー インスタンスを指定します。 このプロパティは、すべての接続に必要です。 有効な値には、サーバーのネットワーク名または IP アドレス、ローカル接続の local または localhost、URL (サーバーが HTTP または HTTPS アクセス用に構成されている場合)、またはローカル キューブ (.cub) ファイルの名前があります。|`Data source=AW-SRV01` : 既定のインスタンスとポート (TCP 2383) の場合。<br /><br /> `Data source=AW-SRV01$Finance:8081` : 名前付きインスタンス ($Finance) と固定ポートの場合。<br /><br /> `Data source=AW-SRV01.corp.Adventure-Works.com` : 完全修飾ドメイン名の場合。既定のインスタンスとポートを想定しています。<br /><br /> `Data source=172.16.254.1` : サーバーの IP アドレスの場合。DNS サーバーの参照をバイパスします。接続の問題をトラブルシューティングする場合に便利です。|  
|`Initial Catalog` または `Catalog`|接続先の Analysis Services データベースの名前を指定します。 データベースが Analysis Services に配置されており、データベースに接続するための権限を持っている必要があります。 このプロパティは、AMO 接続では省略できますが、ADOMD.NET では必須です。|`Initial catalog=AdventureWorks2012`|  
|`Provider`|有効な値には、MSOLAP または MSOLAP が含まれます。\<バージョン > ここで、\<バージョン > 3、4、または 5 のいずれかです。 ファイル システム上では、データ プロバイダーの名前は、msolap110.dll (Server 2012 バージョン)、msolap100.dll (SQL Server SQL Server 2008 および 2008 R2)、および msolap90.dll (SQL Server 2005) です。<br /><br /> 現在のバージョンは、MSOLAP.5 です。 このプロパティは省略可能です。 既定では、クライアント ライブラリは、レジストリから現在のバージョンの OLE DB プロバイダーを読み取ります。 SQL Server 2008 インスタンスに接続するなど、特定のバージョンのデータ プロバイダーが必要な場合のみ、このプロパティを設定する必要があります。<br /><br /> データ プロバイダーは、SQL Server のバージョンに対応しています。 現在と以前のバージョンの Analysis Services を使用している場合は、通常、手動で作成した接続文字列で使用するプロバイダーを指定する必要があります。 また、必要なバージョンがインストールされていないコンピューターでは、特定のバージョンのデータ プロバイダーをダウンロードしてインストールすることが必要になる場合もあります。 OLE DB プロバイダーは、ダウンロード センターの SQL Server Feature Pack のページからダウンロードできます。 SQL Server 2012 用の Analysis Services OLE DB プロバイダーをダウンロードするには、「 [Microsoft SQL Server 2012 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=296473) 」にアクセスしてください。<br /><br /> MSOLAP.4 は、SQL Server 2008 と SQL Server 2008 R2 の両方でリリースされました。 2008 R2 バージョンは、PowerPivot ブックをサポートしており、SharePoint サーバーに手動でインストールすることが必要な場合があります。 これらのバージョンを区別するためには、プロバイダーのファイル プロパティでビルド番号を確認する必要があります。Program files\Microsoft Analysis Services\AS OLEDB\10 に移動します。 msolap110.dll を右クリックし、 **[プロパティ]** をクリックします。 **[詳細]** をクリックします。 ファイルのバージョン情報が表示されます。 バージョンは 10.50 を含める必要があります。\<buildnumber > の SQL Server 2008 R2。 詳細については、「 [SharePoint サーバーへの Analysis Services OLE DB プロバイダーのインストール](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md) 」および「 [Analysis Services 接続に使用するデータ プロバイダー](data-providers-used-for-analysis-services-connections.md)」を参照してください。<br /><br /> MSOLAP.3 は、SQL Server 2005 でリリースされました。<br /><br /> MSOLAP.4 は、SQL Server 2008 と SQL Server 2008 R2 でリリースされました<br /><br /> MSOLAP.5 は、SQL Server 2012 でリリースされました|`Provider=MSOLAP.3` は、SQL Server 2005 バージョンの OLE DB Provider for Analysis Services を必要とする接続に使用します。|  
|`Cube`|キューブ名またはパースペクティブ名。 データベースには、複数のキューブおよびパースペクティブを含めることができます。 複数の対象が考えられる場合は、接続文字列にキューブ名またはパースペクティブ名を含めます。|`Cube=SalesPerspective` は、Cube 接続文字列プロパティを使用して、キューブの名前またはパースペクティブの名前を指定できることを示しています。|  
  
##  <a name="bkmk_auth"></a> 認証およびセキュリティ  
 このセクションでは、認証および暗号化に関連する接続文字列プロパティを示します。 Analysis Services では Windows 認証のみを使用しますが、接続文字列でプロパティを設定して、特定のユーザー名とパスワードを渡すことができます。  
  
 プロパティは、アルファベット順に示しています。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|`EffectiveUserName`|サーバーでエンド ユーザー ID の権限を借用する必要がある場合に使用します。 アカウントを domain\user という形式で指定します。 このプロパティを使用するには、呼び出し元に Analysis Services に対する管理権限が必要です。 SharePoint から Excel ブックのこのプロパティを使用する方法の詳細については、「 [SharePoint Server 2013 で Analysis Services の EffectiveUserName を使用する](https://go.microsoft.com/fwlink/?LinkId=311905)」をご覧ください。 Reporting Services でこのプロパティを使用する方法の詳細については、「 [SSAS での EffectiveUserName を使用した権限の借用](https://www.artisconsulting.com/blogs/greggalloway/2010/4/1/using-effectiveusername-to-impersonate-in-ssas)」をご覧ください。<br /><br /> `EffectiveUserName` は、PowerPivot for SharePoint のインストールで使用情報を取得する場合に使用します。 ユーザー ID を含むイベントまたはエラーをログ ファイルに記録できるように、ユーザー ID がサーバーに渡されます。 PowerPivot の場合、承認には使用されません。|  
|**Encrypt Password**|ローカル キューブを暗号化するためにローカル パスワードを使用するかどうかを指定します。 有効な値は True または False です。 既定値は False です。|  
|`Encryption Password`|暗号化されたローカル キューブの暗号化を解除するために使用するパスワード。 既定値は空です。 この値は、ユーザーが明示的に設定する必要があります。|  
|`Impersonation Level`|サーバーがクライアントの権限を借用するときに使用できる権限借用レベルを示します。 有効な値は次のとおりです。<br /><br /> **匿名**:クライアントはサーバーに対して匿名です。 サーバー プロセスではクライアントに関する情報を取得できず、クライアントの権限を借用できません。<br /><br /> **識別**:サーバー プロセスではクライアント ID を取得できます。 また、サーバーでは承認のためにクライアント ID の権限を借用できますが、クライアントとしてシステム オブジェクトにアクセスすることはできません。<br /><br /> **権限を借用**:これが既定値です。 クライアント ID の権限を借用できますが、接続を確立する場合に限られ、すべての呼び出しで借用できるわけではありません。<br /><br /> **デリゲート**:サーバー プロセスでは、クライアントに代わって機能を実行するときに、クライアントのセキュリティ コンテキストの権限を借用できます。 また、他のサーバーに対する呼び出しを送信することもできます。|  
|`Integrated Security`|Analysis Services に接続するために使用する呼び出し元の Windows ID。 有効な値は、空白、SSPI、および BASIC です。<br /><br /> `Integrated Security`=`SSPI` NTLM、Kerberos、または匿名認証を許可する TCP 接続の既定値です。 空白は、HTTP 接続の既定値です。<br /><br /> `SSPI` を使用する場合、`ProtectionLevel` を `Connect`、`PktIntegrity`、`PktPrivacy` のいずれかに設定する必要があります。|  
|`Persist Encrypted`|クライアント アプリケーションでデータ ソース オブジェクトに暗号化された形式で秘密の認証情報 (パスワードなど) を保存する必要がある場合に、このプロパティを設定します。 既定では、認証情報は保存されません。|  
|`Persist Security Info`|有効値は True および False です。 True に設定した場合、以前に接続文字列に指定したユーザー ID やパスワードなどのセキュリティ情報を接続の確立後に接続から取得できます。 既定値は False です。|  
|`ProtectionLevel`|接続で使用するセキュリティ レベルを指定します。 有効な値は、<br /><br /> `None` 。 未認証の接続または匿名接続。 サーバーに送信されるデータの認証は行われません。<br /><br /> `Connect` 。 認証された接続。 クライアントがサーバーとのリレーションシップを確立するときにのみ認証が行われます。<br /><br /> `PktIntegrity` 。 暗号化された接続。 すべてのデータが正しいクライアントから受信されていること、および転送中に変更されていないことが確認されます。<br /><br /> `PktPrivacy` 。 署名された暗号化 (XMLA でのみサポートされます)。 すべてのデータが正しいクライアントから受信されていること、および転送中に変更されておらず、暗号化することでデータのプライバシーが保護されていることが確認されます。<br /><br /> <br /><br /> 詳細については、「 [Establishing Secure Connections in ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-client/connections-in-adomd-net-establishing-secure-connections)」をご覧ください。|  
|`Roles`|定義済みロールのコンマ区切りの一覧を指定します。そのロールによって与えられる権限を使用して、サーバーまたはデータベースに接続します。 このプロパティを省略した場合、すべてのロールを使用し、有効な権限はすべてのロールの組み合わせになります。 プロパティを空の値に設定 (たとえば、ロール =' ') クライアント接続には、ロールのメンバーシップがありません。<br /><br /> このプロパティを使用した管理者は、ロールによって与えられた権限を使用して接続します。 ロールによって与えられた権限が十分でない場合、コマンドが失敗することがあります。|  
|`SSPI`|`Integrated Security` が `SSPI` に設定されているときにクライアント認証に使用するセキュリティ パッケージを明示的に指定します。 SSPI では複数のパッケージがサポートされていますが、このプロパティを使用すると特定のパッケージを指定できます。 有効な値は、Negotiate、Kerberos、NTLM、および Anonymous User です。 このプロパティを設定しない場合、接続ですべてのパッケージを使用できます。|  
|`Use Encryption for Data`|データ転送を暗号化します。 有効な値は True および False です。|  
|`User ID`=...; `Password`=|`User ID` と `Password` を一緒に使用します。 Analysis Services では、これらの資格情報によって指定されたユーザー ID の権限を借用します。 Analysis Services 接続では、サーバーが HTTP アクセス用に構成されており、IIS 仮想ディレクトリに統合セキュリティではなく基本認証を指定した場合にのみ、コマンド ラインで資格情報を入力します。<br /><br /> ユーザー名とパスワードは、Windows ID (ローカルまたはドメイン ユーザー アカウント) の資格情報である必要があります。 `User ID` には空白が挿入されていることに注意してください。 このプロパティの他の別名には、`UserName` (空白なし) および `UID` があります。 `Password` の別名は、`PWD` です。|  
  
##  <a name="bkmk_special"></a> 特別な用途のパラメーター  
 ここでは、残りの接続文字列パラメーターについて説明します。 これらは、アプリケーションで必要な特定の接続動作を実現するために使用します。  
  
 プロパティは、アルファベット順に示しています。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|`Application Name`|接続に関連付けられたアプリケーションの名前を設定します。 この値は、トレース イベントを監視する場合 (特に、同じデータベースにアクセスするアプリケーションが複数ある場合) に役立ちます。 たとえば、アプリケーション名を追加 = 'test'、接続文字列 'test' を SQL Server Profiler トレースに表示する次のスクリーン ショットに示すようにします。<br /><br /> ![SSAS_AppNameExcample](../media/ssas-appnameexcample.gif "SSAS_AppNameExcample")<br /><br /> このプロパティの別名には、`sspropinitAppName` および `AppName` があります。 詳細については、「 [SQL Server に接続する場合の Application Name パラメーターの使用](https://www.connectionstrings.com/use-application-name-sql-server/)」をご覧ください。|  
|`AutoSyncPeriod`|クライアントとサーバーのキャッシュを同期する頻度 (ミリ秒単位) を設定します。 ADOMD.NET には、最小限のメモリ オーバーヘッドが発生する、よく使用されるオブジェクトのために、クライアント キャッシュが用意されています。 これは、サーバーへのラウンド トリップを減らすのに役立ちます。 既定値は 10,000 ミリ秒 (10 秒) です。 null または 0 に設定した場合、自動同期は無効になります。|  
|`Character Encoding`|要求での文字をエンコードする方法を定義します。 有効な値は、Default または UTF-8 (これらは同じです) と、UTF-16 です。|  
|`CompareCaseSensitiveStringFlags`|指定されたロケールの大文字と小文字を区別する文字列の比較を調整します。 このプロパティの設定の詳細については、「 [CompareCaseSensitiveStringFlags プロパティ](https://msdn.microsoft.com/library/aa237459\(v=sql.80\).aspx)」をご覧ください。|  
|`Compression Level`|`TransportCompression` が XPRESS の場合、圧縮レベルを設定して、圧縮率を制御できます。 有効値は 0 ～ 9 です。0 の場合に圧縮率が最も低く、9 の場合に圧縮率が最も高くなります。 圧縮率を上げると、パフォーマンスが低下します。 既定値は 0 です。|  
|`Connect Timeout`|クライアントの接続試行がタイムアウトするまでの最長時間 (秒単位) を指定します。接続がこの期間内に成功しなかった場合、クライアントは接続試行を終了し、エラーが発生します。|  
|`MDX Compatibility`|このプロパティの目的は、MDX クエリを発行するアプリケーションの MDX 動作の一貫性を確保することです。 Excel で MDX クエリを使用して、Analysis Services に接続されたピボットテーブルを設定および計算する場合は、このプロパティを 1 に設定し、不規則階層のプレースホルダー メンバーがピボットテーブルに表示されるようにします。 有効な値は、0、1、および 2 です。<br /><br /> 0 および 1 では、プレースホルダー メンバーが公開されます。2 では、公開されません。 このプロパティが空の場合は、0 と見なされます。|  
|`MDX Missing Member Mode=Error`|欠落したメンバーを MDX ステートメントで無視するかどうかを示します。 有効な値は、Default、Error、および Ignore です。 既定では、サーバーで定義されている値を使用します。 Error では、メンバーが存在しない場合、エラーが発生します。 Ignore では、欠落した値を無視するように指定します。|  
|`Optimize Response`|次のどのクエリ応答の最適化を有効にするかを示すビットマスク。<br /><br /> 0x01:既定値です。 0x01normaltupleset を使用します。 <br />0x02:スライサーが空の場合に使用|  
|`Packet Size`|ネットワーク パケットのバイト単位のサイズ (512 ～ 32,767)。 既定のネットワーク パケット サイズは 4,096 です。|  
|`Protocol Format`|サーバーに送信される XML の形式を設定します。 有効な値は、Default、XML、または Binary です。 プロトコルは XMLA です。 圧縮形式 (これが既定値です)、未加工の XML、またはバイナリ形式で XML を送信するように指定できます。 バイナリ形式では、XML 要素と属性をエンコードするため、サイズが小さくなります。 圧縮形式は、要求と応答のサイズをさらに小さくする専用の形式です。 圧縮形式とバイナリ形式は、データ転送の要求と応答を高速化するために使用します。<br /><br /> バイナリまたは圧縮形式を使用する場合は、接続でクライアント ライブラリを使用する必要があります。 OLE DB プロバイダーでは、要求と応答をバイナリ形式または圧縮形式に変換できます。 AMO および ADOMD.NET では、要求をテキスト形式に変換しますが、バイナリ形式または圧縮形式の応答を受け入れます。<br /><br /> この接続文字列プロパティは、`EnableBinaryXML` および `EnableCompression` サーバー構成設定と同じです。|  
|`Real Time Olap`|キャッシュをバイパスし、すべてのパーティションでクエリ通知をアクティブにリッスンするには、このプロパティを設定します。 既定では、このプロパティは設定されません。|  
|`Safety Options`|ユーザー定義関数とユーザー定義アクションの安全性レベルを設定します。 有効な値は、0、1、2 です。 Excel 接続では、このプロパティは Safety Options=2 です。 このオプションの詳細については、「 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>」をご覧ください。|  
|`SQLQueryMode`|SQL クエリに計算を含めるかどうかを指定します。 有効な値は、Data、Calculated、IncludeEmpty です。 Data は、計算を許可しないことを示します。 Calculated では、計算を許可します。 IncludeEmpty では、クエリ結果で計算および空の行を返すことができます。|  
|`Timeout`|エラーが発生するまでに、クライアント ライブラリがコマンドの完了を待機する時間 (ミリ秒単位) を指定します。|  
|`Transport Compression`|`Protocol Format` プロパティで圧縮を指定した場合に、クライアントとサーバーの通信を圧縮する方法を定義します。 有効な値は、Default、None、Compressed、および `gzip` です。 Default では、TCP の場合は圧縮なしに、HTTP の場合は `gzip` になります。 None は、圧縮を使用しないことを示します。 Compressed では、XPRESS 圧縮を使用します (SQL Server 2008 以降)。 `gzip` は、HTTP 要求に Accept-Encoding=gzip が含まれる HTTP 接続でのみ有効です。|  
|`UseExistingFile`|ローカル キューブに接続する場合に使用します。 このプロパティでは、ローカル キューブを上書きするかどうかを指定します。 有効な値は True または False です。 True に設定した場合、キューブ ファイルが存在する必要があります。 既存のファイルが接続の対象となります。 False に設定した場合、キューブ ファイルが上書きされます。|  
|`VisualMode`|ディメンションのセキュリティを適用する場合に、メンバーを集計する方法を制御するには、このプロパティを設定します。<br /><br /> すべてのユーザーが表示できるキューブ データでは、合計に合算されるすべての値を表示できるため、すべてのメンバーを集計することは適切です。 ただし、ユーザー ID に基づいてディメンションをフィルター選択または制限している場合は、すべてのメンバーに基づいた合計を表示すると、制限されている値と許可されている値の両方が単一の合計に合算されるため、わかりにくくなることや、必要以上の情報が表示されることになります。<br /><br /> ディメンションのセキュリティを適用する場合に、メンバーを集計する方法を指定するには、このプロパティを True に設定して、集計に許可されている値のみを使用するか、False に設定して、制限されている値を合計から除外します。<br /><br /> 接続文字列で設定した場合、この値はキューブ レベルまたはパースペクティブ レベルに適用されます。 モデル内では、より細かなレベルで表示部分の合計を制御できます。<br /><br /> 有効な値は 0、1、および 2 です。<br /><br /> 既定値は 0 です。 現在、既定の動作は 2 と同じです。集計には、ユーザーに対して表示されない値が含まれます。<br /><br /> 1 では、表示されない値を合計から除外します。 これは、Excel での既定値です。<br /><br /> 2 では、表示されない値を合計に含めます。 これは、サーバーでの既定値です。<br /><br /> <br /><br /> このプロパティの別名には、`Visual Total` または `Default MDX Visual Mode` があります。|  
  
##  <a name="bkmk_reserved"></a> 予約済み  
 次のプロパティは、接続文字列では使用できますが、Analysis Services の現在のリリースでは機能しません。  
  
-   Authenticated User  
  
-   Cache Authentication  
  
-   Cache Mode (このプロパティの使用については、以前のリリースで調査しました。 このプロパティの使用を推奨するブログ投稿が見つかる場合がありますが、Microsoft サポートからの指示がない限り、このプロパティを設定しないでください)。  
  
-   Cache Policy  
  
-   Cache Ratio  
  
-   Cache Ratio2  
  
-   Dynamic Debug Limit  
  
-   デバッグ モード  
  
-   モード  
  
-   SQLCompatibility  
  
-   Use Formula Cache  
  
##  <a name="bkmk_examples"></a> 接続文字列の例  
 このセクションでは、アプリケーションで使用される一般的で Analysis Services 接続を設定するときに使用するほとんどの場合、接続文字列が表示されます。  
  
 **一般的な接続文字列**  
  
 Reporting Services から接続を構成する際は、次のような接続文字列を使用できます。  
  
 `Data source=<servername>; initial catalog=<databasename>`  
  
 **Excel での接続文字列**  
  
 Excel での既定の ADOMD.NET 接続文字列では、データ プロバイダー、サーバー、データベース名、Windows 統合セキュリティを指定します。 MDX の互換性レベルは常に 1 に設定されます。 現在のセッションの値を変更できますが、ファイルを次回開いたときに、Excel によって MDX の互換性が 1 にリセットされます。  
  
 `Provider=MSOLAP.5;Integrated Security=SSPI;Persist Security Info=True;Initial Catalog=Adventure Works DW 2008R2;Data Source=AW-SRV01;MDX Compatibility=1;Safety Options=2;MDX Missing Member Mode=Error`  
  
 詳細については、次を参照してください。[データ接続、データ ソース、および Reporting Services の接続文字列](../../reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)と[SharePoint Server 2013 の Excel Services 用のデータ認証](https://go.microsoft.com/fwlink/?LinkId=296350)します。  
  
##  <a name="bkmk_supportedstrings"></a> Analysis Services で使用される接続文字列の形式  
 このセクションでは、Analysis Services でサポートされている接続文字列の形式を箇条書きにして説明します。 PowerPivot データベースへの接続を除く、Analysis Services に接続するアプリケーションでこれらの接続文字列を指定できます。  
  
 **サーバーへのネイティブ (直接) 接続**  
  
 `Data Source=server[:port][\instance]` 場所"port"および"\instance"は省略可能です。 たとえば、指定すると"データ ソース = server1""server1"という名前のサーバーで、既定のインスタンス (と既定のポート 2383) への接続を開きます。  
  
 "データ ソース = server1:port1"ポート"port1""server1"上で実行されている Analysis Services インスタンスへの接続が開きます。  
  
 "データ ソース = server1\instance1"は (既定のポート 2382) で SQL Browser への接続を開き、ポート、名前付きインスタンス"instance1"を解決、その Analysis Services ポートへの接続を開きます。  
  
 "データ ソース = server1:port1\instance1"は"port1"で SQL Browser への接続を開き、名前付きインスタンス"instance1"のポートを解決するには、その Analysis Services ポートへの接続を開きます。  
  
 **ローカル キューブ接続 (.cub ファイル)**  
  
 `Data Source=<path>`、たとえば"データ Source=c:\temp\a.cub"  
  
 **msmdpump.dll への Http(s) 接続**  
  
 `Data Source=<URL>`。URL には、msmdpump.dll が格納された仮想 IIS フォルダーの HTTP アドレスまたは HTTPS アドレスを指定します。 詳細については、「 [インターネット インフォメーション サービス &#40;IIS&#41; 8.0 上の Analysis Services への HTTP アクセスの構成](configure-http-access-to-analysis-services-on-iis-8-0.md)」をご覧ください。  
  
 **PowerPivot ブック (.xlsx、.xlsb、または .xlsm ファイル) への http (s) 接続**  
  
 `Data Source=<URL>`。URL には、SharePoint ライブラリにパブリッシュされた PowerPivot ブックへの SharePoint パスを指定します。 たとえば、"データ ソース =<http://localhost/Shared> Documents/Sales.xlsx"。  
  
 **BI Semantic Model 接続ファイルへの Http(s) 接続**  
  
 `Data Source=<URL>` 。URL には、.bism ファイルへの SharePoint パスを指定します。 たとえば、"データ ソース =<http://localhost/Shared> Documents/Sales.bism"。  
  
 **埋め込み PowerPivot 接続**  
  
 `Data Source=$Embedded$`。$embedded$ には、ブック内の埋め込み PowerPivot データ モデルを参照するモニカーを指定します。 この接続文字列は内部的に作成、管理されます。 変更しないでください。 埋め込み接続文字列は、クライアント ワークステーション上の PowerPivot for Excel アドイン、または SharePoint ファーム内の PowerPivot for SharePoint インスタンスによって解決されます。  
  
 **Analysis Services ストアド プロシージャ内のローカル サーバーのコンテキスト**  
  
 `Data Source=*`。"*" はローカル インスタンスに解決されます。  
  
##  <a name="bkmk_encrypt"></a> 接続文字列の暗号化  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、各データ ソースへの接続に使用する接続文字列が暗号化されて保存されます。 データ ソースへの接続にユーザー名とパスワードが必要な場合は、接続文字列を使用して [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] に名前とパスワードを保存するか、データ ソースへの接続が必要になるたびに名前とパスワードを要求するプロンプトを表示できます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] でユーザー情報を要求するプロンプトを表示する場合、この情報の保存と暗号化は必要ありません。 ただし、接続文字列にこの情報を保存する場合、この情報の暗号化とセキュリティ保護が必要です。  
  
 接続文字列情報を暗号化し、セキュリティを確保するために、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ではデータ保護 API が使用されます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースごとに別個の暗号化キーを使用して、接続文字列情報を暗号化します。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって作成され、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 開始アカウントに基づいて接続文字列情報を暗号化します。 各データベースの暗号化キーが [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の起動時に読み取られ、暗号化が解除されて保管されます。 以後、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] がデータ ソースに接続する際は、暗号化の解除された適切なキーが [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって使用され、データ ソースの接続文字列情報の暗号化が解除されます。  
  
## <a name="see-also"></a>参照  
 [インターネット インフォメーション サービス &#40;IIS&#41; 8.0 上の Analysis Services への HTTP アクセスの構成](configure-http-access-to-analysis-services-on-iis-8-0.md)   
 [Kerberos の制約付き委任のための Analysis Services の構成](configure-analysis-services-for-kerberos-constrained-delegation.md)   
 [Analysis Services 接続に使用するデータ プロバイダー](data-providers-used-for-analysis-services-connections.md)   
 [Analysis Services への接続](connect-to-analysis-services.md)  
  
  
