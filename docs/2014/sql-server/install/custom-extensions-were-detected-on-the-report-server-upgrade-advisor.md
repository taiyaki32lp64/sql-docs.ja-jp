---
title: レポートサーバーでカスタム拡張機能が検出されました (アップグレードアドバイザー) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- rendering extensions [Reporting Services], custom extensions
- security extensions [Reporting Services]
- custom extensions [Reporting Services]
- data processing extensions [Reporting Services], custom extensions
- delivery extensions [Reporting Services]
ms.assetid: fa184bd7-11d6-4ea3-9249-bc1b13db49e5
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: f985f41104dd194d851760c3d1c3e5479a65b7e8
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952594"
---
# <a name="custom-extensions-were-detected-on-the-report-server-upgrade-advisor"></a>レポート サーバーでカスタム拡張機能が検出された (アップグレード アドバイザー)
  構成ファイル内のカスタム拡張機能の設定がアップグレード アドバイザーによって検出されました。これは、データ処理、配信、表示、セキュリティ、または認証用のカスタム拡張機能が 1 つ以上インストールに含まれていることを示しています。 アップグレードによって、拡張機能の構成設定はアップグレード後のレポート サーバーに移動されます。 ただし、カスタム拡張機能を既存のレポート サーバーのインストール フォルダーにインストールした場合、アップグレードの処理中に、これらのカスタム拡張機能のアセンブリ ファイルは新しいインストール フォルダーに移動されません。 アップグレードの完了後、アセンブリ ファイルを新しい [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インストール フォルダーに移動する必要があります。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モード。|  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>[説明]  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は、データ処理、配信、表示、セキュリティ、および認証用のカスタム拡張機能を開発者が作成するための拡張可能なアーキテクチャを提供します。  
  
 現在インストールされている [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] でカスタム拡張機能またはアセンブリを使用している場合、セットアップを使用してアップグレードを実行できますが、アップグレードの完了後に拡張機能を新しいインストール場所に移動するか、アップグレードの前に手順を実行する必要が生じることがあります。  
  
> [!NOTE]  
>  アイテムの値、スタイル、および書式設定を計算するためにレポートで使用するようにカスタム コード アセンブリが設定されているかどうかは、アップグレード アドバイザーによって検出されません。 詳細については、「[その他の Reporting Services アップグレードに関する問題](../../../2014/sql-server/install/other-reporting-services-upgrade-issues.md)」を参照してください。  
  
 カスタム拡張機能をソフトウェア ベンダーから購入した場合、ベンダーに問い合わせて、そのカスタム機能のアップグレードに関する詳細を確認してください。  
  
## <a name="corrective-action"></a>修正措置  
 次のセクションに従って、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のアップグレードに加えて、またはアップグレードの前に実行する手順を確認してください。  
  
 [カスタムデータ処理または配信拡張機能](#dataprocdeliver)  
  
 [カスタム表示拡張機能](#render)  
  
 [SQL Server 2000 レポートサーバーでのカスタムセキュリティまたは認証の拡張機能](#secauth2000)  
  
 [SQL Server 2005 レポートサーバーでのカスタムセキュリティまたは認証の拡張機能](#secauth2005)  
  
 アップグレードの完了後、拡張機能アセンブリを新しいインストール フォルダーに移動し、カスタム拡張機能が想定どおりに動作することを確認します。 拡張機能が動作しない場合は、再コンパイルが必要なことがあります。  
  
#### <a name="to-recompile-an-extension"></a>拡張機能を再コンパイルするには  
  
1.  Microsoft.ReportingServices.Interfaces.dll ファイルをソース コードが含まれるフォルダーにコピーします。  
  
2.  ソース ファイルが含まれるプロジェクトを開き、Microsoft.ReportingServices.Interfaces.dll ファイルへの参照を追加します。  
  
3.  ソリューションを再構築して拡張機能をバインドします。  
  
 アップグレードを続行しない場合、代わりに [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を移行できます。 カスタム拡張機能の移行手順については、このトピックの「[カスタム拡張機能の移行](#migrcustext)」を参照してください。  
  
###  <a name="dataprocdeliver"></a>カスタムデータ処理または配信拡張機能  
 データ処理または配信のカスタム拡張機能がアップグレード アドバイザーによって検出された場合、アップグレード プロセスはブロックされません。 ただし、アップグレードの完了後、これらの拡張機能によって提供されるカスタム機能を使用する前に、追加の手順を実行する必要が生じることがあります。 たとえば、カスタム拡張機能ファイルが [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インストール フォルダーにインストールされている場合は、追加の手順を実行する必要があります。  
  
##### <a name="post-upgrade-steps-for-custom-data-processing-or-delivery-extensions"></a>データ処理または配信のカスタム拡張機能のアップグレード後に行う手順  
  
1.  1 つまたは複数の拡張機能ファイルを、レポート サーバーの新しいプログラム フォルダーに移動します。 既定では、レポートサーバーのプログラムフォルダーは、SQL Server \ MSRS10_50 にあります。*instance_name*> レポートサーバーを\<します。  
  
 詳細については、SQL Server オンライン ブックの「データ処理拡張機能の配置」および「配信拡張機能の実装」を参照してください。  
  
###  <a name="render"></a>カスタム表示拡張機能  
 カスタム表示拡張機能がアップグレード アドバイザーによって検出された場合、アップグレード プロセスはブロックされます。 アップグレード プロセスを続行するには、カスタム拡張機能の構成エントリを構成ファイルから削除します。 ただし、アップグレードの完了後にカスタム拡張機能を使用できなくなります。 アップグレード後にカスタム表示拡張機能が必要な場合は、更新された表示拡張機能をビルドするか、更新された表示拡張機能をカスタム拡張機能ベンダーから入手する必要があります。  
  
 アップグレードを可能にするための手順を実行する必要があります。または、代わりに [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の移行を選択できます。  
  
> [!IMPORTANT]  
>  更新された表示拡張機能が想定どおりに動作することをテストして確認するまで、レポート サーバーをアップグレードまたは移行しないでください。  
  
##### <a name="to-upgrade-custom-rendering-extensions"></a>カスタム表示拡張機能をアップグレードするには  
  
1.  最新のインターフェイスを備えた表示拡張機能を入手します。  
  
2.  RSReportServer.config から 1 つまたは複数の古いカスタム表示拡張機能エントリを削除します。  
  
3.  レポート サーバーをアップグレードします。  
  
4.  アップグレードが完了したら、更新された拡張機能をレポート サーバーにインストールします。  
  
 詳細については、SQL Server オンライン ブックの「表示拡張機能の実装」を参照してください。  
  
###  <a name="secauth2000"></a>SQL Server 2000 レポートサーバーでのカスタムセキュリティまたは認証の拡張機能  
 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] レポート サーバーのセキュリティまたは認証のカスタム拡張機能がアップグレード アドバイザーによって検出された場合、アップグレード プロセスはブロックされます。 アップグレードを可能にするための手順を実行する必要があります。または、代わりに [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の移行を選択できます。 いずれの場合も、Microsoft.ReportingServices.Interfaces.dll の最新のインターフェイスを使用して、拡張機能を更新および再コンパイルする必要があります。これは、[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] と [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ではインターフェイスが異なるためです。  
  
> [!IMPORTANT]  
>  更新されたセキュリティまたは認証の拡張機能が想定どおりに動作することをテストして確認するまで、レポート サーバーをアップグレードまたは移行しないでください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 用に作成したカスタム認証拡張機能を使用する場合は、モデル ドリブン レポート用に導入された新しいクラスとメンバーをサポートするようにソース コードを変更する必要があります。  
  
##### <a name="to-upgrade-custom-security-or-authentication-extensions-from-a-sql-server-2000-report-server"></a>SQL Server 2000 レポートサーバーからカスタムセキュリティまたは認証の拡張機能をアップグレードするには  
  
1.  最新のインターフェイスを使用して、すべてのセキュリティまたは認証の拡張機能を更新および再コンパイルします。  
  
2.  RSReportServer.config から 1 つまたは複数のセキュリティまたは認証の拡張機能エントリを削除します。  
  
3.  レポート サーバーをアップグレードします。  
  
4.  アップグレードが完了したら、更新された拡張機能をレポート サーバーにインストールします。  
  
 詳細については、SQL Server オンライン ブックの「セキュリティ拡張機能の実装」を参照してください。  
  
###  <a name="secauth2005"></a>SQL Server 2005 レポートサーバーでのカスタムセキュリティまたは認証の拡張機能  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] レポート サーバーのセキュリティまたは認証のカスタム拡張機能がアップグレード アドバイザーによって検出された場合、アップグレード プロセスはブロックされます。 アップグレードを可能にするための手順を実行する必要があります。または、代わりに [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の移行を選択できます。  
  
##### <a name="to-upgrade-custom-security-or-authentication-extensions-from-a-sql-server-2005-report-server"></a>SQL Server 2005 レポート サーバーのセキュリティまたは認証のカスタム拡張機能をアップグレードするには  
  
1.  RSReportServer.config からセキュリティまたは認証の拡張機能の構成エントリを削除します。  
  
2.  レポート サーバーをアップグレードします。  
  
3.  アップグレードの完了後、構成エントリを再び RSReportServer.config に追加します。  
  
4.  拡張機能アセンブリが古い [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インストール フォルダーにインストールされている場合、これを新しいインストール フォルダーに移動します。  
  
 詳細については、SQL Server オンライン ブックの「セキュリティ拡張機能の実装」を参照してください。  
  
###  <a name="migrcustext"></a>カスタム拡張機能の移行  
 アップグレードを実行する代わりに [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を移行する場合は、カスタム拡張機能を新しい [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インスタンスに移行する手順に従います。  
  
##### <a name="to-migrate-custom-extensions-to-a-new-reporting-services-instance"></a>カスタム拡張機能を新しい Reporting Services インスタンスに移行するには  
  
1.  最新の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インターフェイスを使用して更新された拡張機能をビルドまたは入手します。  
  
2.  レポート サーバーを新しいインスタンスに移行します。  
  
3.  新しいインスタンスで拡張機能を構成します。  
  
## <a name="see-also"></a>参照  
 [アップグレードに関する&#40;問題の Reporting Services アップグレードアドバイザー&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
