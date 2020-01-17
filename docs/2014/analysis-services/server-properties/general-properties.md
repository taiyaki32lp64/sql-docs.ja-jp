---
title: '[全般] プロパティ |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- IdleConnectionTimeout property
- InstanceVisible property
- TempDir property
- AdminTimeout property
- MinIdleSessionTimeout property
- MaxIdleSessionTimeout property
- IdleOrphanSessionTimeout property
- BackupDir property
- CommitTimeout property
- ExternalCommandTimeout property
- Enabled property
- ForceCommitTimeout property
- Port property
- CoordinatorShutdownMode property
- ServerTimeout property
- AllowedBrowsingFolders property
- CoordinatorCancelCount property
- DataDir property
- CoordinatorQueryMaxThreads property
- CoordinatorExecutionMode property
- ExternalConnectionTimeout property
- CollationName property
- EnableFast1033Locale property
- CoordinatorBuildMaxThreads property
- Language property
- StatisticsStoreSize property
- RepositoryConnectionString property
ms.assetid: 88a8117c-396a-469f-a62d-c6f262504021
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6b833fe2710ce04cb4a0c8b08fedc9a882c19add
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66069028"
---
# <a name="general-properties"></a>全般プロパティ
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、次の表に示すサーバー プロパティがサポートされています。 このトピックでは、Security、Network、ThreadPool など、個別のセクションで取り上げることのできなかった、msmdsrv.ini ファイル内のサーバー プロパティについて説明しています。 その他のサーバー プロパティとその設定方法の詳細については、「 [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md)」を参照してください。  
  
 **適用対象:** 多次元および表形式サーバー モードでは、それ以外の場合に記載されていない場合  
  
## <a name="non-specific-category"></a>不特定カテゴリ  
 `AdminTimeout`  
 管理者のタイムアウトを秒単位で定義する、符号付き 32 ビット整数のプロパティです。 これは詳細プロパティなので、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] サポートの指示がない限り、変更しないでください。  
  
 このプロパティの既定値は 0 であり、タイムアウトがないことを示します。  
  
 `AllowedBrowsingFolders`  
 Analysis Services のダイアログ ボックスでファイルを保存、開く、および検索するときに参照できるフォルダーを区切り記号で区切った一覧で指定する文字列プロパティです。 Analysis Services のサービス アカウントには、リストに追加するすべてのフォルダーの読み取り権限と書き込み権限が必要です。  
  
 `BackupDir`  
 バックアップ コマンドの一部として、パスが指定されていない場合に、既定では、バックアップのファイルが格納されるディレクトリの名前を指定する文字列プロパティ。  
  
 `CollationName`  
 サーバーの照合順序を指定する文字列プロパティです。 詳細については、「[言語および照合順序 &#40;Analysis Services&#41;](../languages-and-collations-analysis-services.md)」を参照してください。  
  
 `CommitTimeout`  
 サーバーがトランザクションをコミットする目的で書き込みロックの取得を待機する時間 (ミリ秒単位) を指定する整数のプロパティです。 サーバーはトランザクションをコミットする書き込みロックを取得する前に他のロックが解放されるのを待機する必要があるため、待機期間が必要になることがあります。  
  
 このプロパティの既定値は 0 であり、サーバーで無限に待機することを示します。 ロックに関連したプロパティの詳細については、「 [SQL Server 2008 R2 Analysis Services 操作ガイド](https://go.microsoft.com/fwlink/?LinkID=225539)」を参照してください。  
  
 `CoordinatorBuildMaxThreads`  
 パーティション インデックスの作成に割り当てられるスレッドの最大数を定義する、符号付き 32 ビット整数のプロパティです。 パーティション インデックスの作成時間を短縮するには、この値を大きくしてください。ただし、メモリの使用量は増えます。 このプロパティの詳細については、「 [SQL Server 2008 R2 Analysis Services 操作ガイド](https://go.microsoft.com/fwlink/?LinkID=225539)」を参照してください。  
  
 `CoordinatorCancelCount`  
 キャンセル イベントが発生したかどうかを内部反復カウントに基づいてサーバーがチェックする頻度を定義する、符号付き 32 ビット整数のプロパティです。 キャンセルのチェック頻度を多くするには、この値を小さくしてください。ただし、全体的なパフォーマンスは低下します。  
  
 表形式サーバー モードでは、`CoordinatorCancelCount` は無視されます。  
  
 `CoordinatorExecutionMode`  
 処理操作やクエリ操作など、サーバーによって試行される並列操作の最大数を定義する、符号付き 32 ビット整数のプロパティです。 0 を指定すると、サーバーの内部アルゴリズムに基づいて決定されます。 正の数値は、操作の最大総数を示します。 負の数値 (反対の符号) は、プロセッサあたりの操作の最大数を示します。  
  
 表形式サーバー モードでは、`CoordinatorExecutionMode` は無視されます。  
  
 このプロパティの既定値は -4 であり、サーバーのプロセッサあたりの並列操作が 4 に制限されることを示します。 このプロパティの詳細については、「 [SQL Server 2008 R2 Analysis Services 操作ガイド](https://go.microsoft.com/fwlink/?LinkID=225539)」を参照してください。  
  
 `CoordinatorQueryMaxThreads`  
 クエリ解決時のパーティション セグメントあたりの最大スレッド数を定義する、符号付き 32 ビット整数のプロパティです。 同時ユーザーの数が少なくなるほど大きい値を設定できますが、値を大きくするとメモリの使用量が増えます。 逆に、同時ユーザーが多い場合は、この値を小さくする必要があります。  
  
 `CoordinatorShutdownMode`  
 コーディネーターのシャットダウン モードを定義するブール型プロパティです。 これは詳細プロパティなので、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] サポートの指示がない限り、変更しないでください。  
  
 `DataDir`  
 データを保存するディレクトリの名前を指定する文字列プロパティです。  
  
 `DeploymentMode`  
 Analysis Services サーバー インスタンスの操作コンテキストを指定します。 このプロパティは、ダイアログ ボックス、メッセージ、およびドキュメントの「サーバー モード」と呼ばれます。 このプロパティは、Analysis Services のインストール時に選択したサーバー モードに基づいて、SQL Server セットアップによって構成されます。 このプロパティは内部使用のみと見なしてください。常にセットアップによって指定された値が使用されます。  
  
 このプロパティの有効値を以下に示します。  
  
|値|Description|  
|-----------|-----------------|  
|0|これが既定値です。 MOLAP、HOLAP、ROLAP の各ストレージ、およびデータ マイニング モデルを使用する多次元データベースの処理に使用される多次元モードを指定します。|  
|1|PowerPivot for SharePoint 配置の一部としてインストールされた Analysis Services インスタンスを指定します。 PowerPivot for SharePoint インストールの一部である Analysis Services インスタンスの配置モード プロパティは変更しないでください。 モードを変更すると、PowerPivot データがサーバー上で実行されなくなります。|  
|2|インメモリ ストレージまたは DirectQuery ストレージを使用するテーブル モデル データベースをホストするために使用するテーブル モードを指定します。|  
  
 各モードは、他のモードと相互に排他的です。 テーブル モード用に構成されたサーバーでは、キューブおよびディメンションを含む Analysis Services データベースを実行できません。 基になるコンピューターのハードウェアでサポートできる場合は、Analysis Services の複数のインスタンスを同じコンピューターにインストールし、さまざまな配置モードを使用するように各インスタンスを構成できます。 Analysis Services はリソースを大量に消費するアプリケーションであることに注意してください。 同じシステム上に複数のインスタンスを配置する構成は、ハイエンド サーバーの場合のみお勧めします。  
  
 `EnableFast1033Locale`  
 詳細プロパティです。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] サポートの指示がない限り、変更しないでください。  
  
 `ExternalCommandTimeout`  
 リレーショナル データ ソースや外部 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバーなど、外部サーバーに対して発行されたコマンドのタイムアウトを秒単位で定義する整数のプロパティです。  
  
 このプロパティの既定値は 3600 (秒) です。  
  
 `ExternalConnectionTimeout`  
 リレーショナル データ ソースや外部 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバーなど、外部サーバーへの接続確立のタイムアウトを秒単位で定義する整数のプロパティです。 このプロパティは、接続のタイムアウトが接続文字列に指定されている場合に無視されます。  
  
 このプロパティの既定値は 60 (秒) です。  
  
 `ForceCommitTimeout`  
 処理中のクエリなど、現在のコマンドに先行する他のコマンドを取り消す前に書き込みコミット操作が待機する必要のある時間をミリ秒単位で指定する整数のプロパティです。 これにより、クエリなどの優先順位の低い操作を取り消すことでコミット トランザクションを続行できます。  
  
 このプロパティの既定値は 30 秒 (30,000 ミリ秒) であり、コミット トランザクションが 30 秒間待機するまで他のコマンドはタイムアウトにならないことを示します。  
  
> [!NOTE]  
>  このイベントによってクエリやプロセスが取り消されると、"`Server: The operation has been cancelled`" というエラー メッセージが報告されます。  
  
 このプロパティの詳細については、「 [SQL Server 2008 R2 Analysis Services 操作ガイド](https://go.microsoft.com/fwlink/?LinkID=225539)」を参照してください。  
  
> [!IMPORTANT]  
>  `ForceCommitTimeout` は、キューブ処理コマンドと書き戻し操作に適用されます。  
  
 `IdleConnectionTimeout`  
 アクティブでない接続のタイムアウトを秒単位で指定する整数のプロパティです。  
  
 このプロパティの既定値は 0 であり、アイドル状態の接続がタイムアウトにならないことを示します。  
  
 `IdleOrphanSessionTimeout`  
 孤立したセッションをサーバー メモリに保持しておく時間を秒単位で定義する整数のプロパティです。 孤立セッションとは、関連付けられている接続がなくなったセッションです。 既定値は 120 秒です。  
  
 `InstanceVisible`  
 SQL Server Browser サービスからのインスタンス要求を検出するためにサーバー インスタンスを表示するかどうかを指定するブール型プロパティです。 既定値は True です。 false に設定した場合、インスタンスは SQL Server Browser に表示されません。  
  
 `Language`  
 エラー メッセージや数値書式などの言語を定義する文字列プロパティです。 このプロパティは CollationName プロパティをオーバーライドします。  
  
 このプロパティの既定値は空白であり、CollationName プロパティによって言語が定義されることを示します。  
  
 `LogDir`  
 サーバー ログを保存するディレクトリの名前を指定する文字列プロパティです。 このプロパティは、データベース テーブル (既定の動作) ではなく、ディスク ファイルがログ記録に使用される場合にのみ適用されます。  
  
 `MaxIdleSessionTimeout`  
 アイドル状態のセッションの最大タイムアウトを秒単位で定義する整数のプロパティです。 既定値は 0 (ゼロ) で、セッションがタイムアウトにならないことを示します。ただし、サーバーにリソースの制約がある場合はアイドル状態のセッションが削除されます。  
  
 `MinIdleSessionTimeout`  
 アイドル状態のセッションがタイムアウトになるまでの最短時間を秒単位で定義する整数のプロパティです。 既定値は 2700 秒です。 この時間を経過すると、メモリが必要な場合に限り、アイドル状態のセッションがサーバーによって終了されます。  
  
 `Port`  
 サーバーがクライアント接続をリッスンするポート番号を定義する整数のプロパティです。 このプロパティを設定しない場合、サーバーは最初の未使用ポートを動的に検出します。  
  
 このプロパティの既定値は 0 であり、ポート 2383 が既定により使用されます。 ポートの構成の詳細については、「 [Analysis Services のアクセスを許可するための Windows ファイアウォールの構成](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)」をご覧ください。  
  
 `ServerTimeout`  
 クエリのタイムアウトを秒単位で定義する整数です。 既定値は 3600 秒 (60 分) です。 ゼロ (0) はクエリがタイムアウトにならないことを指定します。  
  
 `TempDir`  
 処理、復元、その他の操作時に使用する一時ファイルの格納場所を指定する文字列プロパティです。 このプロパティの既定値は、セットアップによって指定されます。 このプロパティを指定しない場合、既定値は Data ディレクトリです。  
  
## <a name="requestprioritization-category"></a>要求の優先順位付けカテゴリ  
 `Enabled`  
 詳細プロパティです。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] サポートの指示がない限り、変更しないでください。  
  
 `StatisticsStoreSize`  
 詳細プロパティです。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] サポートの指示がない限り、変更しないでください。  
  
## <a name="see-also"></a>参照  
 [Analysis services サーバーのプロパティを構成します。](server-properties-in-analysis-services.md)   
 [Analysis Services インスタンスのサーバー モードの決定](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
