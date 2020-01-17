---
title: .dqs ファイルからのナレッジ ベースのインポート | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 9b9786fe-9e80-429a-afcb-dc3b3dd6f0b0
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: f31f93ba468e6ffc91313e7ca653d122c1664ad2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65480663"
---
# <a name="import-a-knowledge-base-from-a-dqs-file"></a>.dqs ファイルからのナレッジ ベースのインポート
  このトピックでは、 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) で .dqs データ ファイルからナレッジ ベース全体をインポートする方法について説明します。 データ ファイルは、既存のナレッジ ベースを [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] アプリケーションでエクスポートすることによって作成します (「 [ナレッジ ベースを .dqs ファイルにエクスポート](../../2014/data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)」を参照)。  
  
 .dqs データ ファイルを使用してナレッジ ベースのコンテンツをエクスポートし、後でそのコンテンツを同じ [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] の別のナレッジ ベースや異なる [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] にインポートすることで、ナレッジの生成処理を簡略化し、時間と労力を節約します。 ナレッジ ベースやその中のナレッジを他のユーザーと共有でき、他のユーザーの時間を節約できます。 .dqs ファイルには、ドメインや照合ポリシーを含むナレッジ ベースのすべての情報が含まれます。ただし、アタッチされた参照データ情報は含まれません。 発行済みのデータと発行されていないデータがインポートされます。  
  
 .dqs データ ファイルは、表示できないように暗号化されています。  
  
 ナレッジ ベースをインポートする際に同じ名前を使用できますが、クライアント アプリケーションにそのナレッジ ベースの名前が既に存在する場合は名前を変更する必要があります。  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Prerequisites"></a> 前提条件  
 ナレッジ ベースを .dqs ファイルからインポートするには、事前にナッレジ ベースを .dqs ファイルにエクスポートしている必要があります。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 ナレッジ ベースを .dqs データ ファイルからインポートするには、DQS_MAIN データベースの dqs_kb_editor ロールまたは dqs_administrator ロールが必要です。  
  
##  <a name="Import"></a> .dqs ファイルからのナレッジ ベースのインポート  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)]「[Data Quality Client アプリケーションの実行](../../2014/data-quality-services/run-the-data-quality-client-application.md)」をご覧ください。  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で **[新しいナレッジ ベース]** をクリックします。  
  
3.  ナレッジ ベースの名前を入力します。  
  
4.  **[次の場所からナレッジ ベースを作成]** の下矢印をクリックし、 **[DQS ファイルからインポート]** をクリックします。  
  
5.  **[データ ファイルの選択]** で **[参照]** をクリックします。  
  
6.  **[データ ファイルからインポート]** ダイアログ ボックスで、インポートする .dqs ファイルを含むフォルダーに移動してファイル名をクリックします。 **[開く]** をクリックします。  
  
7.  正しいナレッジ ベースとドメインが **[ドメイン]** リストに表示されていることを確認します。  
  
8.  実行するアクティビティを選択して **[作成]** をクリックします。  
  
9. **[ナレッジ ベースのインポート]** ダイアログ ボックスで、ステータス行にインポートの完了が表示されていることを確認します。 [**OK**] をクリックします。  
  
10. 必要なナレッジ検出、ドメイン管理、または照合ポリシー タスクを実行し、 **[完了]** をクリックします。  
  
11. ナレッジ ベースのナレッジを発行する場合は **[発行]** をクリックし、発行しない場合は **[いいえ]** をクリックします。  
  
12. ナレッジ ベースを発行した場合は **[OK]** をクリックします。  
  
13. Data Quality Services のホーム ページで、 **[最近使用したナレッジ ベース]** の下にナレッジ ベースが表示されていることを確認します。  
  
##  <a name="FollowUp"></a>補足情報: .dqs ファイルからナレッジ ベースをインポートした後  
 .dqs ファイルからナレッジ ベースをインポートした後で、ナレッジ ベースのコンテンツに応じてナレッジをナレッジ ベースに追加したり、ナレッジ ベースをクレンジング プロジェクトや照合プロジェクトで使用したりすることができます。 詳しくは、「[ナレッジ検出の実行](../../2014/data-quality-services/perform-knowledge-discovery.md)」、「[ドメインの管理](../../2014/data-quality-services/managing-a-domain.md)」、「[複合ドメインの管理](../../2014/data-quality-services/managing-a-composite-domain.md)」、「[照合ポリシーの作成](../../2014/data-quality-services/create-a-matching-policy.md)」、「[データ クレンジング](../../2014/data-quality-services/data-cleansing.md)」、または「[データ照合](../../2014/data-quality-services/data-matching.md)」をご覧ください。  
  
  
