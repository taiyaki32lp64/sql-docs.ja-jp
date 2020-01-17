---
title: Integration Services サービスによってログに記録されるイベント | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- service [Integration Services], events
- events [Integration Services], service
- Integration Services service, events
ms.assetid: d4122dcf-f16f-47a0-93a2-ffa3d0d4f9cf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8b2f033557c566050dffbd82bc64df84feabb7b6
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296926"
---
# <a name="events-logged-by-the-integration-services-service"></a>Integration Services サービスによってログに記録されるイベント

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、各種のメッセージを Windows アプリケーション イベント ログに記録します。 これらのメッセージは、サービスの起動時、サービスの停止時、および特定の問題の発生時にログに記録されます。  
  
 このトピックでは、アプリケーション イベント ログに記録される一般的なイベント メッセージについて説明します。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、SQLISService のイベント ソースを使用してこのトピックで説明されているすべてのメッセージをログに記録します。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの概要については、「[Integration Services サービス &#40;SSIS サービス&#41;](../../integration-services/service/integration-services-service-ssis-service.md)」を参照してください。  
  
## <a name="service-status-messages"></a>サービスの状態メッセージ
 インストールで [ [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ] を選択すると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスがインストールおよび起動され、スタートアップの種類が自動に設定されます。  
  
|イベント ID|シンボル名|Text|注|  
|--------------|-------------------|----------|-----------|  
|256|DTS_MSG_SERVER_STARTING|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] サービスを開始しています。|サービスが開始されようとしています。|  
|257|DTS_MSG_SERVER_STARTED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] サービスが開始されました。|サービスが開始されました。|  
|260|DTS_MSG_SERVER_START_FAILED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] サービスを開始できませんでした。%nエラー: %1|サービスを開始できませんでした。 開始できないのは、インストールが破損したか、サービス アカウントが適切でないことが原因である可能性があります。|  
|258|DTS_MSG_SERVER_STOPPING|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] サービスを停止しています。%n%n実行中のパッケージはサーバー終了時にすべて停止します: %1|サービスを停止しています。また、パッケージを停止するようにサービスを構成している場合は、実行中のパッケージもサービスによってすべて停止されます。 構成ファイルで true 値または false 値を設定して、サービスの停止時に実行中のパッケージを停止するかどうかを指定できます。 このイベントのメッセージには、この設定値が含まれています。|  
|259|DTS_MSG_SERVER_STOPPED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] サービスが停止しました。%nサーバーのバージョン %1|サービスが停止しました。|  
  
## <a name="settings-file-messages"></a>設定ファイルのメッセージ  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの設定は、変更可能な XML ファイルに格納されています。 詳細については、「[Integration Services サービス (SSIS サービス)](../../integration-services/service/integration-services-service-ssis-service.md)」を参照してください。  
  
|イベント ID|シンボル名|Text|注|  
|--------------|-------------------|----------|-----------|  
|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] サービス: %n構成ファイルを指定するレジストリ設定がありません。 %n既定の構成ファイルを読み込もうとしています。|構成ファイルのパスを含むレジストリ エントリが存在しないか、空です。|  
|272|DTS_MSG_SERVER_MISSING_CONFIG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] サービス構成ファイルが存在しません。%n既定の設定を使用して読み込んでいます。|指定した場所に構成ファイル自体が存在しません。|  
|273|DTS_MSG_SERVER_BAD_CONFIG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] サービス構成ファイルが正しくありません。%n構成ファイルの読み取り中にエラーが発生しました: %1%n%n既定の設定を使用してサーバーを読み込んでいます。|構成ファイルを読み取ることができないか、無効です。 このエラーは、ファイル内の XML 構文エラーによって発生する可能性があります。|  
  
## <a name="other-messages"></a>その他のメッセージ  
  
|イベント ID|シンボル名|Text|注|  
|--------------|-------------------|----------|-----------|  
|336|DTS_MSG_SERVER_STOPPING_PACKAGE|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] サービス: 実行中のパッケージを停止しています。%nパッケージ インスタンス ID: %1%nパッケージ ID: %2%nパッケージ名: %3%nパッケージの説明: %4%nパッケージ|実行中のパッケージをサービスが停止しようとしています。 実行中のパッケージは、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] で監視および停止できます。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] でパッケージを管理する方法については、「[パッケージの管理 &#40;SSIS サービス&#41;](../../integration-services/service/package-management-ssis-service.md)」を参照してください。|  

## <a name="view-events"></a>イベントの表示
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスのイベントを表示できるツールには、次の 2 つがあります。  
  
-   **の** [ログ ファイルの表示] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ダイアログ ボックス。 **[ログ ファイルの表示]** ダイアログ ボックスには、ログのエクスポート、フィルター、および検索を行うオプションがあります。 **[ログ ファイルの表示]** のオプションの詳細については、「 [[ログ ファイルの表示] の F1 ヘルプ](../../relational-databases/logs/log-file-viewer-f1-help.md)」を参照してください。  
  
-   Windows イベント ビューアー。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスによってログに記録されるイベントの詳細については、「 [Integration Services サービスによってログに記録されるイベント](../../integration-services/service/events-logged-by-the-integration-services-service.md)」を参照してください。  
  
### <a name="to-view-service-events-for-integration-services-in-sql-server-management-studio"></a>SQL Server Management Studio で Integration Services のサービス イベントを表示するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を開きます。  
  
2.  **[ファイル]** メニューの **[オブジェクト エクスプローラーを接続]** をクリックします。  
  
3.  **[サーバーへの接続]** ダイアログ ボックスで [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のサーバーの種類を選択し、接続するサーバー名を選択または参照して、 **[接続]** をクリックします。  
  
4.  オブジェクト エクスプローラーで [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] を右クリックして、 **[ログの表示]** をクリックします。  
  
5.  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のイベントを表示するには、 **[SQL Server Integration Services]** を選択します。 **[NT イベント]** オプションは、 **[SQL Server Integration Services]** オプションに応じて、自動的に選択または選択解除されます。  
  
### <a name="to-view-service-events-for-integration-services-in-windows-event-viewer"></a>Windows イベント ビューアーで Integration Services のサービス イベントを表示するには  
  
1.  **[コントロール パネル]** で、クラシック表示を使用している場合は **[管理ツール]** 、カテゴリの表示を使用している場合は **[パフォーマンスとメンテナンス]** をクリックしてから **[管理ツール]** をクリックします。  
  
2.  **[イベント ビューアー]** をクリックします。  
  
3.  **[イベント ビューアー]** ダイアログ ボックスで、 **[アプリケーション]** をクリックします。  
  
4.  **[アプリケーション]** スナップインから **[ソース]** 列の値が **[SQLISService]** のエントリを探して右クリックし、 **[プロパティ]** をクリックします。  
  
5.  必要に応じて、上矢印または下矢印をクリックして、前後のイベントを表示します。  
  
6.  必要に応じて、[クリップボードにコピー] アイコンをクリックして、イベントの情報をコピーします。  
  
7.  イベントのデータをバイトと単語のどちらで表示するか選択します。  
  
8.  **[OK]** をクリックします。  
  
9. **[ファイル]** メニューの **[終了]** をクリックして、 **[イベント ビューアー]** ダイアログ ボックスを閉じます。  
 
## <a name="related-tasks"></a>Related Tasks  
 ログ エントリを表示する方法については、「 [Integration Services パッケージによってログに記録されるイベント](../../integration-services/performance/events-logged-by-an-integration-services-package.md)  
