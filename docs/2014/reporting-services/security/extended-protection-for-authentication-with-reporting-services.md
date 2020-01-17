---
title: Reporting Services での認証の拡張保護 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: eb5c6f4a-3ed5-430b-a712-d5ed4b6b9b2b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c1ce348edd9b4d4b6260a0eea56fe28656b03985
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101946"
---
# <a name="extended-protection-for-authentication-with-reporting-services"></a>Reporting Services での認証の拡張保護
  拡張保護は、最新バージョンの [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows オペレーティング システムに追加された一連の拡張機能です。 拡張保護により、アプリケーションで資格情報と認証を保護する方法の幅が広がります。 この機能自体は、資格情報の転送をはじめとする特定の攻撃を直接防ぐものではありませんが、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] などのアプリケーションに対し、認証の拡張保護を適用するためのインフラストラクチャを提供します。  
  
 拡張保護に含まれる認証の拡張機能を代表するのが、サービス バインドとチャネル バインドです。 チャネル バインドでは、チャネル バインド トークン (CBT) を使用して、2 つのエンド ポイント間に確立されたチャネルに問題が生じていないかどうかを確認します。 サービス バインドでは、サービス プリンシパル名 (SPN) を使用して認証トークンの目的の送信先を検証します。 拡張保護の詳細な背景情報については、「 [拡張保護付き統合 Windows 認証](https://go.microsoft.com/fwlink/?LinkId=179922)」を参照してください。  
  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] でサポートおよび適用されるのは、オペレーティング システムで有効化し、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. 既定では、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] はネゴシエート認証または NTLM 認証を指定する要求を受け入れるため、オペレーティング システムでの拡張保護のサポートと [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の拡張保護機能を活用できます。  
  
> [!IMPORTANT]  
>  既定では、Windows の拡張保護は有効になっていません。 Windows で拡張保護を有効にする方法の詳細については、「 [認証に対する保護の強化](https://go.microsoft.com/fwlink/?LinkID=178431)」を参照してください。 認証を成功させるためには、オペレーティング システムとクライアントの認証スタックが両方とも拡張保護をサポートしている必要があります。 旧バージョンのオペレーティング システムを使用している場合は、拡張保護に対応したコンピューターを準備するために、1 つ以上の更新プログラムのインストールが必要になることがあります。 拡張保護の最新情報については、 [こちら](https://go.microsoft.com/fwlink/?LinkId=183362)を参照してください。  
  
## <a name="reporting-services-extended-protection-overview"></a>Reporting Services の拡張保護の概要  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] では、オペレーティング システムで有効になっている拡張保護がサポートされ、適用されます。 オペレーティング システムが拡張保護をサポートしていないか、拡張保護機能がオペレーティング システムで有効化されていない場合、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の拡張保護機能を使用した認証は失敗します。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の拡張保護では、SSL 証明書も必要になります。 詳細については、「 [ネイティブ モードのレポート サーバーでの SSL 接続の構成](configure-ssl-connections-on-a-native-mode-report-server.md)」を参照してください。  
  
> [!IMPORTANT]
>  既定では、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の拡張保護は有効になっていません。 この機能を有効にするには、`rsreportserver.config` 構成ファイルを変更するか、WMI API を使用して構成ファイルを更新します。 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 拡張保護の設定を変更または表示するユーザー インターフェイスは提供されません。 詳細については、このトピックの [構成設定に関するセクション](#ConfigurationSettings) を参照してください。  
  
 拡張保護の設定に加えた変更や設定の不適切な構成が原因で一般的な問題が発生しても、目に見えるエラー メッセージやダイアログ ウィンドウで示されることはありません。 拡張保護の構成や互換性に関係する問題が生じると、認証に失敗し、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のトレース ログにエラーが記録されます。  
  
> [!IMPORTANT]
>  一部のデータ アクセス テクノロジでは、拡張保護がサポートされないことがあります。 データ アクセス テクノロジは、SQL Server データ ソースおよび [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] カタログ データベースへの接続に使用されます。 データ アクセス テクノロジで拡張保護がサポートされない場合、 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] に次のような影響が生じます。  
> 
>  -   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] カタログ データベースを実行する SQL Server は拡張保護を有効にできません。つまり、レポート サーバーがカタログ データベースへの接続に失敗し、認証エラーが返されます。  
> -   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] レポート データ ソースとして使用される SQL Server は拡張保護を有効にできません。つまり、レポート サーバーがレポート データ ソースへの接続に失敗し、認証エラーが返されます。  
> 
>  データ アクセス テクノロジのドキュメントには、拡張保護のサポートに関する情報が記載されています。  
  
### <a name="upgrade"></a>アップグレード  
  
-   アップグレードを[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]サーバーを[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]に既定値で構成設定を追加、`rsreportserver.config`ファイル。 存在する場合は、既に設定していた場合、[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]インストールはそれらを保持、`rsreportserver.config`ファイル。  
  
-   構成設定が追加されたとき、`rsreportserver.config`の構成ファイルで、既定の動作は、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]拡張保護機能はオフと、このトピックの説明に従って、機能を有効にする必要があります。 詳細については、このトピックの [構成設定に関するセクション](#ConfigurationSettings) を参照してください。  
  
-   `RSWindowsExtendedProtectionLevel` 設定の既定値は `Off` です。  
  
-   `RSWindowsExtendedProtectionScenario` 設定の既定値は `Proxy` です。  
  
-   [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] アップグレード アドバイザーは、オペレーティング システムまたは [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の現在のインストールで拡張保護のサポートが有効かどうかを確認しません。  
  
### <a name="what-reporting-services-extended-protection-does-not-cover"></a>Reporting Services の拡張保護でサポートされない機能とシナリオ  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の拡張保護機能では、次の機能領域とシナリオがサポートされません。  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のカスタム セキュリティ拡張機能の作成者は、拡張保護のサポートをカスタム セキュリティ拡張機能に追加する必要があります。  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のインストールで使用または追加されるコンポーネントを開発したサード パーティ ベンダーは、そのコンポーネントを更新して拡張保護をサポートする必要があります。 詳細については、サード パーティ ベンダーに問い合わせてください。  
  
## <a name="deployment-scenarios-and-recommendations"></a>配置のシナリオと推奨事項  
 以下のシナリオでは、さまざまな配置とトポロジを紹介します。また、それらを [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の拡張保護でセキュリティ保護するにあたっての推奨構成も示します。  
  
### <a name="direct"></a>[直接]  
 このシナリオでは、イントラネット環境などでのレポート サーバーへの直接的な接続について説明します。  
  
|シナリオ|シナリオを表した図|セキュリティ保護の方法|  
|--------------|----------------------|-------------------|  
|直接的な SSL 通信を使用します。<br /><br /> レポート サーバーにより、クライアントからレポート サーバーへのチャネル バインドが適用されます。|![RS_ExtendedProtection_DirectSSL](../media/rs-extendedprotection-directssl.gif "RS_ExtendedProtection_DirectSSL")<br /><br /> 1) クライアント アプリケーション<br /><br /> 2) レポート サーバー|チャネル バインドには SSL チャネルが使用されるため、サービス バインドは不要です。<br /><br /> `RSWindowsExtendedProtectionLevel` を `Allow` または `Require` に設定します。<br /><br /> `RSWindowsExtendedProtectionScenario` を `Direct` に設定します。|  
|直接的な HTTP 通信を使用します。 レポート サーバーにより、クライアントからレポート サーバーへのサービス バインドが適用されます。|![RS_ExtendedProtection_Direct](../media/rs-extendedprotection-direct.gif "RS_ExtendedProtection_Direct")<br /><br /> 1) クライアント アプリケーション<br /><br /> 2) レポート サーバー|SSL チャネルが存在しないため、チャネル バインドは適用できません。<br /><br /> サービス バインドの検証は可能ですが、チャネル バインドがないため完全な保護は不可能です。サービス バインド自体で防ぐことができるのは、基本的な脅威のみです。<br /><br /> `RSWindowsExtendedProtectionLevel` を `Allow` または `Require` に設定します。<br /><br /> `RSWindowsExtendedProtectionScenario` を `Any` に設定します。|  
  
### <a name="proxy-and-network-load-balancing"></a>プロキシとネットワーク負荷分散  
 クライアント アプリケーションは、エクストラネット、インターネット、セキュリティで保護されたイントラネットなどで、SSL を実行して認証のためにサーバーに資格情報を渡すデバイスまたはソフトウェアに接続します。 クライアントはプロキシに接続します。つまり、すべてのクライアントがプロキシを使用します。  
  
 この状況は、ネットワーク負荷分散 (NLB) デバイスを使用する場合と同じです。  
  
|シナリオ|シナリオを表した図|セキュリティ保護の方法|  
|--------------|----------------------|-------------------|  
|HTTP 通信を使用します。 レポート サーバーにより、クライアントからレポート サーバーへのサービス バインドが適用されます。|![RS_ExtendedProtection_Indirect](../media/rs-extendedprotection-indirect.gif "RS_ExtendedProtection_Indirect")<br /><br /> 1) クライアント アプリケーション<br /><br /> 2) レポート サーバー<br /><br /> 3) プロキシ|SSL チャネルが存在しないため、チャネル バインドは適用できません。<br /><br /> `RSWindowsExtendedProtectionLevel` を `Allow` または `Require` に設定します。<br /><br /> `RSWindowsExtendedProtectionScenario` を `Any` に設定します。<br /><br /> サービス バインドが正しく適用されていることを確認するプロキシ サーバーの名前を把握して、レポート サーバーを構成する必要がありますに注意してください。|  
|HTTP 通信を使用します。<br /><br /> レポート サーバーによって、クライアントからプロキシへのチャネル バインドと、クライアントからレポート サーバーへのサービス バインドが適用されます。|![RS_ExtendedProtection_Indirect_SSL](../media/rs-extendedprotection-indirect-ssl.gif "RS_ExtendedProtection_Indirect_SSL")<br /><br /> 1) クライアント アプリケーション<br /><br /> 2) レポート サーバー<br /><br /> 3) プロキシ|プロキシへの SSL チャネルを利用できるため、プロキシへのチャネル バインドを適用できます。<br /><br /> サービス バインドも適用できます。<br /><br /> レポート サーバーがプロキシ名を把握できなければなりません。レポート サーバーの管理者は、ホスト ヘッダーを使用してプロキシの URL 予約を作成するか、Windows レジストリ エントリ `BackConnectionHostNames` でプロキシ名を構成する必要があります。<br /><br /> `RSWindowsExtendedProtectionLevel` `Allow`または`Require`します。<br /><br /> `RSWindowsExtendedProtectionScenario` を `Proxy` に設定します。|  
|セキュリティで保護されたプロキシとの間接的な HTTPS 通信を使用します。 レポート サーバーによって、クライアントからプロキシへのチャネル バインドと、クライアントからレポート サーバーへのサービス バインドが適用されます。|![RS_ExtendedProtection_IndirectSSLandHTTPS](../media/rs-extendedprotection-indirectsslandhttps.gif "RS_ExtendedProtection_IndirectSSLandHTTPS")<br /><br /> 1) クライアント アプリケーション<br /><br /> 2) レポート サーバー<br /><br /> 3) プロキシ|プロキシへの SSL チャネルを利用できるため、プロキシへのチャネル バインドを適用できます。<br /><br /> サービス バインドも適用できます。<br /><br /> レポート サーバーがプロキシ名を把握できなければなりません。レポート サーバーの管理者は、ホスト ヘッダーを使用してプロキシの URL 予約を作成するか、Windows レジストリ エントリ `BackConnectionHostNames` でプロキシ名を構成する必要があります。<br /><br /> `RSWindowsExtendedProtectionLevel` `Allow`または`Require`します。<br /><br /> `RSWindowsExtendedProtectionScenario` を `Proxy` に設定します。|  
  
### <a name="gateway"></a>ゲートウェイ  
 このシナリオでは、SSL を実行してユーザーを認証するデバイスまたはソフトウェアに接続するクライアント アプリケーションについて説明します。 このデバイスまたはソフトウェアは、ユーザー コンテキストまたは別のユーザー コンテキストを偽装したうえで、レポート サーバーに対して要求を行います。  
  
|シナリオ|シナリオを表した図|セキュリティ保護の方法|  
|--------------|----------------------|-------------------|  
|間接的な HTTP 通信を使用します。<br /><br /> ゲートウェイによって、クライアントからゲートウェイへのチャネル バインドが適用されます。 ゲートウェイとレポート サーバーの間にはサービス バインドが確立されます。|![RS_ExtendedProtection_Indirect_SSL](../media/rs-extendedprotection-indirect-ssl.gif "RS_ExtendedProtection_Indirect_SSL")<br /><br /> 1) クライアント アプリケーション<br /><br /> 2) レポート サーバー<br /><br /> 3) ゲートウェイ デバイス|ゲートウェイがコンテキストを偽装し、新しい NTLM トークンを作成するため、クライアントからレポート サーバーへのチャネル バインドは確立できません。<br /><br /> ゲートウェイとレポート サーバーの間で SSL が使用されないため、チャネル バインドは適用できません。<br /><br /> サービス バインドを適用できます。<br /><br /> `RSWindowsExtendedProtectionLevel` を `Allow` または `Require` に設定します。<br /><br /> `RSWindowsExtendedProtectionScenario` を `Any` に設定します。<br /><br /> 管理者は、チャネル バインドを適用するようにゲートウェイ デバイスを構成する必要があります。|  
|セキュリティで保護されたゲートウェイとの間接的な HTTPS 通信を使用します。 ゲートウェイによってクライアントからゲートウェイへのチャネル バインドが適用され、レポート サーバーによってゲートウェイからレポート サーバーへのチャネル バインドが適用されます。|![RS_ExtendedProtection_IndirectSSLandHTTPS](../media/rs-extendedprotection-indirectsslandhttps.gif "RS_ExtendedProtection_IndirectSSLandHTTPS")<br /><br /> 1) クライアント アプリケーション<br /><br /> 2) レポート サーバー<br /><br /> 3) ゲートウェイ デバイス|ゲートウェイがコンテキストを偽装し、新しい NTLM トークンを作成するため、クライアントからレポート サーバーへのチャネル バインドは確立できません。<br /><br /> ゲートウェイからレポート サーバーへの SSL は、チャネル バインドを適用することができますを意味します。<br /><br /> サービス バインドは不要です。<br /><br /> `RSWindowsExtendedProtectionLevel` を `Allow` または `Require` に設定します。<br /><br /> `RSWindowsExtendedProtectionScenario` を `Direct` に設定します。<br /><br /> 管理者は、チャネル バインドを適用するようにゲートウェイ デバイスを構成する必要があります。|  
  
### <a name="combination"></a>組み合わせ  
 このシナリオでは、クライアントがプロキシに接続するエクストラネット環境またはインターネット環境について説明します。 これは、クライアントがレポート サーバーに接続するイントラネット環境と組み合わせたシナリオです。  
  
|シナリオ|シナリオを表した図|セキュリティ保護の方法|  
|--------------|----------------------|-------------------|  
|クライアントからレポート サーバー サービスへの間接的なアクセスと直接的なアクセスを行います。クライアントからプロキシ、またはクライアントからレポート サーバーへの接続で SSL を使用しません。|1) クライアント アプリケーション<br /><br /> 2) レポート サーバー<br /><br /> 3) プロキシ<br /><br /> 4) クライアント アプリケーション|クライアントからレポート サーバーへのサービス バインドを適用できます。<br /><br /> レポート サーバーがプロキシ名を把握できなければなりません。レポート サーバーの管理者は、ホスト ヘッダーを使用してプロキシの URL 予約を作成するか、Windows レジストリ エントリ `BackConnectionHostNames` でプロキシ名を構成する必要があります。<br /><br /> `RSWindowsExtendedProtectionLevel` を `Allow` または `Require` に設定します。<br /><br /> `RSWindowsExtendedProtectionScenario` を `Any` に設定します。|  
|クライアントからレポート サーバーへの間接的なアクセスと直接的なアクセスを行います。その際、クライアントからプロキシまたはレポート サーバーへの SSL 接続を確立します。|![RS_ExtendedProtection_CombinationSSL](../media/rs-extendedprotection-combinationssl.gif "RS_ExtendedProtection_CombinationSSL")<br /><br /> 1) クライアント アプリケーション<br /><br /> 2) レポート サーバー<br /><br /> 3) プロキシ<br /><br /> 4) クライアント アプリケーション|チャネル バインドを適用できます。<br /><br /> プロキシの名前は、レポート サーバーに認識する必要があります。 また、レポート サーバー管理者必要がありますホスト ヘッダーを使用してプロキシの URL 予約を作成するか、Windows レジストリ エントリでプロキシ名を構成`BackConnectionHostNames`します。<br /><br /> `RSWindowsExtendedProtectionLevel` を `Allow` または `Require` に設定します。<br /><br /> `RSWindowsExtendedProtectionScenario` を `Proxy` に設定します。|  
  
## <a name="configuring-reporting-rervices-extended-protection"></a>Reporting Services の拡張保護の構成  
 `rsreportserver.config`ファイルには動作を制御する構成値が含まれています[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]拡張保護します。  
  
 使用と編集の詳細については、`rsreportserver.config`ファイルを参照してください[RSReportServer Configuration File](../report-server/rsreportserver-config-configuration-file.md)します。 拡張保護の設定は、WMI API を使用して変更および確認することもできます。 詳細については、「 [SetExtendedProtectionSettings Method &#40;WMI MSReportServer_ConfigurationSetting&#41; (SetExtendedProtectionSettings メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;)](../wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md)」を参照してください。  
  
 構成設定の検証が失敗した場合、`RSWindowsNTLM`、`RSWindowsKerberos`、および `RSWindowsNegotiate` の各認証の種類がレポート サーバーで無効になります。  
  
###  <a name="ConfigurationSettings"></a> Reporting Services の拡張保護の構成設定  
 次の表では、拡張保護の `rsreportserver.config` に含まれる構成設定について説明します。  
  
|設定|説明|  
|-------------|-----------------|  
|`RSWindowsExtendedProtectionLevel`|拡張保護の適用レベルを指定します。 有効な値は `Off`、`Allow`、`Require` です。<br /><br /> 既定値は `Off` です。<br /><br /> `Off` を指定した場合、チャネル バインドまたはサービス バインドの検証は行われません。<br /><br /> `Allow` を指定した場合、拡張保護はサポートされますが、要求されません。 Allow を指定した場合、次の効果があります。<br /><br /> 拡張保護がサポートされているオペレーティング システムで実行中のクライアント アプリケーションに対し、拡張保護が適用されます。 保護の適用方法は、`RsWindowsExtendedProtectionScenario` 設定によって決まります。<br /><br /> 拡張保護がサポートされていないオペレーティング システムで実行中のアプリケーションに対し、認証が許可されます。<br /><br /> `Require` を指定した場合、次の効果があります。<br /><br /> 拡張保護がサポートされているオペレーティング システムで実行中のクライアント アプリケーションに対し、拡張保護が適用されます。<br /><br /> 認証は**いない**拡張保護がサポートされていないオペレーティング システムで実行されているアプリケーションに許可します。|  
|`RsWindowsExtendedProtectionScenario`|検証する拡張保護の形式を指定します。チャネル バインド、サービス バインド、またはその両方です。 有効な値は `Any`、`Proxy`、`Direct` です。<br /><br /> 既定値は `Proxy` です。<br /><br /> `Any` を指定した場合、次の効果があります。<br /><br /> \- Windows NTLM 認証、Kerberos 認証、およびネゴシエート認証とチャネル バインドは要求されません。<br /><br /> \- サービス バインドが適用されます。<br /><br /> `Proxy` を指定した場合、次の効果があります。<br /><br /> \- チャネル バインド トークンが存在する場合は、Windows NTLM 認証、Kerberos 認証、およびネゴシエート認証が行われます。<br /><br /> \- サービス バインドが適用されます。<br /><br /> `Direct` を指定した場合、次の効果があります。<br /><br /> \- CBT と現在のサービスへの SSL 接続が存在し、SSL 接続の CBT が NTLM、Kerberos、またはネゴシエート トークンの CBT に一致する場合に、それぞれ Windows NTLM 認証、Kerberos 認証、またはネゴシート認証が行われます。<br /><br /> \- サービス バインドは適用されません。<br /><br /> <br /><br /> 注:場合、この設定は無視されます`RsWindowsExtendedProtectionLevel`に設定されている`OFF`します。|  
  
 `rsreportserver.config` 構成ファイル内のエントリの例を次に示します。  
  
```  
<Authentication>  
         <RSWindowsExtendedProtectionLevel>Allow</RSWindowsExtendedProtectionLevel>  
         <RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionLevel>  
</Authentication>  
```  
  
## <a name="service-binding-and-included-spns"></a>サービス バインドと含まれる SPN  
 サービス バインドでは、サービス プリンシパル名 (SPN) を使用して認証トークンの目的の送信先を検証します。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] は、既存の URL 予約情報を使用して、有効と見なされる SPN のリストを作成します。 SPN と URL 予約の両方の検証に URL 予約情報を使用することにより、システム管理者による一元管理が可能になります。  
  
 有効な SPN のリストが更新されるのは、レポート サーバーを起動したとき、拡張保護の構成設定を変更したとき、またはアプリケーション ドメインをリサイクルしたときです。  
  
 有効な SPN のリストは、各アプリケーションに固有です。 たとえば、レポート マネージャーとレポート サーバーでは、有効な SPN のリストが別々に計算されます。  
  
 アプリケーションに対して計算される有効な SPN のリストは、次の要素によって決定されます。  
  
-   各 URL 予約。  
  
-   Reporting Services サービス アカウント用にドメイン コントローラーから取得した各 SPN。  
  
-   URL 予約にワイルドカード文字 (* または +) が含まれている場合は、レポート サーバーによってホスト コレクションから各エントリが追加されます。  
  
### <a name="hosts-collection-sources"></a>ホスト コレクションのソース  
 次の表に、ホスト コレクションのソースとなり得るものを示します。  
  
|ソースの種類|説明|  
|--------------------|-----------------|  
|ComputerNameDnsDomain|ローカル コンピューターに割り当てられた DNS ドメインの名前。 ローカル コンピューターがクラスター内のノードである場合、クラスターの仮想サーバーの DNS ドメイン名が使用されます。|  
|ComputerNameDnsFullyQualified|ローカル コンピューターを一意に識別する完全修飾 DNS 名。 この名前は、 *HostName*.*DomainName*という形式で DNS ホスト名と DNS ドメイン名を組み合わせたものです。 ローカル コンピューターがクラスター内のノードである場合、クラスターの仮想サーバーの完全修飾 DNS 名が使用されます。|  
|ComputerNameDnsHostname|ローカル コンピューターの DNS ホスト名。 ローカル コンピューターがクラスター内のノードである場合、クラスターの仮想サーバーの DNS ホスト名が使用されます。|  
|ComputerNameNetBIOS|ローカル コンピューターの NetBIOS 名。 ローカル コンピューターがクラスター内のノードである場合、クラスターの仮想サーバーの NetBIOS 名が使用されます。|  
|ComputerNamePhysicalDnsDomain|ローカル コンピューターに割り当てられた DNS ドメインの名前。 ローカル コンピューターがクラスター内のノードである場合、クラスターの仮想サーバーの名前ではなく、ローカル コンピューターの DNS ドメイン名が使用されます。|  
|ComputerNamePhysicalDnsFullyQualified|コンピューターを一意に識別する完全修飾 DNS 名。 ローカル コンピューターがクラスター内のノードである場合、クラスターの仮想サーバーの名前ではなく、ローカル コンピューターの完全修飾 DNS 名が使用されます。<br /><br /> この完全修飾 DNS 名は、 *HostName*.*DomainName*という形式で DNS ホスト名と DNS ドメイン名を組み合わせたものです。|  
|ComputerNamePhysicalDnsHostname|ローカル コンピューターの DNS ホスト名。 ローカル コンピューターがクラスター内のノードである場合、クラスターの仮想サーバーの名前ではなく、ローカル コンピューターの DNS ホスト名が使用されます。|  
|ComputerNamePhysicalNetBIOS|ローカル コンピューターの NetBIOS 名。 ローカル コンピューターがクラスター内のノードである場合、クラスターの仮想サーバーの名前ではなく、ローカル コンピューターの NetBIOS 名が使用されます。|  
  
 SPN が追加されると、トレース ログに次のようなエントリが追加されます。  
  
 `rshost!rshost!10a8!01/07/2010-19:29:38:: i INFO: SPN Whitelist Added <ComputerNamePhysicalNetBIOS> - <theservername>.`  
  
 `rshost!rshost!10a8!01/07/2010-19:29:38:: i INFO: SPN Whitelist Added <ComputerNamePhysicalDnsHostname> - <theservername>.`  
  
 詳細については、「[レポート サーバーのサービス プリンシパル名 &#40;SPN&#41; の登録](../report-server/register-a-service-principal-name-spn-for-a-report-server.md)」(レポート サーバーのサービス プリンシパル名 &#40;SPN&#41; の登録) および「[URL の予約と登録について &#40;SSRS 構成マネージャー&#41;](../install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [拡張保護を使用したデータベース エンジンへの接続](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)   
 [認証の拡張保護の概要](https://go.microsoft.com/fwlink/?LinkID=177943)   
 [拡張保護付き統合 Windows 認証](https://go.microsoft.com/fwlink/?LinkId=179922)   
 [マイクロソフト セキュリティ アドバイザリ:認証の拡張保護](https://go.microsoft.com/fwlink/?LinkId=179923)   
 [Report Server Service Trace Log](../report-server/report-server-service-trace-log.md)   
 [RSReportServer 構成ファイル](../report-server/rsreportserver-config-configuration-file.md)   
 [SetExtendedProtectionSettings Method &#40;WMI MSReportServer_ConfigurationSetting&#41; (SetExtendedProtectionSettings メソッド &#40;WMI MSReportServer_ConfigurationSetting&#41;)](../wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md)  
  
  
