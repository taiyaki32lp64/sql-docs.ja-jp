---
title: SQL Server サービス更新プログラムのインストール | Microsoft Docs
ms.custom: ''
ms.date: 09/05/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 7d6c962b-c8d0-49f7-a2ac-00ad8dca930a
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 7d88350f00b90156cd1e33a4d816ae649cc6910f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990936"
---
# <a name="install-sql-server-servicing-updates"></a>SQL Server サービス更新プログラムのインストール

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

この記事では、[!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] の更新プログラムのインストールについて説明します。 このセクションでは、次の項目について説明します。
  
- 新規インストール時に [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] の更新プログラムをインストールする  
  
- 既にインストールされている [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] の更新プログラムをインストールする  
  
常に最新のセキュリティ更新プログラムがインストールされた状態になるように、適切なタイミングで最新の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新プログラムをインストールします。  
  
## <a name="installing-updates-for-includenoversionincludesssnoversion-mdmd-during-a-new-installation"></a>新規インストール時に [!INCLUDE[noVersion](../../includes/ssNoVersion-md.md)] の更新プログラムをインストールする  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップでは、メインの製品とそれに適用可能な更新プログラムが同時にインストールされるように、最新の製品の更新プログラムとメインの製品のインストールが統合されています。 製品の更新プログラムでは、次の場所から適用可能な更新プログラムが検索されます。  
  
- [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update  
  
- Windows Server Update Services (WSUS)  
  
- ローカル フォルダー  
  
- ネットワーク共有  
  
セットアップで最新バージョンの適用可能な更新プログラムが検出されると、ダウンロードが実行されて、現在の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ プロセスと統合されます。 製品の更新プログラムには、累積更新プログラム、サービス パック、またはサービス パックと累積更新プログラムが含まれる場合があります。  
  
## <a name="installing-updates-for-includessnoversionincludesssnoversion-mdmd-after-it-has-already-been-installed"></a>既にインストールされている [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] の更新プログラムをインストールする  
[!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]のインストール済みインスタンスでは、一般配布リリース (GDR)、サービス パック (SP)、および累積的な更新プログラム (CU) を含む最新のセキュリティ更新プログラムと重要な更新プログラムを適用することをお勧めします。 詳しくは、[2016 年 3 月の SQL Server 増分サービス モデル (ISM) に関するお知らせ](https://blogs.msdn.microsoft.com/sqlreleaseservices/announcing-updates-to-the-sql-server-incremental-servicing-model-ism/)のページをご覧ください。

> [!NOTE]
> [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 以降では、簡略化された予測可能なメインストリーム サービス ライフサイクルおよびサービス パック (SP) は利用できなくなります。 累積的な更新プログラム (CU) と、必要なときの一般配布リリース (GDR) だけです。
> 詳しくは、[2017 年 9 月の SQL Server に対する最新のサービス モデル (ISM) に関するお知らせ](https://blogs.msdn.microsoft.com/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server/)のページをご覧ください。
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の更新プログラムは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update (MU)、Windows Server Update Services (WSUS)、および Microsoft ダウンロード センターを通じて入手できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセキュリティ更新プログラムと重要な更新プログラムは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update から入手できます。また、MU に対してこれらの更新プログラムを選択する必要があるかどうかは、コントロール パネルの Windows Update アプレットで確認できます。  
  
[!INCLUDE[msCoName](../../includes/msconame-md.md)] Update から更新プログラムを受け取ると、すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能が自動モードで最新バージョンに更新されます。 柔軟に対応する必要がある場合またはインターネットや WSUS にアクセスできない場合は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] ダウンロード センターから更新プログラムを入手する必要があります。  
  
## <a name="see-also"></a>参照  
[SQL Server をインストール ウィザードからインストールする &#40;セットアップ&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)        
[SQL Server のインスタンスへの機能の追加 (セットアップ)](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)         
[失敗した SQL Server のインストールの修復](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)  

