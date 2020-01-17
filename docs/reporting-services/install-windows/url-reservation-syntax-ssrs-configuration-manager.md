---
title: URL 予約の構文 (SSRS 構成マネージャー) | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- URL reservations
ms.assetid: 30e4be2e-e65d-462c-895a-5a0a636d042f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 115035e4ab8711a251ec8d2ac253b9987b5ebe66
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62651669"
---
# <a name="url-reservation-syntax--ssrs-configuration-manager"></a>URL 予約の構文 (SSRS 構成マネージャー)
  このトピックでは、レポート サーバー Web サービスとレポート マネージャーの URL 文字列の各部分について説明します。 内部的に格納される URL 文字列の構造は、ブラウザー ウィンドウのアドレス バーに入力する URL の構造とは異なります。 URL 予約文字列は、URL の構成時の Reporting Services 構成ツールの [結果] ウィンドウおよび RSReportServer.config ファイルに示されます。 URL 文字列の定義方法を理解しておくと、URL 予約の問題のトラブルシューティングや、サーバーで定義されている内部 URL 予約を表示するための HTTP.SYS に対するクエリを実行する場合に役立ちます。  
  
## <a name="url-syntax"></a>URL 構文  
 レポート サーバーの URL は、 **UrlString** 要素と **VirtualDirectory** 要素に格納されます。 **UrlString** と **VirtualDirectory** を個別の要素に分割するのは、URL 文字列は複数定義できますが、仮想ディレクトリ名は [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アプリケーションごとに 1 つしか指定できないためです。  
  
 HTTP.SYS では、URL 予約に **UrlString** と **VirtualDirectory**の両方が含まれます。 URL 予約の構文は、次の各部で構成されます。  
  
 \<scheme>://\<hostname>:\<port>/\<virtualdirectory>  
  
 次の表では、各プロパティについて説明し、各プロパティで有効な値を示します。  
  
|プロパティ|有効な値|[説明]|  
|--------------|------------------|-----------------|  
|scheme|http または https|非 SSL 接続と SSL 接続のプレフィックスです。|  
|hostname|(+) 強いワイルドカード。IP アドレスの **[(すべて割り当て)]** 値に相当します。<br /><br /> (\*) 弱いワイルドカード。 **[(すべて未割り当て)]** の IP アドレスに相当します。<br /><br /> 完全修飾ドメイン名<br /><br /> コンピューター名<br /><br /> IP アドレス (IPv4)<br /><br /> IP アドレス (IPv6)|ネットワーク上のサーバーを識別します。<br /><br /> (+) 強いワイルドカードが既定値です。 HTTP.SYS は、指定されたポートと仮想ディレクトリの組み合わせのすべてのネットワーク アダプターに対するすべての要求を受け入れます。 レポート サーバーは、ポートに対するすべての要求を受け入れます。<br /><br /> (\*) 弱いワイルドカードです。 HTTP.SYS は、指定されたポートと仮想ディレクトリの組み合わせのすべてのネットワーク アダプターに対する要求のうち、他の URL 予約によって処理されないすべての要求を受け入れます。<br /><br /> コンピューター名は、ネットワーク上のコンピューターの NetBIOS 名です。<br /><br /> 完全修飾ドメイン名には、ドメイン コントローラーまたはパブリック ドメイン ネーム サーバーに登録されているドメイン アドレスとサーバー名が含まれます。<br /><br /> IP アドレス (IPv4) は、コンピューターのネットワーク アダプターの *nnn.nnn.nnn.nnn*という IPv4 形式の IP アドレスです。<br /><br /> IP アドレス (IPv6) は、コンピューターのネットワーク アダプターの \<header>:\<header>:*nnn.nnn.nnn.nnn* という IPv6 形式の IP アドレスです。|  
|Port|80<br /><br /> 443<br /><br /> \<custom>|ポート 80 は、サーバーからやり取りされる HTTP 要求の標準ポートです。<br /><br /> ポート 443 は、SSL 接続の標準ポートです。<br /><br /> 別のアプリケーションによって予約されていない任意のポートを使用できます。|  
|VirtualDirectory|ReportServer *[_InstanceName]*<br /><br /> Reports *[_InstanceName]*<br /><br /> \<custom>|アプリケーションの名前を指定します。 この値は文字列です。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の既定では、レポート サーバー Web サービスとレポート マネージャー アプリケーションのアプリケーション名として、ReportServer と Reports が使用されます。 必要に応じて異なる名前を使用できます。<br /><br /> この値は必須です。 この値によってアプリケーションが識別されます。<br /><br /> 仮想ディレクトリは、アプリケーション インスタンスごとに 1 つだけ指定します。 同じインスタンスの同じアプリケーションに対して複数の URL を作成するには、複数のバージョンの **UrlString**を作成します。 複数のアプリケーション インスタンスに対して一意の仮想ディレクトリ名を作成するには、アンダースコア文字 (_) を使用してインスタンス名を追加することによって、インスタンス名を仮想ディレクトリ名に含めることを検討してください。 *InstanceName* は省略可能ですが、1 つのコンピューター上に複数のインスタンスが存在する場合は指定することをお勧めします。 名前付きインスタンスの URL 予約を設定する方法の詳細については、「[レポート サーバーの複数インスタンス配置における URL 予約 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/url-reservations-for-multi-instance-report-server-deployments.md)」を参照してください。<br /><br /> 仮想ディレクトリの値では、大文字と小文字が区別されません。 URL 区切り文字または URL エンコードが含まれていない任意の文字列を使用できます。|  
  
## <a name="see-also"></a>参照  
 [レポート サーバー URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
  
  
