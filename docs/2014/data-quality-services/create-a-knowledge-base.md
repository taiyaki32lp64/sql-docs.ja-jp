---
title: ナレッジ ベースの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.kb.selectkb.f1
- sql12.dqs.kb.newkb.f1
ms.assetid: 2733a284-975f-4650-abcc-cc2aad074cab
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2402a69f428fe0c9ba2359f100e2baf16e1a1d04
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65481004"
---
# <a name="create-a-knowledge-base"></a>ナレッジ ベースの作成
  このトピックでは、 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) でナレッジ ベースを作成し、ドメイン管理、ナレッジ検出、または照合ポリシーの追加の準備を行う方法について説明します。  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Prerequisites"></a> 前提条件  
 ナレッジ ベースを作成するには、 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] と [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]をインストールしている必要があります。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 ナレッジ ベースを作成するには、DQS_MAIN データベースの dqs_kb_editor ロールまたは dqs_administrator ロールが必要です。  
  
##  <a name="Createaknowledgebase"></a> Create a knowledge base  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)]「[Data Quality Client アプリケーションの実行](../../2014/data-quality-services/run-the-data-quality-client-application.md)」をご覧ください。  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で **[新しいナレッジ ベース]** をクリックします。  
  
3.  新しいナレッジ ベースの名前と説明を入力します。  
  
4.  **[次の場所からナレッジ ベースを作成]** で、ナレッジ ベースを作成する際に基にするナレッジ ベースを選択します。  
  
    -   新しいナレッジ ベースを作成する際に既存のナレッジ ベースまたはデータ ファイルを基にしない場合は、 **[なし]** を選択します。  
  
    -   新しいナレッジ ベースを作成する際に、 **で既に作成されているナレッジ ベースまたは既定のナレッジ ベースを基にする場合は、** [既存のナレッジ ベース] [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]を選択します。 **[ナレッジ ベースの選択]** ボックスの一覧でナレッジ ベースを選択するか、 **[参照]** をクリックして **[ナレッジ ベースの選択]** ダイアログ ボックスを表示し、新しいナレッジ ベースを作成する際に基にする既存のナレッジ ベースを選択して、 **[OK]** をクリックします。 ナレッジ ベースをタブレットから選択する場合は、ナレッジ ベースのドメインと照合ルールがダイアログ ボックスの右側のペインに表示されます。 **[DQS データ]** ナレッジ ベースを選択することもできます。これは、米国の企業、住所、および関係者のデータに関連する、追加設定なしで使用できる一般的なドメインおよびナレッジを含む既定のナレッジ ベースです。  
  
    -   新しいナレッジ ベースを作成する際に **の DQS ファイルを基にする場合は、** [DQS ファイルからインポート] [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]を選択します。 **[参照]** をクリックし、拡張子が .dqs の DQS データ ファイルを選択して、 **[OK]** をクリックします。  
  
5.  **[アクティビティの選択]** で、新しいナレッジ ベースに対して実行するアクティビティを選択します。  
  
    -   **[ドメイン管理]** を選択すると、ナレッジ ベースが作成され、ナレッジ ベースのドメインを変更するための画面が表示されます。  
  
    -   **[ナレッジ検出]** を選択すると、ナレッジ ベースが作成され、データ サンプルを分析して結果をナレッジ ベースのドメインに設定するためのウィザードが表示されます。  
  
    -   **[照合ポリシー]** を選択すると、照合ポリシーを作成してナレッジ ベースに追加します。  
  
6.  **[作成]** をクリックします。  
  
##  <a name="FollowUp"></a>補足情報: ナレッジ ベースを作成した後  
 ナレッジ ベースを作成した後は、ナレッジ検出を実行するためのウィザード、照合ポリシーを作成するためのウィザード、またはドメイン管理を実行するためのページが表示されます。 ナレッジ検出、ドメイン管理、または照合ポリシーについて詳しくは、「[ナレッジ検出の実行](../../2014/data-quality-services/perform-knowledge-discovery.md)」、「[ドメインの管理](../../2014/data-quality-services/managing-a-domain.md)」、または「[照合ポリシーの作成](../../2014/data-quality-services/create-a-matching-policy.md)」をご覧ください。  
  
  
