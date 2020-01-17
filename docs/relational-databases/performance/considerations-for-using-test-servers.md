---
title: テスト サーバーの使用に関する注意点 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- overhead [Database Engine Tuning Advisor]
- tuning overhead [SQL Server]
- reducing production server tuning load
- Database Engine Tuning Advisor [SQL Server], test servers
- xp_msver
- test servers [Database Engine Tuning Advisor]
- production servers [SQL Server]
- offload tuning overhead [SQL Server]
ms.assetid: 94e6c3e5-1f09-4616-9da2-4e44d066d494
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: a1cf7a4bb37abd60f7067381ba4da6a2d44328ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946984"
---
# <a name="considerations-for-using-test-servers"></a>テスト サーバーの使用に関する注意点
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  実稼働サーバー上のデータベースのチューニングにテスト サーバーを使用することは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーの大きな利点です。 この機能を使用して、実際のデータを実稼働サーバーからテスト サーバーにコピーすることなく、チューニングにかかるオーバーヘッドをテスト サーバーに移行できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーのグラフィカル ユーザー インターフェイス (GUI) では、テスト サーバーのチューニング機能はサポートされません。  
  
 この機能を正しく使用するために、以下のセクションの考慮事項を確認してください。  
  
## <a name="setting-up-the-test-serverproduction-server-environment"></a>テスト サーバー/実稼働サーバー環境の設定  
  
-   実稼働サーバー上のデータベースをチューニングするためにテスト サーバーを使用するユーザーは、両方のサーバーに存在している必要があります。存在しない場合、このシナリオは失敗します。  
  
-   テスト サーバーと実稼働サーバーのシナリオでは、拡張ストアド プロシージャ **xp_msver**を有効にする必要があります。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーでは、この拡張ストアド プロシージャを使用して、実稼働サーバーのプロセッサ数と使用可能なメモリをフェッチし、テスト サーバーでのチューニングに使用します。 **xp_msver** が有効ではない場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーでは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーを実行しているコンピューターのハードウェア特性が想定値として使用されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーを実行しているコンピューターのハードウェア特性を推定できない場合は、1 つのプロセッサと 1,024 MB のメモリがあると仮定します。 この拡張ストアド プロシージャは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールしたときに既定でオンになっています。 詳細については、「[セキュリティ構成](../../relational-databases/security/surface-area-configuration.md)」および「[xp_msver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-msver-transact-sql.md)」を参照してください。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーでは、テスト サーバーと実稼働サーバーの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエディションが同じである必要があります。 2 つの異なるエディションがある場合は、テスト サーバーのエディションが優先されます。 たとえば、テスト サーバーで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard が実行されている場合は、実稼働サーバーで実行されているのが [!INCLUDE[ssDE](../../includes/ssde-md.md)] Enterprise であっても、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] チューニング アドバイザーの推奨設定にはインデックス付きビュー、パーティション分割、およびオンライン操作は含まれません。  
  
## <a name="about-test-serverproduction-server-behavior"></a>テスト サーバー/実稼働サーバーの動作について  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーでは、推奨設定の作成時に実稼働サーバーとテスト サーバー間のハードウェア上の違いが考慮されます。 推奨設定は、実稼働サーバーだけでチューニングを行った場合と同じになります。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーでは、チューニングに必要な統計情報を作成したり、メタデータを収集するために、実稼働サーバーにある程度負荷をかける場合があります。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーでは、実稼働サーバーからテスト サーバーに実際のデータがコピーされることはありません。 データベースのメタデータと必要な統計情報がコピーされるだけです。  
  
-   すべてのセッション情報が、実稼働サーバー上の **msdb** に格納されます。 そのため、使用可能なテスト サーバーはすべてチューニングに利用でき、すべてのセッションについての情報を 1 か所 (実稼働サーバー) で使用できます。  
  
## <a name="issues-related-to-the-shell-database"></a>シェル データベースに関連する問題  
  
-   チューニング後は、チューニング処理中に [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーによってテスト サーバー上に作成されたすべてのメタデータが削除されます。 シェル データベースも削除されます。 同じ実稼働サーバーとテスト サーバーを使って一連のチューニング セッションを実行する場合は、このシェル データベースを保持しておいて時間を節約することができます。 XML 入力ファイルでは、 **RetainShellDB** サブ要素を、 **TuningOptions** 親要素の下のその他のサブ要素と共に指定します。 これらのオプションを使用することで、[!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーでシェル データベースが保持されるようになります。 詳細については、「[XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)」を参照してください。  
  
-   テスト サーバー/実稼働サーバーのチューニング セッションが成功した後、**RetainShellDB** サブ要素を指定していないにもかかわらず、シェル データベースがテスト サーバーに残る場合があります。 こうした不要なシェル データベースはその後のチューニング セッションに干渉する可能性があるため、別のテスト サーバー/実稼働サーバーのチューニング セッションを実行する前に削除する必要があります。 また、チューニング セッションが予期せず終了した場合は、テスト サーバー上のシェル データベースと、それらのデータベース内のオブジェクトが、テスト サーバー上に残る可能性があります。 これらのデータベースとオブジェクトも、新しいテスト サーバー/実稼働サーバーのチューニング セッションを開始する前に削除する必要があります。  
  
## <a name="issues-related-to-the-tuning-process"></a>チューニング処理に関連する問題  
  
-   ユーザーは、実稼働サーバーとテスト サーバー間の違いに起因するチューニング エラーと、実稼働サーバーからテスト サーバーへのメタデータのコピーに起因するエラーについて、チューニング ログを確認する必要があります。 たとえば、ユーザーのログイン情報がテスト サーバーに存在しない場合があります。 ユーザーのログインがテスト サーバーに存在しない場合、ワークロード内のイベントのうち、そのユーザー ログインによって発生するイベントをチューニングできない場合があります。 チューニング ログを表示するには、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーの GUI を使用します。 詳細については、「 [データベース エンジン チューニング アドバイザーからの出力の表示および操作](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)」を参照してください。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーによってテスト サーバー上に作成されるシェル データベースにオブジェクトが見つからないために、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーで多数のイベントをチューニングできない場合は、チューニング ログを確認する必要があります。 チューニングできないイベントは、ログに記録されます。 テスト サーバー上のデータベースを正常にチューニングするには、シェル データベースに見つからないオブジェクトを作成してから新しいチューニング セッションを開始する必要があります  
  
-   同一名のデータベースが既にテスト サーバー上に存在する場合は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーではメタデータがコピーされずにチューニングが続行され、必要に応じて統計情報が収集されます。 これは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーを起動する前に、ユーザーが既にデータベースをテスト サーバー上に作成し、適切なメタデータをコピーし終わっている場合に便利です。  
  
-   DATE_CORRELATION_OPTIMIZATION オプションが実稼働サーバー上のデータベースに対して有効になっていると、メタデータと、このオプションに関連付けられているデータの一部が、テスト サーバーのチューニング中にスクリプト化されません。 テスト サーバーと実稼働サーバーのシナリオでチューニングを実行する場合、次の問題が当てはまる場合があります。  
  
    -   DATE_CORRELATION_OPTIMIZATION オプションを使用するクエリの場合、サーバー間でクエリ プランが異なることがあります。  
  
    -   [!INCLUDE[ssDE](../../includes/ssde-md.md)] インデックス付きビューの推奨設定スクリプトで DATE_CORRELATION_OPTIMIZATION オプションを設定している場合、チューニング アドバイザーからそのビューを削除するように提示されることがあります。  
  
     このため、相関関係の統計情報を保持するインデックス付きビューについては、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーによって作成される推奨設定を無視してもかまいません。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーでは、このようなインデックス付きビューのコストのみが認識され、利点が認識されないためです。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーでは、DATE_CORRELATION_OPTIMIZATION が有効であれば有益だった可能性がある **datetime** 列のクラスター化インデックスなど、特定のインデックスの選択が推奨されない場合があります。  
  
     特定のビューが相関関係の統計情報に基づいているかどうかを判断するには、 **sys.views** カタログ ビューの [is_date_correlation_view](../../relational-databases/system-catalog-views/sys-views-transact-sql.md) 列を選択します。  
  
  
