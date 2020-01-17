---
title: データベース エンジンのインスタンス (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: af9ae643-9866-4014-b36f-11ab556a773e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2d5f89f5e3aa801386642bfb75470cef15db6e96
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68012053"
---
# <a name="database-engine-instances-sql-server"></a>データベース エンジンのインスタンス (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスは、オペレーティング システム サービスとして実行される **sqlservr** 実行可能ファイルのコピーです。 各インスタンスは、いくつかのシステム データベースと、1 つまたは複数のユーザー データベースを管理します。 各コンピューターは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]の複数のインスタンスを実行できます。 アプリケーションはインスタンスに接続して、インスタンスに管理されているデータベースでの作業を実行します。  
  
## <a name="instances"></a>インスタンス  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスは、そのインスタンスで管理されているいずれかのデータベースのデータを操作するすべてのアプリケーション要求を処理するサービスとして動作します。 アプリケーションからの接続要求 (ログイン) の送信先です。 アプリケーションとインスタンスが別のコンピューター上にある場合、接続はネットワーク接続を通じて確立されます。 アプリケーションとインスタンスが同じコンピューター上にある場合、SQL Server 接続はネットワーク接続としてもインメモリ接続としても確立できます。 接続が完了すると、アプリケーションは接続を通じてインスタンスに [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを送信します。 インスタンスは [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントをデータベース内のデータおよびオブジェクトに対する操作に解決して、必要な権限がログイン資格情報に付与されていれば、操作を実行します。 取得されたデータは、エラーなどのメッセージと共にアプリケーションに返されます。  
  
 1 台のコンピューター上で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] の複数のインスタンスを実行できます。 1 つのインスタンスを既定のインスタンスにすることができます。 既定のインスタンスには名前がありません。 接続要求にコンピューター名しか指定されていない場合、接続は既定のインスタンスに対して確立されます。 名前付きインスタンスは、インスタンスをインストールするときに名前を指定するインスタンスです。 このインスタンスに対する接続要求では、コンピューター名とインスタンス名の両方を指定する必要があります。 既定のインスタンスのインストールは必須ではありません。コンピューターで実行されているすべてのインスタンスが名前付きインスタンスであってもかまいません。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|インスタンスのプロパティを構成する方法について説明します。 ファイルの場所、データ形式などの既定値や、インスタンスがオペレーティング システムのリソース (メモリ、スレッドなど) をどのように使用するかを構成します。|[データベース エンジンのインスタンスの構成 &#40;SQL Server&#41;](../../database-engine/configure-windows/configure-database-engine-instances-sql-server.md)|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスの照合順序を管理する方法について説明します。 照合順序では、文字を表現するために使用されるビット パターンと、関連付けられている動作 (並べ替え、比較操作での大文字と小文字またはアクセントの区別など) が定義されます。|[照合順序と Unicode のサポート](../../relational-databases/collations/collation-and-unicode-support.md)|  
|インスタンスで実行される [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが別の OLE DB データ ソースに格納されているデータを操作できるように、リンク サーバー定義を構成する方法について説明します。|[リンク サーバー &#40;データベース エンジン&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)|  
|ログオン試行の検証後、インスタンスのリソースの操作が開始される前に行われる動作を指定する、ログオン トリガーを作成する方法について説明します。 ログオン トリガーは、接続アクティビティのログ記録や、Windows および SQL Server による資格情報認証に加えて行われるロジックに基づくログイン制限などの動作をサポートしています。|[ログオン トリガー](../../relational-databases/triggers/logon-triggers.md)|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに関連付けられているサービスを管理する方法について説明します。 これには、サービスの開始と停止、スタートアップ オプションの構成などの動作が含まれています。|[データベース エンジン サービスの管理](../../database-engine/configure-windows/manage-the-database-engine-services.md)|  
|プロトコルの有効化、プロトコルで使用されるポートやパイプの変更、暗号化の構成、SQL Server Browser サービスの構成、ネットワーク上での SQL Server データベース エンジンの公開または非表示、サーバー プリンシパル名の登録など、サーバーのネットワーク構成タスクを実行する方法について説明します。|[サーバー ネットワークの構成](../../database-engine/configure-windows/server-network-configuration.md)|  
|クライアント プロトコルの構成やサーバーの別名の作成または削除など、クライアントのネットワーク構成タスクを実行する方法について説明します。|[クライアント ネットワーク構成](../../database-engine/configure-windows/client-network-configuration.md)|  
|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] スクリプトなどのスクリプトの設計、デバッグ、および実行に使用できる [!INCLUDE[tsql](../../includes/tsql-md.md)] エディターについて説明します。 SQL Server コンポーネントを操作する Windows PowerShell スクリプトを記述する方法についても説明します。|[データベース エンジン スクリプト](../../relational-databases/scripting/database-engine-scripting.md)|  
|インスタンスの一般的な管理タスクのワークフローを指定するメンテナンス プランを使用する方法について説明します。 ワークフローには、データベースのバックアップや、パフォーマンスを向上させるための統計情報の更新などのタスクが含まれます。|[メンテナンス プラン](../../relational-databases/maintenance-plans/maintenance-plans.md)|  
|アプリケーション要求で使用可能な CPU とメモリの量の制限を指定することによってリソース消費量と負荷を管理するためにリソース ガバナーを使用する方法について説明します。|[リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)]から電子メール メッセージを送信するために、データベース アプリケーションがどのようにデータベース メールを使用できるかについて説明します。|[データベース メール](../../relational-databases/database-mail/database-mail.md)|  
|パフォーマンス基準の策定やパフォーマンスの問題の診断に使用できるパフォーマンス データをキャプチャするために拡張イベントを使用する方法について説明します。 拡張イベントは、パフォーマンス データを収集するための軽量で拡張性の高いシステムです。|[拡張イベント](../../relational-databases/extended-events/extended-events.md)|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)]のイベントのキャプチャおよび記録用にカスタマイズされたシステムを構築するために SQL トレースを使用する方法について説明します。|[SQL トレース (SQL Trace)](../../relational-databases/sql-trace/sql-trace.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが受け取ったアプリケーション要求のトレースをキャプチャするために [!INCLUDE[ssDE](../../includes/ssde-md.md)]Profiler を使用する方法について説明します。 これらのトレースは、後でパフォーマンスのテストや問題の診断などの活動のために再生できます。|[SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)|  
|変更データ キャプチャ (CDC) 機能および変更の追跡機能について説明し、これらの機能を使用してデータベースのデータに対する変更を追跡する方法について説明します。|[データ変更の追跡 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)|  
|さまざまなログ ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ジョブ履歴、SQL Server ログ、Windows イベント ログなど) 内の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラーやメッセージを検索および表示するために [ログ ファイルの表示] を使用する方法について説明します。|[ログ ファイルの表示](../../relational-databases/logs/log-file-viewer.md)|  
|データベースを分析し、潜在的なパフォーマンスの問題に対処する提案を行うために [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーを使用する方法について説明します。|[Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)|  
|標準接続が受け入れられないときに実稼働データベース管理者がインスタンスへの診断接続を確立する方法について説明します。|[データベース管理者用の診断接続](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] の 1 つのインスタンスから別のインスタンスにアクセスできるようにする、非推奨のリモート サーバー機能を使用する方法について説明します。 この機能のための推奨メカニズムは、リンク サーバーです。|[リモート サーバー](../../database-engine/configure-windows/remote-servers.md)|  
|メッセージング アプリケーションおよびキューイング アプリケーションのための Service Broker の機能について説明し、Service Broker のドキュメントを示します。|[Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)|  
|バッファー プール拡張が、不揮発性ランダム アクセス ストレージ (ソリッドステート ドライブ) とデータベース エンジン バッファー プールとのシームレスな統合をどのように実現し、I/O スループットを大幅に向上させるかについて説明します。|[バッファー プール拡張ファイル](../../database-engine/configure-windows/buffer-pool-extension.md)|  
  
## <a name="see-also"></a>参照  
 [sqlservr アプリケーション](../../tools/sqlservr-application.md)   
 [データベース機能](../../relational-databases/database-features.md)   
 [データベース エンジンのインスタンス間機能](../../relational-databases/database-engine-cross-instance-features.md)  
  
  
