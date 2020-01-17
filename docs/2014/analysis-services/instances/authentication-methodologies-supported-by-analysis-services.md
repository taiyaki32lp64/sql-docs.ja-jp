---
title: Analysis Services でサポートされる認証方法 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b7aee903-d33a-4c20-86c2-aa013a50949f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a57aff903d41e8bcddef25e21def39a45e33d23f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080342"
---
# <a name="authentication-methodologies-supported-by-analysis-services"></a>Analysis Services でサポートされる認証方法
  クライアント アプリケーションから Analysis Services インスタンスへの接続には Windows 認証 (統合) が必要です。 次の手法のいずれかを使用して Windows ユーザー ID を指定できます。  
  
-   NTLM  
  
-   Kerberos (詳細については、「 [Kerberos の制約付き委任のための Analysis Services の構成](configure-analysis-services-for-kerberos-constrained-delegation.md)」をご覧ください)  
  
-   接続文字列での EffectiveUserName  
  
-   基本または匿名 (HTTP アクセスの構成が必要)  
  
-   格納された資格情報  
  
 要求認証はサポートされません。 Windows クレーム トークンを使用して Analysis Services にアクセスすることはできません。 Analysis Services クライアント ライブラリは、Windows セキュリティ プリンシパルでのみ機能します。 使用する BI ソリューションにクレーム ID が含まれている場合は、各ユーザーの Windows ID シャドウ アカウントが必要になるか、保存された資格情報を使用して Analysis Services データにアクセスすることになります。  
  
 BI および Analysis Services の認証フローの詳細については、「 [Microsoft BI 認証と ID 委任](https://go.microsoft.com/fwlink/?LinkID=286576)」をご覧ください。  
  
##  <a name="bkmk_auth"></a> 別の認証手法について  
 Analysis Services データベースへの接続には、Windows ユーザーまたはグループの ID と、関連付けられた権限が必要です。 ID は、レポートを表示する必要のある任意のユーザーが使用する、一般的な目的のログインである場合もありますが、通常のシナリオでは、個々のユーザーの ID です。  
  
 多くの場合、表形式または多次元のモデルには、だれが要求しているかに応じて、オブジェクトごとに、またはデータ自体の内部にさまざまなレベルのデータ アクセスがあります。 この要件を満たすには、NTLM、Kerberos、EffectiveUserName、または基本認証を使用できます。 これらの手法はすべて、各接続で異なるユーザー ID を渡すための方法です。 ただし、これらのほとんどは、シングルホップの制限の対象です。 委任を伴う Kerberos でのみ、元のユーザー ID を、リモート サーバー上のバックエンド データ ストアへの複数のコンピューター接続にわたって使用できます。  
  
 **NTLM**  
  
 `SSPI=Negotiate`を指定した接続では、Kerberos ドメイン コントローラーを使用できない場合に、NTLM がバックアップ認証サブシステムとして使用されます。 NTLM では、あらゆるユーザーまたはクライアント アプリケーションがサーバー リソースにアクセスできます。ただし、要求がクライアントからサーバーへの直接接続で、接続を要求しているユーザーにリソースへのアクセス権があり、クライアント コンピューターとサーバー コンピューターが同じドメインにある場合に限ります。  
  
 多層ソリューションでは、NLTM のシングルホップ制限が大きな制約となる場合があります。 要求を行っているユーザー ID は、ただ 1 台のリモート サーバーでのみ権限を借用できます。それ以上は不可能です。 現在の操作に、複数のコンピューターで動作しているサービスが必要な場合は、セキュリティ トークンの再利用によって、同じ ID がバックエンド サーバーでも使用できるように、Kerberos の制約付き委任を構成する必要があります。 別の方法として、保存された資格情報または基本認証を使用して、シングルホップ接続上に新しい ID 情報を渡すこともできます。  
  
 **Kerberos 認証および Kerberos 制約付き委任**  
  
 Kerberos 認証は、Active Directory ドメインの Windows 統合セキュリティの基礎です。 NTLM のように、委任を有効にしない限り、Kerberos での権限借用はシングルホップに制限されます。  
  
 マルチホップ接続をサポートするために、Kerberos は、制約付き委任と制約なし委任の両方を提供していますが、ほとんどのシナリオでは、制約付き委任がセキュリティの推奨方法と見なされます。 制約付き委任では、サービスがユーザー ID のセキュリティ トークンを、リモート コンピューター上の指定された下位レベル サービスに渡すことが許可されます。 多層アプリケーションの場合、中間層アプリケーション サーバーから、Analysis Services などのバックエンド データベースへのユーザー ID の委任は、一般的な要件です。 たとえば、ユーザー ID に基づいてさまざまなデータを返す表形式または多次元のモデルでは、中間層サービスからの ID の委任を要求し、ユーザーが資格情報を再入力せずに済むようにしたり、セキュリティ資格情報を他の方法で入手したりします。  
  
 Active Directory では、制約付き委任に、追加の構成が必要です。これは、要求の送信側と受信側の両方にあるサービスが明示的に委任を承認されているためです。 事前に構成のコストが発生しますが、サービスを構成した後は、パスワードの更新が Active Directory で個別に管理されます。 以降で説明する、保存された資格情報オプションを使用している場合のように、アプリケーションに保存されたアカウント情報を更新する必要はありません。  
  
 制約付き委任用に Analysis Services を構成する方法の詳細については、「 [Kerberos の制約付き委任のための Analysis Services の構成](configure-analysis-services-for-kerberos-constrained-delegation.md)」をご覧ください。  
  
> [!NOTE]  
>  Windows Server 2012 は、すべてのドメインで制約付き委任をサポートしています。 対照的に、Windows Server 2008 や 2008 R2 など、より低い機能レベルのドメインでの Kerberos 制約付き委任の構成では、クライアントとサーバーのコンピューターが両方とも、同じドメインのメンバーであることが必要です。  
  
 **EffectiveUserName**  
  
 EffectiveUserName は、ID 情報を Analysis Services に渡すために使用される接続文字列です。 PowerPivot for SharePoint は、これを使用して、ユーザーの利用状況を使用状況ログに記録します。 Excel Services と PerformancePoint Services は、これを使用して、SharePoint でブックやダッシュボードが使用するデータを取得します。 また、Analysis Services インスタンスで操作を実行するカスタムのアプリケーションやスクリプトでも、この接続文字列が使用されます。  
  
 SharePoint での EffectiveUserName の使用の詳細については、「 [Use Analysis Services EffectiveUserName in SharePoint Server 2010](https://go.microsoft.com/fwlink/?LinkId=311905)」(SharePoint Server 2010 で Analysis Services の EffectiveUserName を使用する) をご覧ください。  
  
 **基本認証と匿名ユーザー**  
  
 基本認証は、特定のユーザーとしてバックエンド サーバーに接続する場合の第 4 の方法となります。 基本認証を使用すると、ワイヤ暗号化の要件が強化されて、Windows のユーザー名とパスワードが接続文字列で渡されるため、転送中に機密情報が確実に保護されます。 基本認証の使用の重要なメリットは、ドメインの境界を越えて認証を要求できることです。  
  
 匿名認証の場合は、匿名ユーザー ID を、特定の Windows ユーザー アカウント (既定では IUSR_GUEST) またはアプリケーション プール ID に対して設定できます。 匿名ユーザー アカウントは、Analysis Services 接続で使用され、Analysis Services インスタンスに対するデータ アクセス権限を備えている必要があります。 このアプローチを使用すると、匿名アカウントに関連付けられたユーザー ID のみが接続で使用されます。 追加の ID 管理がアプリケーションに必要な場合は、他のアプローチのいずれかを選択するか、現在の ID 管理ソリューションを補う必要があります。  
  
 基本と匿名は、IIS と msmdpump.dll を使用して接続を確立し、Analysis Services を HTTP アクセス向けに構成した場合にのみ使用できます。 詳細については、「 [インターネット インフォメーション サービス &#40;IIS&#41; 8.0 上の Analysis Services への HTTP アクセスの構成](configure-http-access-to-analysis-services-on-iis-8-0.md)」をご覧ください。  
  
 **Stored Credentials**  
  
 中間層アプリケーションのほとんどには、ユーザー名とパスワードを保存する機能が含まれており、これを使用して、以降の動作で、Analysis Services や SQL Server リレーショナル エンジンなどの下位データ ストアからデータを取得します。 そのため、保存された資格情報は、データを取得するための第 5 の方法となります。 このアプローチでの制限としては、ユーザー名とパスワードを最新の状態に保つためのメンテナンスのオーバーヘッドと、接続での単一の ID の使用があります。 本来の呼び出し元の ID がソリューションに必要な場合、保存された資格情報は、利用可能な方法ではありません。  
  
 保存された資格情報の詳細については、「[共有データ ソースを作成、変更、および削除する &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)」および「[SharePoint Server 2013 の Secure Store Service で Excel Services を使用する](https://go.microsoft.com/fwlink/?LinkID=309869)」をご覧ください。  
  
## <a name="see-also"></a>関連項目  
 [トランスポート セキュリティでの権限借用の使用](https://go.microsoft.com/fwlink/?LinkId=311727)   
 [インターネット インフォメーション サービス &#40;IIS&#41; 8.0 上の Analysis Services への HTTP アクセスの構成](configure-http-access-to-analysis-services-on-iis-8-0.md)   
 [Kerberos の制約付き委任のための Analysis Services の構成](configure-analysis-services-for-kerberos-constrained-delegation.md)   
 [Analysis Services インスタンスの SPN 登録](spn-registration-for-an-analysis-services-instance.md)   
 [Analysis Services への接続](connect-to-analysis-services.md)  
  
  
