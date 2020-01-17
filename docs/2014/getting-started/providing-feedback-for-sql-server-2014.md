---
title: SQL Server 2014 に関するフィードバックの |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- sending feedback to Microsoft
- errors [SQL Server], feedback reporting
- feedback [SQL Server]
- submitting feedback [SQL Server]
- bug reporting [SQL Server]
- reporting usage information to Microsoft
- reporting errors to Microsoft
- SQL Server, feedback reporting
- documentation feedback [SQL Server]
- usage information reporting [SQL Server]
- product feedback [SQL Server]
- automatic error or usage reporting
ms.assetid: 28f3ebf0-ad71-4816-86a6-18a46f023cfe
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10466721f50dd8b090b5d6b1a06b5bffd6e5289d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62772279"
---
# <a name="providing-feedback-for-sql-server-2014"></a>SQL Server 2014 に関するフィードバックの送信
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 製品やドキュメントの改善にご協力いただき、ありがとうございます。 製品の機能やユーザー インターフェイスに関するご意見や不具合の報告を送信したり、ドキュメントに関するフィードバックを送信できます。また、エラー レポートや機能の使用状況のデータを分析できるように、[!INCLUDE[msCoName](../includes/msconame-md.md)] に自動的に送信することもできます。 このトピックでは、次の 3 つのフィードバック オプションについて説明します。  
  
## <a name="submitting-feedback-about-the-product"></a>製品に関するフィードバックの送信  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の機能に関するご意見や不具合の報告を送信するには、[!INCLUDE[msCoName](../includes/msconame-md.md)] Connect の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] フィードバック ページを使用します。 対象になるのは、ツールやユーティリティ、言語、プログラミング インターフェイスなどの機能です。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connect の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] フィードバック ページにアクセスするには、さまざまな方法があります。  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] Connect の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] フィードバックの [Web ページ](https://go.microsoft.com/fwlink/?linkid=34178)にアクセスします。  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] で、[ヘルプ] ツール バーの **[フィードバックの送信]** ボタンをクリックするか、 **[コミュニティ]** メニューの [フィードバックの送信] をクリックします。  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] で、[ヘルプ] ツール バーの **[フィードバックの送信]** ボタンをクリックします。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] オンライン ブックの任意のトピックの最上部にある **[フィードバックの送信]** ボタンをクリックします。  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] または [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] に [ヘルプ] ツール バーが表示されていない場合は、次の方法で表示してください。  
  
-   ユーティリティからヘルプにアクセスします。  
  
-   選択、**ヘルプ**チェック ボックスをオン、**ツールバー**のタブ、**ツール/カスタマイズしています.** コマンド。  
  
## <a name="automatic-error-and-usage-reporting"></a>エラーと使用状況レポートの自動送信  
 エラー報告や [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ソフトウェアと各種サービスの使用データを自動的に送信するための機能を有効にできます。 [!INCLUDE[msCoName](../includes/msconame-md.md)] では、この情報を [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の改善に役立てます。 すべての情報を機密情報として扱います。  
  
### <a name="managing-automatic-usage-reporting"></a>使用状況レポートの自動送信機能の管理  
 使用状況レポートの自動送信機能を使用すると、データを収集して [!INCLUDE[msCoName](../includes/msconame-md.md)] に送信するかどうかを決定できます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、使用状況データの送信に 2 つのパイプラインを使用します。 どちらのパイプラインも類似のデータを送信しますが、送信するデータの対象プログラムが異なっており、別々にオン/オフの設定ができるようになっています。 プログラムのいずれかを使用してそのパイプラインのオン/オフを切り替えると、そのパイプラインを共有する他のプログラムに関するデータの収集もそれに応じて停止または開始されます。  
  
-   パイプラインの 1 つは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 全体の使用状況データを送信するときに使用されます。ただし、[!INCLUDE[msCoName](../includes/msconame-md.md)] の各種ツールの中で、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Visual Studio ベースのユーザー インターフェイス要素およびオンライン ブックの構成要素は対象外となります。 セットアップ後にこのパイプラインをオフにする (またはオンにする) こともできます。 この操作を行うには、[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] で [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ベースのプロジェクトを開き、 **[ヘルプ]** メニューの **[カスタマー フィードバックのオプション]** をクリックします。 このコマンドは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ベースのプロジェクトを開くまでは表示されません。  
  
-   もう 1 つのパイプラインは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] オンライン ブック、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 各種ツール内の Visual Studio ベースのユーザー インターフェイス要素、および Visual Studio に使用されます。 セットアップ後にこのパイプラインをオフにする (またはオンにする) こともできます。 この操作を行うには、[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] で [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ベースのプロジェクトを開き、 **[ヘルプ]** メニューの **[カスタマー フィードバックのオプション]** をクリックします。 このコマンドは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ベースのプロジェクトを開くまでは表示されません。  
  
## <a name="helping-build-a-better-books-online"></a>オンライン ブックの改善のための支援  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] オンライン ブックの使用状況レポート機能を有効にすると、チームがさらに優れたドキュメントを開発する際に役立ちます。 弊社が受け取る集計データによって顧客のニーズを把握できます。 ユーザーがトピック間をどのように移動し、特定のトピックをどの程度頻繁に表示し、どのトピックが最も役立ち、どのトピックが最も役に立たないと考えているかがわかります。  
  
 フィードバックによって、ユーザーがどのようにドキュメントを使用しているかを理解できます。 これは、ドキュメント スタッフを最も重要なトピックに割り振り、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の今後のドキュメント構成方法を検討していくうえで役立ちます。 オンライン ブックのこの使用状況情報から、顧客が頻繁にヘルプを参照する機能を特定することもできます。 それによって、操作性を改善する必要がある領域が明らかになります。  
  
  
