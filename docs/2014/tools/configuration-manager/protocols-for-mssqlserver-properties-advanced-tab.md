---
title: MSSQLSERVER のプロトコルのプロパティ ([詳細設定] タブ) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: abd5ca68-825f-4c07-b27c-3b3a79d03d74
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9000dd2b7456036f4828640694aaf697036b71d7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62645793"
---
# <a name="protocols-for-mssqlserver-properties-advanced-tab"></a>MSSQLSERVER のプロトコルのプロパティ ([詳細設定] タブ)
  **[MSSQLSERVER のプロトコルのプロパティ]** ダイアログ ボックスの **[詳細設定]** タブを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]の**認証の拡張保護**を構成します。 **拡張保護** とは、オペレーティング システムで実装されているネットワーク コンポーネントの機能です。 **拡張保護** は、Windows 7 および Windows Server 2008 R2 で使用でき、それ以前のオペレーティング システムではサービス パックに含まれています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の接続を **拡張保護**を使用して確立することで、安全性を高めることができます。 **拡張保護** の利点には、 **[フラグ]** タブで **[強制的に暗号化]** を選択していないと得られないものもあります。  
  
> [!IMPORTANT]  
>  既定では、Windows の **拡張保護** は有効になっていません。 Windows で **拡張保護** を有効にする方法の詳細については、サポート技術情報の記事「 [認証に対する保護の強化](https://go.microsoft.com/fwlink/?LinkId=178431)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の他のサービスの構成方法と **拡張保護**の詳細については、 [Microsoft.com](https://go.microsoft.com/fwlink/?LinkId=177752)の最新情報を参照してください。  
  
 **拡張保護** は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以降の [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]Native Client によって完全にサポートされています。 その他の **クライアント プロバイダーでは、** 拡張保護 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は現時点ではサポートされていません。  
  
## <a name="options"></a>および  
 **拡張保護**  
 指定可能な 3 つの値は次のとおりです。  
  
-   **[オフ]** に設定すると、 **[拡張保護]** は無効になります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスは、クライアントが保護されているかどうかに関係なく、任意のクライアントからの接続を許可します。 **[オフ]** は、古いオペレーティング システムや修正プログラムの適用が解除されたオペレーティング システムと互換性がありますが、安全性は低くなります。 この設定は、クライアント オペレーティング システムで拡張保護がサポートされていないことがわかっている場合にのみ使用してください。  
  
-   **[許可]** に設定すると、 **拡張保護** をサポートするオペレーティング システムからの接続に **拡張保護**が必要になります。 保護されたクライアント オペレーティング システムで実行されている保護されていないクライアント アプリケーションからの接続は拒否されます。 保護されていないオペレーティング システムからの接続では、**拡張保護** が無視されます。 この設定は、 **[オフ]** よりも安全性が高いですが、最も安全な設定ではありません。 この設定は、 **拡張保護** をサポートするオペレーティング システムやアプリケーションとサポートしないオペレーティング システムやアプリケーションが混在する環境で使用します。  
  
-   **[必須]** に設定すると、保護されたクライアント オペレーティング システム上の保護されているアプリケーションからの接続のみが許可されます。 この設定は、3 つのオプションのうち最も安全ですが、 **拡張保護** をサポートしないオペレーティング システムからの接続では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続することができません。  
  
 **[承認された NTLM SPN]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが複数の NTLM サービス プリンシパル名 (SPN) で識別されると、ここに、SPN がセミコロンで区切られた一連の文字列として表示されます。 たとえば、値 **MSSQLSvc/HostName1.Contoso.com;MSSQLSvc/HostName2.Contoso.com**は、 **MSSQLSvc/HOST1.Contoso.com** および **MSSQLSvc/HOST2.Contoso.com** という名前の SPN への接続を試みているクライアントが許可されることを示します。 変数の最大長は 2048 文字です。  
  
## <a name="see-also"></a>参照  
 [Reporting Services での認証の拡張保護](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)  
  
  
