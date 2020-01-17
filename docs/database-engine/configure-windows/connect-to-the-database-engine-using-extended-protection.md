---
title: 拡張保護を使用したデータベース エンジンへの接続 | Microsoft Docs
ms.custom: ''
ms.date: 05/21/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- spoofing attacks
- service binding
- luring attacks
- Schannel
- channel binding
- Extended Protection
ms.assetid: ecfd783e-7dbb-4a6c-b5ab-c6c27d5dd57f
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 5216b324477f1af7fb727af3462ccce8d64e6a64
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68012098"
---
# <a name="connect-to-the-database-engine-using-extended-protection"></a>拡張保護を使用したデータベース エンジンへの接続
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では **で始まる** 拡張保護 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]がサポートされています。 **認証の拡張保護** とは、オペレーティング システムで実装されているネットワーク コンポーネントの機能です。 **拡張保護** は、Windows 7 および Windows Server 2008 R2 でサポートされており、 **以前のオペレーティング システムでは、** 拡張保護 [!INCLUDE[msCoName](../../includes/msconame-md.md)] がサービス パックに含まれています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の接続を **拡張保護**を使用して確立することで、安全性を高めることができます。  
  
> [!IMPORTANT]  
> 既定では、Windows の **拡張保護** は有効になっていません。 Windows で **拡張保護** を有効にする方法の詳細については、「 [認証に対する保護の強化](/dotnet/framework/wcf/feature-details/extended-protection-for-authentication-overview)」を参照してください。
  
## <a name="description-of-extended-protection"></a>拡張保護の説明  
 **拡張保護** では、認証リレー攻撃を防止するために、サービス バインドとチャネル バインドが使用されます。 認証リレー攻撃では、NTLM 認証を実行できるクライアント (Windows エクスプローラー、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Outlook、.NET SqlClient アプリケーションなど) が攻撃者のサーバー (悪意のある CIFS ファイル サーバーなど) に接続します。 攻撃者は、そのクライアントの資格情報を使用してクライアントになりすまし、サービス ([!INCLUDE[ssDE](../../includes/ssde-md.md)] サービスのインスタンスなど) への認証を行います。  
  
 この攻撃には次の 2 つのバリエーションがあります。  
  
-   おびき寄せによる攻撃。クライアントが自ら攻撃者のサーバーに接続するようにおびき寄せられます。  
  
-   なりすましによる攻撃。正当なサービスに接続しているつもりのクライアントが、汚染された DNS ルーティングや IP ルーティングによって、知らない間に攻撃者のサーバーにリダイレクトされます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対するこれらの攻撃を減らすために、サービス バインドとチャネル バインドがサポートされています。  
  
### <a name="service-binding"></a>サービス バインド  
 サービス バインドでは、接続しようとしている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの署名付きサービス プリンシパル名 (SPN) を送信するようにクライアントに要求することで、おびき寄せによる攻撃に対処します。 サービスでは、認証応答の一部として、パケットで受信した SPN がサービス自身の SPN と一致するかどうかの確認が行われます。 クライアントが攻撃者のサーバーに接続するようにおびき寄せられている場合は、パケットに攻撃者の署名付き SPN が含まれます。 そのため、攻撃者がパケットをリレーして本物の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスにクライアントとして認証を受けることはできません。 サービス バインドのコストはごく小さく、1 回しか発生しませんが、サービス バインドではなりすましによる攻撃には対処できません。 サービス バインドが発生するのは、クライアント アプリケーションが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]への接続に暗号化を使用しない場合です。  
  
### <a name="channel-binding"></a>チャネル バインド  
 チャネル バインドでは、クライアントと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス インスタンスとの間に、セキュリティで保護されたチャネル (Schannel) を確立します。 サービスでは、クライアントとサービス自身のチャネル固有のチャネル バインド トークン (CBT) を比較することにより、クライアントが本物かどうかが確認されます。 チャネル バインドでは、おびき寄せによる攻撃となりすましによる攻撃の両方に対処できますが、 すべてのセッション トラフィックのトランスポート層セキュリティ (TLS) 暗号化が必要になるため、実行時のコストが大きくなります。 チャネル バインドが発生するのは、暗号化がクライアントとサーバーのどちらで強制されているかにかかわらず、クライアント アプリケーションが暗号化を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続する場合です。  
  
> [!WARNING]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 向けの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および [!INCLUDE[msCoName](../../includes/msconame-md.md)] データ プロバイダーでは、SSL 3.0、TLS 1.0 がサポートされています。 オペレーティング システムの SChannel 層を変更して別のプロトコル (TLS 1.1、TLS 1.2 など) を適用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続に失敗する可能性があります。  
  
### <a name="operating-system-support"></a>オペレーティング システムのサポート  
 Windows による **拡張保護**のサポートの詳細については、以下のリンク先を参照してください。  
  
-   [拡張保護付き統合 Windows 認証](https://msdn.microsoft.com/library/dd639324.aspx)  
  
-   [マイクロソフト セキュリティ アドバイザリ (973811)、認証の拡張保護](/security-updates/SecurityAdvisories/2009/973811)
  
## <a name="settings"></a>[設定]  
 サービス バインドとチャネル バインドに影響する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の接続設定は 3 つあります。 これらの設定を構成するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーまたは WMI を使用します。これらの設定を表示するには、ポリシー ベースの管理の **[サーバー プロトコル設定]** ファセットを使用します。  
  
-   **[強制的に暗号化]**  
  
     選択できる値は、 **[オン]** と **[オフ]** です。 チャネル バインドを使用する場合は、 **[強制的に暗号化]** を **[オン]** に設定して、すべてのクライアントで暗号化が強制されるようにする必要があります。 この設定を **[オフ]** にした場合、保証されるのはサービス バインドだけになります。 **[強制的に暗号化]** は、 **構成マネージャーの** [MSSQLSERVER のプロトコルのプロパティ] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([フラグ] タブ) にあります。  
  
-   **拡張保護**  
  
     選択できる値は、 **[オフ]** 、 **[許可]** 、および **[必須]** です。 **拡張保護** 変数を使用すると、各 **インスタンスの** 拡張保護 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レベルを構成できます。 **[拡張保護]** は、 **構成マネージャーの** [MSSQLSERVER のプロトコルのプロパティ] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([詳細設定] タブ) にあります。  
  
    -   **[オフ]** に設定すると、 **[拡張保護]** は無効になります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスは、クライアントが保護されているかどうかに関係なく、任意のクライアントからの接続を許可します。 **[オフ]** は、古いオペレーティング システムや修正プログラムの適用が解除されたオペレーティング システムと互換性がありますが、安全性は低くなります。 この設定は、クライアント オペレーティング システムで拡張保護がサポートされていないことがわかっている場合に使用してください。  
  
    -   **[許可]** に設定すると、 **拡張保護** をサポートするオペレーティング システムからの接続に **拡張保護**が必要になります。 **拡張保護** をサポートしないオペレーティング システムからの接続では **拡張保護**が無視されます。 保護されたクライアント オペレーティング システムで実行されている保護されていないクライアント アプリケーションからの接続は拒否されます。 この設定は、 **[オフ]** よりも安全性が高いですが、最も安全な設定ではありません。 この設定は、 **拡張保護** をサポートするオペレーティング システムとサポートしないオペレーティング システムが混在する環境で使用します。  
  
    -   **[必須]** に設定すると、保護されたクライアント オペレーティング システム上の保護されているアプリケーションからの接続のみが許可されます。 この設定は最も安全ですが、 **拡張保護** をサポートしないオペレーティング システムやアプリケーションからの接続では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続することができません。  
  
-   **[承認された NTLM SPN]**  
  
     **[承認された NTLM SPN]** の変数は、サーバーに複数の SPN がある場合に必要です。 クライアントがサーバーへの接続に使用した有効な SPN がサーバーで認識されないと、サービス バインドが失敗します。 この問題を回避するには、 **[承認された NTLM SPN]** を使用して、サーバーを表す複数の SPN を指定します。 **[承認された NTLM SPN]** には、一連の SPN をセミコロンで区切って指定します。 たとえば、 **MSSQLSvc/ HostName1.Contoso.com** および **MSSQLSvc/ HostName2.Contoso.com**という SPN を許可するには、 **[承認された NTLM SPN]** ボックスに「 **MSSQLSvc/HostName1.Contoso.com;MSSQLSvc/HostName2.Contoso.com** 」と入力します。 変数の最大長は 2048 文字です。 **[承認された NTLM SPN]** は、 **構成マネージャーの** [MSSQLSERVER のプロトコルのプロパティ] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([詳細設定] タブ)) にあります。  
  
## <a name="enabling-extended-protection-for-the-database-engine"></a>データベース エンジンでの拡張保護の有効化  
 **拡張保護**を使用するには、サーバーとクライアントの両方のオペレーティング システムで **拡張保護**がサポートされていて、オペレーティング システムで **拡張保護** が有効になっている必要があります。 オペレーティング システムで **拡張保護** を有効にする方法の詳細については、「 [認証に対する保護の強化](/dotnet/framework/wcf/feature-details/extended-protection-for-authentication-overview)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では **で始まる** 拡張保護 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]がサポートされています。 以前のバージョンの**については、今後の更新によって一部で** 拡張保護 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用できるようになります。 サーバー コンピューターで **拡張保護** を有効にした後、次の手順に従って **拡張保護**を有効にします。  
  
1.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[Microsoft SQL Server]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。  
  
2.  **[SQL Server ネットワークの構成]** を展開し、 **[** _\<_InstanceName *> のプロトコル]* を右クリックして、 **[プロパティ]** をクリックします。  
  
3.  チャネル バインドとサービス バインドの両方について、 **[詳細設定]** タブで **[拡張保護]** を適切な値に設定します。  
  
4.  サーバーに複数の SPN がある場合は、 **[詳細設定]** タブで **[承認された NTLM SPN]** フィールドを構成します。詳細については、「設定」セクションを参照してください。  
  
5.  チャネル バインドを使用する場合は、 **[フラグ]** タブで **[強制的に暗号化]** を **[オン]** に設定します。  
  
6.  [!INCLUDE[ssDE](../../includes/ssde-md.md)] サービスを再開します。  
  
## <a name="configuring-other-sql-server-components"></a>その他の SQL Server コンポーネントの構成  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]の 構成方法の詳細については、「 [Reporting Services での認証の拡張保護](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)」を参照してください。  
  
 IIS を使用して HTTP 接続または HTTPS 接続経由で [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データにアクセスする場合は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] で IIS によって提供される拡張保護を利用できます。 拡張保護を使用するように IIS を構成する方法の詳細については、「 [IIS 7.5 における拡張保護の構成](https://go.microsoft.com/fwlink/?LinkId=181105)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [サーバー ネットワークの構成](../../database-engine/configure-windows/server-network-configuration.md)   
 [クライアント ネットワーク構成](../../database-engine/configure-windows/client-network-configuration.md)   
 [認証の拡張保護の概要](https://go.microsoft.com/fwlink/?LinkID=177943)   
 [拡張保護付き統合 Windows 認証](https://go.microsoft.com/fwlink/?LinkId=179922)  
  
  
