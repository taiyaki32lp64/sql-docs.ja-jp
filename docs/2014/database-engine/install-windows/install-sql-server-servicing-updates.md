---
title: SQL Server 2014 サービス更新プログラムのインストール |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 7d6c962b-c8d0-49f7-a2ac-00ad8dca930a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 07f438f86a22b866351a0b83ee7634338f3ad2cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62775345"
---
# <a name="install-sql-server-2014-servicing-updates"></a>SQL Server 2014 サービス更新プログラムのインストール
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]の更新プログラムのインストールについて説明します。 このセクションでは、次の項目について説明します。  
  
-   新規インストール時に [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の更新プログラムをインストールする  
  
-   既にインストールされている [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の更新プログラムをインストールする  
  
 常に最新のセキュリティ更新プログラムがインストールされた状態になるように、適切なタイミングで最新の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新プログラムを評価してインストールすることをお勧めします。  
  
## <a name="installing-updates-for-includesscurrentincludessscurrent-mdmd-during-a-new-installation"></a>新規インストール時に [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の更新プログラムをインストールする  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップでは、メインの製品とそれに適用可能な更新プログラムが同時にインストールされるように、最新の製品の更新プログラムとメインの製品のインストールが統合されています。 製品の更新プログラムでは、次の場所から適用可能な更新プログラムが検索されます。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update  
  
-   Windows Server Update Services (WSUS)  
  
-   ローカル フォルダー  
  
-   ネットワーク共有  
  
 セットアップで最新バージョンの適用可能な更新プログラムが検出されると、ダウンロードが実行されて、現在の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ プロセスと統合されます。 製品の更新プログラムには、累積更新プログラム、サービス パック、またはサービス パックと累積更新プログラムが含まれる場合があります。 製品の更新機能の拡張機能は、[スリップ ストリーム機能](https://go.microsoft.com/fwlink/?LinkId=219945)で使用可能だった[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]PCU1 します。  
  
## <a name="installing-updates-for-includesscurrentincludessscurrent-mdmd-after-it-has-already-been-installed"></a>既にインストールされている [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の更新プログラムをインストールする  
 インストール済みのインスタンスで[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、利用可能なすべての更新を適用することをお勧めします。一般配布リリース (GDR のセキュリティと重要な更新プログラム)、サービス パック (SP) と、最新使用可能な累積的な更新プログラム (CU)。  
  
 SQL Server 更新プログラムは、サービス リリースの種類に応じて、Microsoft Update (MU)、Microsoft ダウンロード センター、またはサーバーのカスタマー サポート サービス修正プログラムを使用して使用できます。 SQL Server のセキュリティと重要な更新プログラムは、(では、Windows Update を通じて MU コントロール パネル にする必要があるこれらの更新プログラムを確認できるように) を Microsoft Update によって自動的に提供されます。 サービス パックは、ダウンロード センターおよびダウンロードが省略可能/重要 MU でご確認いただけます。 CU サポート技術情報の記事で提供される Microsoft の修正プログラムのダウンロード サーバーに累積的更新プログラムを利用できます。  
  
## <a name="see-also"></a>参照  
 [SQL Server 2014 インストール ウィザードからインストール&#40;セットアップ&#41;](install-sql-server-from-the-installation-wizard-setup.md)   
 [コマンド プロンプトから更新プログラムのインストール](installing-updates-from-the-command-prompt.md) [、インスタンスの SQL Server 2014 への機能の追加&#40;セットアップ&#41;](add-features-to-an-instance-of-sql-server-setup.md)   
 [SQL Server 2014 のインストールの削除](repair-a-failed-sql-server-installation.md)  
  
  
