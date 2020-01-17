---
title: 高度な複数 Web サイト構成 (SSRS ネイティブモード) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.advancedmultiplewebsiteconfig.F1
ms.assetid: af4ede43-2225-45b5-ae7e-9202411551ba
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: b331015abd90fbff4c3810118666dbc9b356369b
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952670"
---
# <a name="advanced-multiple-web-site-configuration-ssrs-native-mode"></a>高度な複数 Web サイト構成 (SSRS ネイティブ モード)
  このダイアログ ボックスは、レポート サーバーまたはレポート マネージャーへのアクセスに使用される URL を作成し、管理するために使用します。 **[高度な複数 Web サイト構成]** ダイアログ ボックスでは、追加の URL、つまりホスト ヘッダー名を含んだカスタム URL を作成することも、IPv4 または IPv6 形式の IP アドレスを指定することもできます。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード。  
  
 レポート サーバーに複数の方法でアクセスできるように構成する場合は、複数の URL を作成すると便利です。 たとえば、イントラネットおよびエクストラネット接続を介してレポート サーバーにアクセスするには、接続の種類ごとに異なる URL を用意する必要があります。  
  
 **[高度な複数 Web サイト構成]** ダイアログ ボックスを開くには、 **構成マネージャーの** [Web サービス URL] **ページまたは** [レポート マネージャー URL] **ページで** [詳細設定] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をクリックします。 **[高度な複数 Web サイト構成]** ダイアログ ボックスが開いたら、 **[追加]** または **[編集]** をクリックして、新しい URL の定義、既存の URL の変更や削除ができます。  
  
 **[OK]** をクリックして変更を保存します。 URL を追加または削除した後に、 **[OK]** をクリックせずにダイアログ ボックスを閉じると、変更は失われます。  
  
## <a name="options"></a>および  
 **[IP アドレス]**  
 TCP/IP ネットワーク上でレポート サーバー コンピューターを識別します。 有効な値は次のとおりです。  
  
-   **[すべて割り当て]** は、レポート サーバー アプリケーションを指す URL に、コンピューターに割り当てられている IP アドレスをどれでも使用できることを示します。 コンピューターに割り当てられている IP アドレスに対してドメイン ネーム サーバーによって解決されるわかりやすいホスト名 (コンピューター名など) も、この値の対象に含まれます。 これは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL の既定値です。  
  
-   **[すべて未割り当て]** は、IP アドレスまたはホスト名が正確に一致しない要求をレポート サーバーがすべて受け入れることを示します。 別の Web アプリケーションが既に使用している場合は、この値を使用しないでください。 使用すると、他のアプリケーションのサービスが中断されます。  
  
-   **[127.0.0.1]** は、localhost にアクセスする場合に使用します。 この値は、レポート サーバー コンピューターでのローカル管理をサポートします。 この値のみを選択すると、レポート サーバー コンピューターにローカルにログオンしているユーザーだけがアプリケーションにアクセスできるようになります。  
  
-   "*nnn.nnn.nnn.nnn* " は、コンピューターのネットワーク アダプター カードの IPv4 アドレスです。 ネットワークで IPv6 アドレス指定が使用されている場合、IP アドレスは \<ヘッダー >:*nnnn: nnnn: nnnn: nnnn*の形式と同様の 8 4 バイトのフィールドの128ビット値になります。  
  
     複数のカードがある場合は、それぞれに IP アドレスが割り当てられます。 この値のみを選択すると、アプリケーション アクセスがその IP アドレス (およびドメイン ネーム サーバーによってそのアドレスにマップされるホスト名) に限定されます。 localhost を使用してレポート サーバーにアクセスすることはできません。また、レポート サーバー コンピューターにインストールされている他のネットワーク アダプター カードの IP アドレスは使用できません。  
  
 **[ポート]**  
 レポート サーバーが要求を監視するポートを指定します。 既定のポートは、ポート 80 です。 ポート 80 を使用する場合は、URL にポートを含める必要はありません。 他のポート番号を使用する場合は、URL に必ず含める必要があります (http://localhost:8181/reports)など)。  
  
 **ホスト ヘッダー**  
 コンピューターに解決されるホスト ヘッダーをドメイン ネーム サーバーに既に定義している場合は、レポート サーバー アクセス用に構成する URL にそのホスト ヘッダーを指定できます。  
  
 ホスト ヘッダーは一意の名前であり、これを使用して複数の Web サイトで単一の IP アドレスとポートを共有できます。 ホスト ヘッダー名は、IP アドレスとポート番号に比べて容易に記憶でき、入力も簡単です。 たとえば、www.adventure-works.com などはホスト ヘッダー名の一例です。  
  
 **[SSL ポート]**  
 SSL 接続のポートを指定します。 SSL の既定のポートは 443 です。  
  
 **[SSL 証明書]**  
 対象のコンピューターにインストールした SSL 証明書の名前を指定します。 証明書がワイルドカードにマップされている場合は、それをレポート サーバーの接続に使用できます。  
  
 証明書が登録されている完全修飾コンピューター名を指定します。 証明書が登録されている名前と同じ名前を指定する必要があります。  
  
 このオプションを使用するには、証明書がインストールされている必要があります。 また、RSReportServer.config ファイルの UrlRoot 構成設定を、証明書で登録されたコンピューターの完全修飾名を指すように変更する必要があります。 詳細については、 [オンライン ブックの「](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) ネイティブ モードのレポート サーバーでの SSL 接続の構成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 」を参照してください。  
  
 **発行先**  
 証明書が作成されたコンピューターの名前を示します。  
  
 **[追加]**  
 追加の URL を定義します。  
  
 **[編集]**  
 URL 構文の一部を変更します。  
  
 **[削除]**  
 一覧から URL エントリを削除します。  
  
## <a name="see-also"></a>参照  
 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [レポート サーバー URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
