---
title: MSSQLSERVER のプロトコルのプロパティ ([詳細設定] タブ) | Microsoft Docs
ms.custom: ''
ms.date: 01/24/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: abd5ca68-825f-4c07-b27c-3b3a79d03d74
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e2cce3ddb17324e234395dcf764855dcffbc44ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071983"
---
# <a name="protocols-for-mssqlserver-properties-advanced-tab"></a>MSSQLSERVER のプロトコルのプロパティ ([詳細設定] タブ)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**[MSSQLSERVER のプロトコルのプロパティ]** ダイアログ ボックスの **[詳細設定]** タブを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]の**認証の拡張保護**を構成します。 **拡張保護** とは、オペレーティング システムで実装されているネットワーク コンポーネントの機能です。 **拡張保護** は、Windows 7 および Windows Server 2008 R2 で使用でき、それ以前のオペレーティング システムではサービス パックに含まれています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の接続を **拡張保護**を使用して確立することで、安全性を高めることができます。 **拡張保護** の利点には、 **[フラグ]** タブで **[強制的に暗号化]** を選択していないと得られないものもあります。

> [!IMPORTANT]  
> 既定では、Windows の **拡張保護** は有効になっていません。 **拡張保護**を有効にする方法の詳細については、次を参照してください。
> - [Windows 拡張保護\<の extendedprotection\>](https://docs.microsoft.com/iis/configuration/system.webserver/security/authentication/windowsauthentication/extendedprotection/)
> - [認証の拡張保護の概要](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/extended-protection-for-authentication-overview)

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の他のサービスの構成方法と **拡張保護**の詳細については、 [Microsoft.com](https://go.microsoft.com/fwlink/?LinkId=177752)の最新情報を参照してください。

**拡張保護** は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以降の [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]Native Client によって完全にサポートされています。 その他の **クライアント プロバイダーでは、** 拡張保護 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は現時点ではサポートされていません。

## <a name="options"></a>オプション

### <a name="extended-protection"></a>で始まる

指定可能な 3 つの値は次のとおりです。  

- **Off**:**拡張保護**が無効であることを意味します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスは、クライアントが保護されているかどうかに関係なく、任意のクライアントからの接続を許可します。 **[オフ]** は、古いオペレーティング システムや修正プログラムの適用が解除されたオペレーティング システムと互換性がありますが、安全性は低くなります。 この設定は、クライアント オペレーティング システムで拡張保護がサポートされていないことがわかっている場合にのみ使用してください。

- **[許可]** : **[拡張保護]** をサポートするオペレーティング システムからの接続に **[拡張保護]** が必要になります。 保護されたクライアント オペレーティング システムで実行されている保護されていないクライアント アプリケーションからの接続は拒否されます。 保護されていないオペレーティング システムからの接続では、**拡張保護** が無視されます。 この設定は、 **[オフ]** よりも安全性が高いですが、最も安全な設定ではありません。 この設定は、 **拡張保護** をサポートするオペレーティング システムやアプリケーションとサポートしないオペレーティング システムやアプリケーションが混在する環境で使用します。

- **必須**: 接続を受け入れるには、保護されたオペレーティングシステム上の保護されたアプリケーションから取得する必要があります。 この設定は、3つのオプションの中で最も安全です。 ただし、**拡張保護**をサポートしていないオペレーティングシステムからの接続は、に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]接続できません。

### <a name="accepted-ntlm-spns"></a>[承認された NTLM SPN]

のインスタンスは[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、複数の NTLM サービスプリンシパル名 (SPN) によって識別できます。 Spn は、セミコロンで区切られた一連の文字列として一覧表示されます。 たとえば、値 **MSSQLSvc/HostName1.Contoso.com;MSSQLSvc/HostName2.Contoso.com** は、**MSSQLSvc/HOST1.Contoso.com** または **MSSQLSvc/HOST2.Contoso.com** という名前の SPN への接続を試みているクライアントが許可されることを示します。 変数の最大長は 2048 文字です。

## <a name="see-also"></a>参照

[Reporting Services での認証の拡張保護](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)

