---
title: ナレッジ ベースの作成
ms.date: 06/04/2013
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.selectkb.f1
- sql13.dqs.kb.newkb.f1
ms.assetid: 2733a284-975f-4650-abcc-cc2aad074cab
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 20421ab3584eac51feb09ba717f293449825574c
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247334"
---
# <a name="create-a-knowledge-base"></a>ナレッジ ベースの作成

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  このトピックでは、 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) でナレッジ ベースを作成し、ドメイン管理、ナレッジ検出、または照合ポリシーの追加の準備を行う方法について説明します。  
  
##  <a name="BeforeYouBegin"></a>開始する前に  
  
###  <a name="Prerequisites"></a>応募  
 ナレッジ ベースを作成するには、 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] と [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]をインストールしている必要があります。  
  
###  <a name="Security"></a>保護  
  
####  <a name="Permissions"></a>許可  
 ナレッジ ベースを作成するには、DQS_MAIN データベースの dqs_kb_editor ロールまたは dqs_administrator ロールが必要です。  
  
##  <a name="Createaknowledgebase"></a>ナレッジベースの作成  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client アプリケーションを実行](../data-quality-services/run-the-data-quality-client-application.md)します。  
  
2.  
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で **[新しいナレッジ ベース]** をクリックします。  
  
3.  新しいナレッジ ベースの名前と説明を入力します。  
  
4.  
  **[次の場所からナレッジ ベースを作成]** で、ナレッジ ベースを作成する際に基にするナレッジ ベースを選択します。  
  
    -   新しいナレッジ ベースを作成する際に既存のナレッジ ベースまたはデータ ファイルを基にしない場合は、 **[なし]** を選択します。  
  
    -   新しいナレッジ ベースを作成する際に、 **で既に作成されているナレッジ ベースまたは既定のナレッジ ベースを基にする場合は、** [既存のナレッジ ベース] [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]を選択します。 
  **[ナレッジ ベースの選択]** ボックスの一覧でナレッジ ベースを選択するか、 **[参照]** をクリックして **[ナレッジ ベースの選択]** ダイアログ ボックスを表示し、新しいナレッジ ベースを作成する際に基にする既存のナレッジ ベースを選択して、 **[OK]** をクリックします。 ナレッジ ベースをタブレットから選択する場合は、ナレッジ ベースのドメインと照合ルールがダイアログ ボックスの右側のペインに表示されます。 
  **[DQS データ]** ナレッジ ベースを選択することもできます。これは、米国の企業、住所、および関係者のデータに関連する、追加設定なしで使用できる一般的なドメインおよびナレッジを含む既定のナレッジ ベースです。  
  
    -   新しいナレッジ ベースを作成する際に **の DQS ファイルを基にする場合は、** [DQS ファイルからインポート] [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]を選択します。 
  **[参照]** をクリックし、拡張子が .dqs の DQS データ ファイルを選択して、 **[OK]** をクリックします。  
  
5.  
  **[アクティビティの選択]** で、新しいナレッジ ベースに対して実行するアクティビティを選択します。  
  
    -   
  **[ドメイン管理]** を選択すると、ナレッジ ベースが作成され、ナレッジ ベースのドメインを変更するための画面が表示されます。  
  
    -   
  **[ナレッジ検出]** を選択すると、ナレッジ ベースが作成され、データ サンプルを分析して結果をナレッジ ベースのドメインに設定するためのウィザードが表示されます。  
  
    -   
  **[照合ポリシー]** を選択すると、照合ポリシーを作成してナレッジ ベースに追加します。  
  
6.  
  **[作成]** をクリックします。  
  
##  <a name="FollowUp"></a>補足情報: ナレッジベースを作成した後  
 ナレッジ ベースを作成した後は、ナレッジ検出を実行するためのウィザード、照合ポリシーを作成するためのウィザード、またはドメイン管理を実行するためのページが表示されます。 ナレッジ検出、ドメイン管理、または照合ポリシーについて詳しくは、「[ナレッジ検出の実行](../data-quality-services/perform-knowledge-discovery.md)」、「[ドメインの管理](../data-quality-services/managing-a-domain.md)」、または「[照合ポリシーの作成](../data-quality-services/create-a-matching-policy.md)」をご覧ください。  
  
  
