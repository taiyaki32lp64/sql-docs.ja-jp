---
title: Data Quality Client アプリケーションの実行
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.browseforservers.f1
- sql13.dqs.connecttoserver.f1
ms.assetid: 0b2aa202-7ab2-4c9d-b0f1-802588053a1e
author: swinarko
ms.author: sawinark
ms.openlocfilehash: da099b6a3aca31dd0acdc82f7e2bdbdf13c7c24e
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244129"
---
# <a name="run-the-data-quality-client-application"></a>Data Quality Client アプリケーションの実行

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]を実行して [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]にログオンします。  
  
##  <a name="BeforeYouBegin"></a>開始する前に  
  
###  <a name="Prerequisites"></a>応募  
 DQSInstaller.exe ファイルを実行して [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] のインストールを完了しておく必要があります。 詳細については、「 [Data Quality Server のインストールを完了するための DQSInstaller.exe の実行](../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)」をご覧ください。  
  
###  <a name="Security"></a>保護  
  
####  <a name="Permissions"></a>許可  
 
  [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]にログオンするには、DQS_MAIN データベースに対して、3 つの DQS ロール (dqs_administrator、dqs_kb_editor、dqs_kb_operator) のいずれかが必要です。  
  
##  <a name="Run"></a>実行 Data Quality Client  
 インストール済みのコンピューターで [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] を実行するには:  
  
1.  
  **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をポイントして、**[[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]]**、**[Data Quality Services]**、**[Data Quality Client]** の順にクリックします。  
  
2.  
  **[サーバーへの接続]** ダイアログ ボックスで、次の操作を実行します。  
  
    1.  
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] アプリケーションを接続するサーバーを指定します。 
  **[(ローカル)]** を選択し、ローカル コンピューター上の [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] に接続します。 また、下矢印をクリックし、[ ** \<その他の>サーバーのネットワークを参照**] を選択して、別のサーバーに接続する (またはローカルサーバーに名前で接続する) こともできます。 
  **[サーバーの参照]** ダイアログ ボックスが表示されます。 
  **[ローカル サーバー]** タブまたは **[ネットワーク サーバー]** タブでサーバーを選択できます。  
  
    2.  
  [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] と [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]の間のデータ転送を暗号化するには、 **[オプション]** をクリックし、 **[暗号化接続]** チェック ボックスをオンにします。  
  
3.  
  **[接続]** をクリックします。  
  
 
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面が表示されます。 詳細については、「[Data Quality Client のホーム画面](../data-quality-services/data-quality-client-home-screen.md)」を参照してください。  
  
  
