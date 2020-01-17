---
title: 構成のチェックリスト
description: 独自の環境で分析プラットフォームシステムを構成するために必要なタスクのチェックリストを提供します。 アプライアンスを使用するには、これらの構成タスクが必要です。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 80fc899400be167badaae9d617d43a61e0d346b5
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401460"
---
# <a name="appliance-configuration-checklists-for-analytics-platform-system"></a>Analytics Platform System のアプライアンス構成チェックリスト
独自の環境で分析プラットフォームシステムを構成するために必要なタスクのチェックリストを提供します。 アプライアンスを使用するには、これらの構成タスクが必要です。  
  
> [!WARNING]  
> ツールで使用可能なタスクを実行するには、Analytics Platform System**Configuration Manager**を使用することをお勧めします。また、サポートされている唯一の方法です。  
  
## <a name="BeforeTasks"></a>開始する前に  
  
### <a name="prerequisites"></a>前提条件  
  
1.  アプライアンスは、データセンターにインストールされ、電源がオンになっている必要があります。  
  
2.  次の情報があることを確認してください。これは、IHV によって提供されています。  
  
    -   PDW コントロールノードの外部 IP アドレス (*PDW_region*CTL01)  
  
    -   アプライアンスドメイン名  
  
    -   アプライアンスドメイン管理者のユーザー名とパスワード  
  
3.  信頼された証明書を取得します。 これは、クライアントがセキュリティで保護された接続を使用して**管理コンソール**に接続できるようにするために、後の手順でインポートします。 パスワードで保護された PFX ファイルのコントロールノードに証明書を保存します。  
  
4.  次の手順に従って、 **Configuration Manager**を起動します。  
  
    1.  **リモートデスクトップ**を使用して、PDW コントロールノード (*PDW_region*CTL01) に接続します。 (CTL01 の外部 IP アドレスを使用して接続する必要がある場合があります)。  
  
    2.  PDW コントロールノードの [**スタート**] メニューから**Configuration Manager**を起動します。 Configuration Manager の最初の画面には、IHV によって作成されたアプライアンストポロジが表示されます。 アプライアンスの一部として SQL Server PDW ソフトウェアによって認識されるハードウェアノードの一覧です。 アプライアンスのトポロジ画面で設定を変更する必要はありません。  
  
## <a name="CMTasks"></a>Configuration Manager タスクを実行する  
SQL Server PDW**Configuration Manager** (pdwcm) はアプライアンス管理 SQL Server PDW ツールで、システム管理者はアプライアンスレベルの操作を実行したり、アプライアンスレベルの設定を変更したりするために使用します。 たとえば、PDWCM を使用してパスワードをリセットし、タイムゾーンを設定し、IP アドレスを変更し、SSL 証明書を構成し、ファイアウォール経由でリモートアクセスを有効にする、アプライアンスを開始または停止する、ファイルの瞬時初期化を設定するなどの方法があります。  
  
**Configuration Manager**を使用して、次の構成タスクを実行します。  
  
|構成タスク|説明|  
|----------------------|---------------|  
|物理コンポーネント名について理解を深める|[PDW およびアプライアンスファブリック物理コンポーネント &#40;Analytics Platform System&#41;](pdw-and-appliance-fabric-physical-components.md)|  
|SQL Server PDW の起動 Configuration Manager|[Configuration Manager &#40;Analytics Platform System&#41;を起動します。](launch-the-configuration-manager.md)|  
|ドメイン管理者のパスワードを変更する|アプライアンスには、アプライアンス内のノードを認証するために使用されるプライベート Windows Active Directory Domain Services があります。<br /><br />IHV は、既定のドメイン管理者パスワードを使用してアプライアンスを設定します。 これは、セキュリティで保護されたパスワードに変更する必要があります。<br /><br />**Configuration Manager**は、ドメイン管理者のパスワードを変更する唯一の方法です。<br /><br />詳細については、「[パスワードのリセット &#40;Analytics Platform System&#41;](password-reset.md)」を参照してください。|  
|**Sa**ログオンのパスワードを変更する|SQL Server PDW には、 **sa**というシステム管理者のログオンがあります。 **Sa**ログオンには、すべての特権があります。 権限の許可、拒否、または取り消しを行うことができます。 すべてのシステムビューを表示することもできます。<br /><br />詳細については、「[パスワードのリセット &#40;Analytics Platform System&#41;](password-reset.md)」を参照してください。|  
|アプライアンスのタイムゾーンを設定する|すべてのアプライアンスノードに時間 (ローカルまたはその他の必要な時間) を設定します。<br /><br />詳細については、「[アプライアンスのタイムゾーンの構成 &#40;Analytics Platform System&#41;](appliance-time-zone-configuration.md)」を参照してください。|  
|SQL Server PDW アプライアンスの外部接続ネットワーク設定を指定する|[アプライアンスネットワーク構成 &#40;Analytics Platform System&#41;](appliance-network-configuration.md)|  
|管理コンソールのセキュリティ証明書をインポートする|証明書は、[管理コンソール &#40;Analytics Platform System&#41;を使用](monitor-the-appliance-by-using-the-admin-console.md)して、HTTPS 経由で SECURE SOCKETS LAYER (SSL) 接続をアプライアンスを監視することができます。 既定では、**管理コンソール**には、サーバー認証ではなく、プライバシーを提供する自己署名証明書が含まれています。 この証明書は、Internet Explorer で、ユーザーが接続するときに "この web サイトのセキュリティ証明書に問題があります" というエラーを返します。 この接続ではクライアントとサーバーの間のデータが暗号化されますが、接続は攻撃者からの危険にさらされます。<br /><br />SQL Server PDW 管理者は、セキュリティで保護された接続を確立し、Internet Explorer が報告するエラーを削除するために、クライアントによって認識される信頼された証明機関にチェーンする証明書をすぐに取得する必要があります。 これには、管理コンソールにアクセスするために、コントロールノードの仮想 IP アドレス (推奨) またはユーザーがブラウザーのアドレスバーに入力した値と一致する証明書名をマップする完全修飾ドメイン名が必要です。<br /><br />**Configuration Manager**を使用して、信頼された証明書を追加または削除します。 Microsoft Windows HTTP サービス証明書構成ツール (`winHttpCertCfg.exe`) を直接使用して証明書を管理することはサポートされていません。<br /><br />詳細については、「 [PDW 証明書のプロビジョニング &#40;Analytics Platform System&#41;](pdw-certificate-provisioning.md)」を参照してください。|
|機能スイッチ|Analytics Platform System AU7 で導入された機能スイッチに関する情報を表示します。 このページを使用して、Analytics Platform System の機能と設定を更新または有効/無効にします。 機能スイッチの値を変更するには、サービスを再起動する必要があります。<br /><br />詳細については、「 [PDW 機能スイッチ &#40;Analytics Platform System&#41;](appliance-feature-switch.md)」を参照してください。|
|SQL Server PDW アプライアンスの特定のポートへのアクセスを許可または禁止する Windows ファイアウォール規則を有効または無効にします。|IHV は、アプライアンスを正常に動作させるために必要なファイアウォールルールを構成し、有効にします。 ほとんどの場合、ファイアウォール規則を有効または無効にすることはできません。<br /><br />詳細については、「 [PDW Firewall Configuration &#40;Analytics Platform System&#41;](pdw-firewall-configuration.md)」を参照してください。|  
|SQL Server PDW アプライアンスを開始および停止する|SQL Server PDW アプライアンスを停止または開始します。 詳細については、「 [PDW サービスの状態 &#40;Analytics Platform System&#41;](pdw-services-status.md)」を参照してください。|  
|[**特権**] ダイアログボックスを使用してファイルの瞬時初期化オプションを確認する|ファイルの瞬時初期化は、データファイル操作をより迅速に実行できるようにする SQL Server の機能です。 ネットワークサービスアカウントに SE_MANAGE_VOLUME_NAME 特権が付与されている場合にのみ、SQL Server PDW で有効になります。 既定ではオフになっています。<br /><br />詳細については、「[ファイルの瞬時初期化構成 &#40;Analytics Platform System&#41;](instant-file-initialization-configuration.md)」を参照してください。|  
|バックアップから master データベースを復元する|現在の**master**データベースを削除し、バックアップで置き換えます。 詳細については、「 [Restore The Master Database &#40;Analytics Platform System&#41;](restore-the-master-database.md)」を参照してください。|  
  
## <a name="AddTasks"></a>追加の構成タスクを実行する  
**Configuration Manager**タスクを実行した後、次の追加の構成タスクを実行します。 これらのタスクの一部は省略可能です。  
  
|構成タスク|説明|  
|----------------------|---------------|  
|サードパーティ製のウイルス対策ソフトウェアは、外部に接続されているノードの SQL Server PDW アプライアンスにインストールして構成できます。<br /><br />(省略可能)|詳細については、「[ウイルス対策ソフトウェア &#40;Analytics Platform System&#41;](antivirus-software.md)」を参照してください。|  
|DSRM のパスワードは変更できます。<br /><br />(省略可能)|詳細については、「[ディレクトリサービス復元モードで AD ノードにログオンするための管理者パスワードを設定する」を参照してください &#40;DSRM&#41; &#40;Analytics Platform System&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)です。|  
|ソフトウェア更新プログラムを受信するようにアプライアンスを構成する<br /><br />(推奨)|アプライアンスは、SQL Server PDW および基になるソフトウェアの更新プログラムを受信するように構成する必要があります。<br /><br />詳細については、「 [Configure Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)」を参照してください。 WSUS の詳細については、「[ソフトウェアサービスの &#40;Analytics Platform System&#41;](software-servicing.md)」を参照してください。|  
|Hadoop や Azure blob storage などの外部データへの接続を構成します。<br /><br />(省略可能)|詳細については、「 [Configure PolyBase Connectivity To External Data &#40;Analytics Platform System&#41;](configure-polybase-connectivity-to-external-data.md)」を参照してください。|  
|ウイルス対策ソフトウェアの構成<br /><br />(省略可能)|サードパーティ製のウイルス対策ソリューションは、外部に接続されているノードを保護するために使用できますが、必須ではありません。 「」のガイドラインに従ってください。|  
|バックアップサーバーと読み込みサーバーで InfiniBand ネットワークアダプターを構成する<br /><br />(省略可能)|InfiniBand ネットワークを使用して SQL Server PDW に接続するようにバックアップサーバーと読み込みサーバーを構成するには、現在アクティブな InfiniBand ネットワークへの InfiniBand 接続をアプライアンスの DNS が解決できるようにネットワークアダプターを構成する必要があります。|  
|テレメトリデータを Microsoft に送信するようにを構成する<br /><br />(省略可能)|テレメトリデータを Microsoft に送信するように分析プラットフォームシステムを構成するには、PowerShell スクリプトをコントロールノードで実行する必要があります。 具体的な手順については、「 [Microsoft &#40;SQL Server PDW&#41;にテレメトリのフィードバックを送信する」を](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)参照してください。|  
  
## <a name="see-also"></a>参照  
[ウイルス対策ソフトウェア &#40;Analytics Platform System&#41;](antivirus-software.md)  
[InfiniBand ネットワークアダプター &#40;SQL Server PDW&#41;を構成する](configure-infiniband-network-adapters.md)  
  
