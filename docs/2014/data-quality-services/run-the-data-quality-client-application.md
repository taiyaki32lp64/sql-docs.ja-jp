---
title: Data Quality Client アプリケーションの実行 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.browseforservers.f1
- sql12.dqs.connecttoserver.f1
ms.assetid: 0b2aa202-7ab2-4c9d-b0f1-802588053a1e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: bbb790fc5067d1544cd4b3d9d6e90b34be8e2b77
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65484139"
---
# <a name="run-the-data-quality-client-application"></a>Data Quality Client アプリケーションの実行
  [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] を実行し、[!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] にログオンして、[!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] (DQS) を使用できます。  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Prerequisites"></a> 前提条件  
 DQSInstaller.exe ファイルを実行して [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] のインストールを完了しておく必要があります。 詳細については、「[Data Quality Server のインストールを完了するための DQSInstaller.exe の実行](install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)」をご覧ください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]にログオンするには、DQS_MAIN データベースに対して、3 つの DQS ロール (dqs_administrator、dqs_kb_editor、dqs_kb_operator) のいずれかが必要です。  
  
##  <a name="Run"></a> Data Quality Client の実行  
 インストール済みのコンピューターで [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] を実行するには、次の手順を実行します。  
  
1.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** をポイントして、 **[[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]]** 、 **[Data Quality Services]** 、 **[Data Quality Client]** の順にクリックします。  
  
2.  **[サーバーへの接続]** ダイアログ ボックスで、次の操作を実行します。  
  
    1.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] アプリケーションを接続するサーバーを指定します。 **[(ローカル)]** を選択し、ローカル コンピューター上の [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] に接続します。 または、下矢印をクリックし、 **[\<その他のサーバーをネットワークで参照>]** を選択して別のサーバーに接続する (またはローカル サーバーに名前で接続する) こともできます。 **[サーバーの参照]** ダイアログ ボックスが表示されます。 **[ローカル サーバー]** タブまたは **[ネットワーク サーバー]** タブでサーバーを選択できます。  
  
    2.  [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] と [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] の間のデータ転送を暗号化する場合は、 **[オプション]** をクリックし、 **[暗号化接続]** チェック ボックスをオンにします。  
  
3.  **[接続]** をクリックします。  
  
 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面が表示されます。 詳細については、「[Data Quality Client のホーム画面](../../2014/data-quality-services/data-quality-client-home-screen.md)」を参照してください。  
  
  
