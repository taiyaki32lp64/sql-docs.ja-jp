---
title: 操作方法:アップグレード アドバイザーのインストール |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, installing
- Upgrade Advisor [SQL Server], installing
ms.assetid: 481b0704-ce79-4543-b141-67306128aa2b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0de86b9690f0647803938218ce566508662da20e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094918"
---
# <a name="how-to-install-upgrade-advisor"></a>操作方法:アップグレード アドバイザーをインストールする
  アップグレード アドバイザーでは、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 以外のサポートされているすべてのコンポーネントをリモートで分析できます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインスタンスをスキャンしない場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続できる任意のコンピューターにアップグレード アドバイザーをインストールできます。 コンピューターはアップグレード アドバイザーの前提条件を満たしている必要もあります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインスタンスをスキャンする場合は、アップグレード アドバイザーをレポート サーバーにインストールする必要があります。  
  
 詳細については、次を参照してください。[アップグレード アドバイザーのインストール](../../../2014/sql-server/install/installing-upgrade-advisor.md)します。  
  
### <a name="to-install-upgrade-advisor"></a>アップグレード アドバイザーをインストールするには  
  
1.  次の方法のいずれかを使用してインストールを開始します。  
  
    -   インストールする場合、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Web サイトをクリックして、**ダウンロード**リンクをクリックし、**実行**インストールを開始するボタンをクリックします。  
  
    -   製品メディアからインストールする場合は、開く、 **redist**フォルダーを開き、**アップグレード アドバイザー**フォルダー、およびダブルクリック**SQLUA.msi**します。  
  
    > [!NOTE]  
    >  アップグレード アドバイザーを使用するには、[!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 4 が必要です。 インストールされていない場合やバージョンが古い場合は、エラー メッセージが表示されます。 古いバージョンの [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] をアンインストールしてから、最新バージョンの .NET Framework 4 をインストールします。  
    >   
    >  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom をインストールするための前提条件は、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]アップグレード アドバイザーでは、アップグレード アドバイザー セットアップではインストールされません。 セットアップでは、ダウンロードしてインストールする必要があります、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]から ScriptDom、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Feature Pack。  
  
2.  **へようこそ、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]アップグレード アドバイザー セットアップ**] ページで [**次**。  
  
3.  **使用許諾契約書** ページで、使用許諾契約書を読み取る。 同意する場合は、選択**使用許諾契約書に同意**順にクリックします**次**します。  
  
4.  **登録情報** ページで、名前と会社名を入力します。  
  
5.  **機能の選択**ページで、確認、**インストール パス**値。 必要に応じて、使用して、**参照**場所を変更するボタンをクリックします。 **[次へ]** をクリックします。  
  
6.  **プログラムをインストールする準備が**] ページで [**インストール**アップグレード アドバイザーをインストールします。  
  
7.  **[完了]** をクリックして、ウィザードを終了します。  
  
## <a name="see-also"></a>参照  
 [アップグレード アドバイザーの前提条件](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)  
  
  
