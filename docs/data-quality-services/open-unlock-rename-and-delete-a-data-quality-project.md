---
title: データ品質プロジェクトを開く、ロックを解除する、名前を変更する、削除する
description: SQL Server Data Quality Services を使用してデータ品質プロジェクトを開く、ロックを解除する、名前を変更する、および削除する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.dqproject.opendqproject.f1
helpviewer_keywords:
- data quality project,delete
- data quality project,rename
- data quality project,unlock
- data quality project,open
ms.assetid: de8a2b04-4673-4beb-b4cf-96a28cdf3a93
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 666e7fdbc080af3ed259dae978bd782e437eae2e
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75557808"
---
# <a name="open-unlock-rename-and-delete-a-data-quality-project---data-quality-services-dqs"></a>データ品質プロジェクトを開く、ロックを解除する、名前を変更する、削除する-Data Quality Services (DQS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  このトピックでは、データ品質プロジェクトを開く、ロック解除、名前の変更、削除などの、 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] を使用したデータ品質プロジェクトの管理方法について説明します。  
  
##  <a name="BeforeYouBegin"></a>開始する前に  
  
###  <a name="LimitationsRestrictions"></a>制限事項と制約事項  
  
-   他のユーザーによって作成された、ロックされているプロジェクトは開くことができません。  
  
-   他のユーザーによって作成されたデータ品質プロジェクトのロック解除、名前の変更、または削除はできません。  
  
-   ロックされたデータ品質プロジェクトを削除することはできません。 削除するには先にロックを解除する必要があります。  
  
-   自分が作成したデータ品質プロジェクトのみロックを解除することができます。  
  
###  <a name="Prerequisites"></a>応募  
 管理対象のデータ品質プロジェクトが少なくとも 1 つ必要です。  
  
###  <a name="Security"></a>保護  
  
####  <a name="Permissions"></a>許可  
 データ品質プロジェクトを管理するには、DQS_MAIN データベースに対する dqs_kb_editor または dqs_kb_operator ロールが必要です。  
  
##  <a name="Open"></a>データ品質プロジェクトを開く  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client アプリケーションを実行](../data-quality-services/run-the-data-quality-client-application.md)します。  
  
2.  
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で、 **[データ品質プロジェクトを開く]** をクリックします。 
  **[プロジェクトを開く]** 画面が表示されます。  
  
     または、 **[最近使用したデータ品質プロジェクト]** 領域の下に表示されるデータ品質プロジェクトをクリックして直接開くこともできます。  
  
3.  
  **[プロジェクトを開く]** 画面で、開きたいデータ品質プロジェクトをクリックして選択し、 **[次へ]** をクリックします。  
  
4.  最後に閉じられたときと同じアクティビティの状態でデータ品質プロジェクトが開きます。 データ品質プロジェクトには次の状態があります。  
  
    -   
  **クレンジング** アクティビティでは、データ品質プロジェクトは**クレンジング - マップ**、**クレンジング - 最適化**、**クレンジング - 結果の管理と表示**、および**クレンジング - エクスポート**の状態を取ります。  
  
    -   
  **照合**アクティビティでは、データ品質プロジェクトは**照合 - マップ**、**照合 - 照合**、**照合 - サバイバーシップ**、および**照合 - エクスポート**の状態を取ります。  
  
##  <a name="Unlock"></a>データ品質プロジェクトのロック解除  
 データ品質プロジェクトを作成すると、プロジェクトは他のユーザーによる使用や変更を防ぐためにロック状態になります。 他のユーザーがデータ品質プロジェクトを操作できるようにするには、作業を完了した後にデータ品質プロジェクトのロックを解除する必要があります。 ロックされているプロジェクトには、ロック アイコンが表示されます。  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client アプリケーションを実行](../data-quality-services/run-the-data-quality-client-application.md)します。  
  
2.  
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で、 **[データ品質プロジェクトを開く]** をクリックします。 
  **[プロジェクトを開く]** 画面が表示されます。  
  
3.  
  **[プロジェクトを開く]** 画面で、自分が作成したロックされているデータ品質プロジェクトを右クリックし、ショートカット メニューの **[ロック解除]** をクリックします。 緑のチェック マークがプロジェクトに表示され、ロックされていないことが示されます。  
  
##  <a name="Rename"></a>データ品質プロジェクトの名前を変更する  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client アプリケーションを実行](../data-quality-services/run-the-data-quality-client-application.md)します。  
  
2.  
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で、 **[データ品質プロジェクトを開く]** をクリックします。 
  **[プロジェクトを開く]** 画面が表示されます。  
  
3.  
  **[プロジェクトを開く]** 画面で、自分が作成したデータ品質プロジェクトを右クリックし、ショートカット メニューの **[名前の変更]** をクリックします。  
  
4.  
  **[名前]** 列のデータ品質プロジェクト名が編集可能になります。 新しい名前を入力して、Enter キーを押します。  
  
##  <a name="Delete"></a>データ品質プロジェクトの削除  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client アプリケーションを実行](../data-quality-services/run-the-data-quality-client-application.md)します。  
  
2.  
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で、 **[データ品質プロジェクトを開く]** をクリックします。 
  **[プロジェクトを開く]** 画面が表示されます。  
  
3.  
  **[プロジェクトを開く]** 画面で、自分が作成したロックされていないデータ品質プロジェクトを右クリックし、ショートカット メニューの **[削除]** をクリックします。  
  
4.  確認メッセージが表示されます。 
  **[はい]** をクリックします。  
  
  
