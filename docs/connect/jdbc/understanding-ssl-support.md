---
title: 暗号化のサポートについて |Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: vanto
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 073f3b9e-8edd-4815-88ea-de0655d0325e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5ec3ad142e3dc5e2945afebeb2c9a6c97350672c
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71713297"
---
# <a name="understanding-encryption-support"></a>暗号化のサポートについて

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続する際、アプリケーションによって暗号化が要求され、なおかつ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスで TLS 暗号化がサポートされる構成になっていた場合、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] では TLS ハンドシェイクが開始されます。 サーバーとクライアントは、このハンドシェイクによって、データの保護に使用する暗号化と暗号アルゴリズムをネゴシエートします。 TLS ハンドシェイクが完了すると、暗号化されたデータを安全に送信できるようになります。 サーバーでは、TLS ハンドシェイクの際にクライアントに公開キー証明書が送信されます。 公開キー証明書の発行者は証明機関 (CA) と呼ばれます。 その証明機関が、クライアントが信頼するいずれかの証明機関に該当するかどうかは、クライアント側で検証する必要があります。  
  
アプリケーションから暗号化を要求されなかった場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、TLS 暗号化をサポートするよう [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] によって強制されることはありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスが TLS 暗号化を強制的に使用するように構成されていない場合、接続は暗号化なしで確立されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスが TLS 暗号化を強制的に使用するように構成されている場合は、使用中の Java 仮想マシン (JVM) が正常に構成されていれば自動的に TLS 暗号化が有効になり、そうでなければ接続が終了してエラーが生成されます。  
  
> [!NOTE]  
> TLS 接続に成功するためには、**serverName** に渡された値が、サーバー証明書に含まれる Subject Alternate Name (SAN) の Common Name (CN) または DNS 名と厳密に一致している必要があります。  
>
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の TLS を構成する方法の詳細については、「[データベースエンジンへの暗号化接続の有効化](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
## <a name="remarks"></a>Remarks

TLS 暗号化をアプリケーションで使用できるようにするために、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] のバージョン 1.2 リリース以降では、**encrypt**、**trustServerCertificate**、**trustStore**、**trustStorePassword**、**hostNameInCertificate** の各接続プロパティが導入されました。 詳細については、「[接続プロパティの設定](../../connect/jdbc/setting-the-connection-properties.md)」を参照してください。  
  
 次の表は、想定される TLS 接続シナリオでの [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] バージョンの動作をまとめたものです。 使用する TLS 接続プロパティの組み合わせをシナリオごとに変えています。 表の値の意味を以下に示します。  
  
- **blank**: "接続文字列にプロパティが存在しない"  
  
- **value**: "接続文字列にプロパティが存在し、その値が有効である"  
  
- **any**: "接続文字列にプロパティが存在するかどうか、またはその値が有効であるかどうかは関係ない"  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザー認証でも Windows 統合認証でも同じ動作になります。  
  
| encrypt        | trustServerCertificate | hostNameInCertificate | trustStore | trustStorePassword | 動作                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| -------------- | ---------------------- | --------------------- | ---------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| false または blank | any                    | any                   | any        | any                | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] によって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は TLS 暗号化のサポートを強制されません。 サーバーに自己署名証明書が存在する場合、その TLS 証明書の交換がドライバーによって開始されます。 TLS 証明書の検証は行われず、(ログイン パケット内の) 資格情報のみが暗号化されます。<br /><br /> サーバーによってクライアントに TLS 暗号化のサポートが要求されている場合は、TLS 証明書の交換が開始されます。 TLS 証明書の検証は行われませんが、通信全体が暗号化されます。                                                                                                                                                                                    |
| true           | true                   | any                   | any        | any                | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] によって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に TLS 暗号化を使用するよう要求されます。<br /><br /> サーバーによってクライアントに TLS 暗号化のサポートが要求されている場合、またはサーバーで暗号化がサポートされている場合、ドライバーによって TLS 証明書の交換が開始されます。 **trustServerCertificate** プロパティが "true" に設定されている場合は TLS 証明書の検証が行われないことに注意してください。<br /><br /> サーバーが暗号化をサポートするように構成されていない場合、ドライバーはエラーを生成して接続を終了します。                                                                                                                                                                                          |
| true           | false または blank         | blank                 | blank      | blank              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] によって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に TLS 暗号化を使用するよう要求されます。<br /><br /> サーバーによってクライアントに TLS 暗号化のサポートが要求されている場合、またはサーバーで暗号化がサポートされている場合、ドライバーによって TLS 証明書の交換が開始されます。<br /><br /> ドライバーにより、接続 URL に指定されている **serverName** プロパティを使用してサーバーの TLS 証明書が検証され、信頼マネージャー ファクトリの検索ルールに従って、使用する証明書ストアが決定されます。<br /><br /> サーバーが暗号化をサポートするように構成されていない場合、ドライバーはエラーを生成して接続を終了します。                                                                             |
| true           | false または blank         | value                 | blank      | blank              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] によって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に TLS 暗号化を使用するよう要求されます。<br /><br /> サーバーによってクライアントに TLS 暗号化のサポートが要求されている場合、またはサーバーで暗号化がサポートされている場合、ドライバーによって TLS 証明書の交換が開始されます。<br /><br /> ドライバーにより、**hostNameInCertificate** プロパティに指定されている値を使用して、TLS 証明書のサブジェクトの値が検証されます。<br /><br /> サーバーが暗号化をサポートするように構成されていない場合、ドライバーはエラーを生成して接続を終了します。                                                                                                                                                                 |
| true           | false または blank         | blank                 | value      | value              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] によって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に TLS 暗号化を使用するよう要求されます。<br /><br /> サーバーによってクライアントに TLS 暗号化のサポートが要求されている場合、またはサーバーで暗号化がサポートされている場合、ドライバーによって TLS 証明書の交換が開始されます。<br /><br /> ドライバーは、**trustStore** プロパティの値を使用して証明書の trustStore ファイルを検索し、**trustStorePassword** プロパティの値を使用して trustStore ファイルの整合性をチェックします。<br /><br /> サーバーが暗号化をサポートするように構成されていない場合、ドライバーはエラーを生成して接続を終了します。                                                                                                                |
| true           | false または blank         | blank                 | blank      | value              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] によって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に TLS 暗号化を使用するよう要求されます。<br /><br /> サーバーによってクライアントに TLS 暗号化のサポートが要求されている場合、またはサーバーで暗号化がサポートされている場合、ドライバーによって TLS 証明書の交換が開始されます。<br /><br /> ドライバーは、**trustStorePassword** プロパティの値を使用して、既定の trustStore ファイルの整合性をチェックします。<br /><br /> サーバーが暗号化をサポートするように構成されていない場合、ドライバーはエラーを生成して接続を終了します。                                                                                                                                                                                  |
| true           | false または blank         | blank                 | value      | blank              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] によって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に TLS 暗号化を使用するよう要求されます。<br /><br /> サーバーによってクライアントに TLS 暗号化のサポートが要求されている場合、またはサーバーで暗号化がサポートされている場合、ドライバーによって TLS 証明書の交換が開始されます。<br /><br /> ドライバーは、**trustStore** プロパティの値を使用して、trustStore ファイルの場所を調べます。<br /><br /> サーバーが暗号化をサポートするように構成されていない場合、ドライバーはエラーを生成して接続を終了します。                                                                                                                                                                                                 |
| true           | false または blank         | value                 | blank      | value              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] によって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に TLS 暗号化を使用するよう要求されます。<br /><br /> サーバーによってクライアントに TLS 暗号化のサポートが要求されている場合、またはサーバーで暗号化がサポートされている場合、ドライバーによって TLS 証明書の交換が開始されます。<br /><br /> ドライバーは、**trustStorePassword** プロパティの値を使用して、既定の trustStore ファイルの整合性をチェックします。 また、**hostNameInCertificate** プロパティの値を使用して、TLS 証明書が検証されます。<br /><br /> サーバーが暗号化をサポートするように構成されていない場合、ドライバーはエラーを生成して接続を終了します。                                                                   |
| true           | false または blank         | value                 | value      | blank              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] によって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に TLS 暗号化を使用するよう要求されます。<br /><br /> サーバーによってクライアントに TLS 暗号化のサポートが要求されている場合、またはサーバーで暗号化がサポートされている場合、ドライバーによって TLS 証明書の交換が開始されます。<br /><br /> ドライバーは、**trustStore** プロパティの値を使用して、trustStore ファイルの場所を調べます。 また、**hostNameInCertificate** プロパティの値を使用して、TLS 証明書が検証されます。<br /><br /> サーバーが暗号化をサポートするように構成されていない場合、ドライバーはエラーを生成して接続を終了します。                                                                                  |
| true           | false または blank         | value                 | value      | value              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] によって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に TLS 暗号化を使用するよう要求されます。<br /><br /> サーバーによってクライアントに TLS 暗号化のサポートが要求されている場合、またはサーバーで暗号化がサポートされている場合、ドライバーによって TLS 証明書の交換が開始されます。<br /><br /> ドライバーは、**trustStore** プロパティの値を使用して証明書の trustStore ファイルを検索し、**trustStorePassword** プロパティの値を使用して trustStore ファイルの整合性をチェックします。 また、**hostNameInCertificate** プロパティの値を使用して、TLS 証明書が検証されます。<br /><br /> サーバーが暗号化をサポートするように構成されていない場合、ドライバーはエラーを生成して接続を終了します。 |
  
encrypt プロパティが **true** に設定されている場合、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] では、JVM の既定の JSSE セキュリティ プロバイダーを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と TLS 暗号化がネゴシエートされます。 既定のセキュリティ プロバイダーでは、TLS 暗号化の正常なネゴシエートに必要なすべての機能がサポートされているとは限りません。 たとえば、既定のセキュリティ プロバイダーでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の TLS 証明書で使用されている RSA 公開キーのサイズがサポートされていない場合があります。 この場合、既定のセキュリティ プロバイダーでエラーが発生し、その結果 JDBC ドライバーが接続を終了する可能性があります。 この問題を解決するには、次のいずれかを実行します。  
  
- サイズの小さい RSA 公開キーを持つサーバー証明書を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を構成します。  
  
- "\<java-home>/lib/security/java.security" セキュリティ プロパティ ファイルで、別の JSSE セキュリティ プロバイダーを使用するように JVM を構成します。  
  
- 別の JVM を使用します。  
  
## <a name="validating-server-tls-certificate"></a>サーバー TLS 証明書を検証しています  

サーバーでは、TLS ハンドシェイクの際にクライアントに公開キー証明書が送信されます。 そのサーバー証明書が、クライアントが信頼している証明機関によって発行されているかどうかを、JDBC ドライバーまたはクライアントが検証する必要があります。 ドライバーは、サーバー証明書で次の条件が満たされている状態を必要とします。  
  
- 信頼されている証明機関から発行されている。  
  
- サーバー認証用に証明書が発行されている。  
  
- 証明書の有効期限が切れていない。  
  
- 証明書の Subject の Common Name (CN) または Subject Alternate Name (SAN) の DNS 名が、接続文字列に指定された **serverName** の値 (または **hostNameInCertificate** プロパティの値が指定されている場合はその値) と厳密に一致している。  
  
- DNS 名にはワイルドカード文字を含めることができます。 ただし、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] では、ワイルドカードでのマッチングがサポートされません。 つまり、abc.com は \*.com とは一致せず、\*.com は \*.com と一致します。  
  
## <a name="see-also"></a>参照

[暗号化の使用](../../connect/jdbc/using-ssl-encryption.md)

[JDBC ドライバー アプリケーションのセキュリティ保護](../../connect/jdbc/securing-jdbc-driver-applications.md)  
