---
title: 別のコンピューターへの接続 (SQL Server 構成マネージャー) | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], other computers
ms.assetid: c4c1e94f-4f5f-431e-8b5b-d5ff97baf723
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 03f409e11e037fcc406940d5a97e9934a77b96b4
ms.sourcegitcommit: c98c6e33d04d4a1888db7dbe89cb0b1bb3a66418
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2019
ms.locfileid: "74249765"
---
# <a name="scm-services---connect-to-another-computer"></a>SCM サービス - 別のコンピューターに接続する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で別のコンピューターに接続する方法について説明します。 Windows の [コンピューターの管理] の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console (MMC) を開くための最初の手順に従って、コンピューターに接続し、[サービスとアプリケーション] ツリーを展開します。 2 番目の手順に従って、リモート コンピューター上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーへのリンクを含むファイルを作成します。

> [!NOTE]
> リモートで接続している場合、一部の操作は構成マネージャーで実行することができません。

別のコンピューターのサービスを開始、停止、一時停止、または再開するには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用してサーバーに接続し、サーバーまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを右クリックし、次に目的の操作をクリックします。

## <a name="SSMSProcedure"></a>

### <a name="to-connect-to-another-computer-with-windows-computer-management"></a>Windows のコンピューターの管理を使用して別のコンピューターに接続するには

1. **[スタート]** メニュー ボタンを右クリックし、 **[コンピューターの管理 (ローカル)]** をクリックします。
2. **[操作]** メニューの **[別のコンピューターへ接続]** をクリックします。
3. **[コンピューターの選択]** ダイアログ ボックスの **[別のコンピューター]** ボックスに管理するコンピューターの名前を入力し、 **[OK]** をクリックします。

   リモート コンピューターで実行されているサービスが、[コンピューターの管理] に表示されます。 最上位ノードが **[コンピューターの管理 \<*リモート コンピューター*>]** に変更されます。

4. コンソール ツリーの **[サービスとアプリケーション]** を展開し、 **[SQL Server 構成マネージャー]** を展開して、リモート コンピューターのサービスを管理します。

### <a name="to-save-a-link-to-sql-server-configuration-manager-for-another-computer"></a>別のコンピューターの SQL Server 構成マネージャーへのリンクを保存するには

1. **[スタート]** メニューの **[ファイル名を指定して実行]** をクリックします。

2. **[名前]** ボックスに「**mmc -a**」と入力 (64 ビット コンピューター上では「**mmc /32 -a**」と入力) して、[!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理コンソールを作成者モードで開きます。
3. **[ファイル]** メニューの **[スナップインの追加と削除]** をクリックします。
4. **[スナップインの追加と削除]** ウィンドウで **[追加]** をクリックします。
5. **[スタンドアロン スナップインの追加]** ウィンドウで **[コンピューターの管理]** をクリックし、次に **[追加]** をクリックします。
6. **[コンピューターの管理]** ウィンドウの **[別のコンピューター]** をクリックし、管理するリモート コンピューターの名前を入力して **[完了]** をクリックします。
7. **[スタンドアロン スナップインの追加]** ウィンドウで **[閉じる]** をクリックします。
8. **[スナップインの追加と削除]** ウィンドウで **[OK]** をクリックします。
9. **[コンピューターの管理 (** _\<コンピューター名>_ **)]** 、 **[サービスとアプリケーション]** の順に展開します。
10. **[SQL Server 構成マネージャー]** を右クリックして、 **[ここから新しいウィンドウ]** をクリックします。
11. **[ウィンドウ]** メニューの **[コンソール ルート]** をクリックし、最初のウィンドウに切り替えてからそのウィンドウを削除します。
12. **[ファイル]** メニューの **[名前を付けて保存]** をクリックし、ファイルにファイル拡張子 **.msc** を含む適切なファイル名を付けて目的のフォルダーに保存します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理コンソールを閉じます。
13. ターゲット コンピューターの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを開くには、そのファイルをダブルクリックします。 必要な場合は、デスクトップまたは **[スタート]** メニューにファイルへのリンクを保存します。

> [!CAUTION]
> リモート コンピューターの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用する場合、コンピューター名が明らかではないため、誤って別のコンピューターを停止または構成してしまう可能性があります。 サービスを変更する前に、 **[サービス]** タブの **[ホスト名]** ボックスを調べてコンピューター名を確認してください。

## <a name="see-also"></a>参照

- [SQL Server ツールでサーバーの状態を表示できるようにする WMI の構成](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)
