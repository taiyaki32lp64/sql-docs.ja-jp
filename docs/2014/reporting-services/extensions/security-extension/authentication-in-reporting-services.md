---
title: Reporting Services での認証 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- security [Reporting Services], authentication
- forms-based authentication [Reporting Services]
- authentication [Reporting Services]
- custom authentication [Reporting Services]
ms.assetid: 103ce1f9-31d8-44bb-b540-2752e4dcf60b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c4fc4d98eb32fb07def2fd317ebb7f5a6f6332cb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63282156"
---
# <a name="authentication-in-reporting-services"></a>Reporting Services での認証
  認証とは、ユーザーの本人性を立証するプロセスです。 ユーザー認証にはさまざまな方法がありますが、 最も一般的なのはユーザー パスワードを使用する方法です。 たとえば、フォーム認証を実装する場合は、ユーザーに対して資格情報の提示を要求し (通常は、ログイン名とパスワードを要求するインターフェイスを使用)、データベース テーブルや構成ファイルなどのデータ ストアと照合して、そのユーザーが本人かどうかを検証します。 資格情報の有効性を確認できない場合は、認証プロセスが失敗し、そのユーザーは匿名ユーザーであると見なされます。  
  
## <a name="custom-authentication-in-reporting-services"></a>Reporting Services でのカスタム認証  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] では、統合セキュリティを使用するか、またはユーザーの資格情報を明示的に受信して検証することによって、Windows オペレーティング システムがユーザー認証を実施します。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] では、カスタム認証を開発して追加の認証方法をサポートできます。 そのためには、セキュリティ拡張機能インターフェイス <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension> を使用します。 レポート サーバーであらゆる拡張機能を配置および使用できるように、すべての拡張機能が <xref:Microsoft.ReportingServices.Interfaces.IExtension> ベース インターフェイスから継承されます。 <xref:Microsoft.ReportingServices.Interfaces.IExtension> および <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension> は、<xref:Microsoft.ReportingServices.Interfaces> 名前空間のメンバーです。  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] では、レポート サーバーに対して認証を行うための主要な手段として、<xref:ReportService2010.ReportingService2010.LogonUser%2A> メソッドがあります。 Reporting Services Web サービスのこのメンバーを使用して、検証するユーザーの資格情報をレポート サーバーに渡すことができます。 基になる、セキュリティ拡張機能の実装**IAuthenticationExtension.LogonUser**カスタム認証コードが含まれています。 フォーム認証のサンプルでは、**LogonUser** が指定された資格情報とデータベースのカスタム ユーザー ストアを比較する認証チェックを実行します。 **LogonUser** の実装例は、次のようになります。  
  
```  
public bool LogonUser(string userName, string password, string authority)  
{  
   return AuthenticationUtilities.VerifyPassword(userName, password);  
}  
  
```  
  
 次のサンプル関数を使用して、指定された資格情報を検証します。  
  
```  
  
internal static bool VerifyPassword(string suppliedUserName,  
   string suppliedPassword)  
{   
   bool passwordMatch = false;  
   // Get the salt and pwd from the database based on the user name.  
   // See "How To: Use DPAPI (Machine Store) from ASP.NET," "How To:  
   // Use DPAPI (User Store) from Enterprise Services," and "How To:  
   // Create a DPAPI Library" for more information about how to use  
   // DPAPI to securely store connection strings.  
   SqlConnection conn = new SqlConnection(  
      "Server=localhost;" +   
      "Integrated Security=SSPI;" +  
      "database=UserAccounts");  
   SqlCommand cmd = new SqlCommand("LookupUser", conn);  
   cmd.CommandType = CommandType.StoredProcedure;  
  
   SqlParameter sqlParam = cmd.Parameters.Add("@userName",  
       SqlDbType.VarChar,  
       255);  
   sqlParam.Value = suppliedUserName;  
   try  
   {  
      conn.Open();  
      SqlDataReader reader = cmd.ExecuteReader();  
      reader.Read(); // Advance to the one and only row  
      // Return output parameters from returned data stream  
      string dbPasswordHash = reader.GetString(0);  
      string salt = reader.GetString(1);  
      reader.Close();  
      // Now take the salt and the password entered by the user  
      // and concatenate them together.  
      string passwordAndSalt = String.Concat(suppliedPassword, salt);  
      // Now hash them  
      string hashedPasswordAndSalt =  
         FormsAuthentication.HashPasswordForStoringInConfigFile(  
         passwordAndSalt,  
         "SHA1");  
      // Now verify them. Returns true if they are equal.  
      passwordMatch = hashedPasswordAndSalt.Equals(dbPasswordHash);  
   }  
   catch (Exception ex)  
   {  
       throw new Exception("Exception verifying password. " +  
          ex.Message);  
   }  
   finally  
   {  
       conn.Close();  
   }  
   return passwordMatch;  
}  
```  
  
## <a name="authentication-flow"></a>認証フロー  
 Reporting Services Web サービスには、レポート マネージャーとレポート サーバーによるフォーム認証を可能にするカスタム認証拡張機能が用意されています。  
  
 Reporting Services Web サービスの <xref:ReportService2010.ReportingService2010.LogonUser%2A> メソッドを使用して、認証する資格情報をレポート サーバーに送信します。 Web サービスは HTTP ヘッダーを使用して、検証されたログオン要求の認証チケット (クッキー) をサーバーからクライアントに渡します。  
  
 次の図は、レポート サーバーがカスタム認証拡張機能を使用するように構成されたアプリケーション配置における、Web サービスのユーザーを認証するメソッドを示しています。  
  
 ![Reporting Services のセキュリティ認証フロー](../../media/rosettasecurityextensionauthenticationflow.gif "Reporting Services のセキュリティ認証フロー")  
  
 図 2 が示すように、認証プロセスは次のようになります。  
  
1.  クライアント アプリケーションは、ユーザーを認証するために Web サービス メソッド <xref:ReportService2010.ReportingService2010.LogonUser%2A> を呼び出します。  
  
2.  Web サービスを呼び出すは、 <xref:ReportService2010.ReportingService2010.LogonUser%2A> 、セキュリティ拡張機能のメソッドを実装するクラスでは具体的には、 **IAuthenticationExtension**します。  
  
3.  <xref:ReportService2010.ReportingService2010.LogonUser%2A> の実装によって、ユーザー ストアまたはセキュリティ機関のユーザー名とパスワードが検証されます。  
  
4.  認証の完了後に、Web サービスがクッキーを作成し、セッション用にそれを管理します。  
  
5.  Web サービスは、HTTP ヘッダーの呼び出し元アプリケーションに認証チケットを返します。  
  
 Web サービスがセキュリティ拡張機能によってユーザーの認証を正常に完了すると、以降の要求に使用されるクッキーが生成されます。 クッキーをカスタム セキュリティ機関に保持することはできません。レポート サーバーがセキュリティ機関を所有していないためです。 クッキーは <xref:ReportService2010.ReportingService2010.LogonUser%2A> Web サービス メソッドから返され、以降の Web サービス メソッド呼び出しおよび URL アクセスに使用されます。  
  
> [!NOTE]  
>  転送時にクッキーが損傷しないよう、<xref:ReportService2010.ReportingService2010.LogonUser%2A> から返される認証クッキーの転送を Secure Sockets Layer (SSL) 暗号化を使用して保護する必要があります。  
  
 カスタム セキュリティ拡張機能をインストールした場合に URL アクセスによってレポート サーバーにアクセスすると、インターネット インフォメーション サービス (IIS) および [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] が認証チケットの転送を自動的に管理します。 OAP API によってレポート サーバーにアクセスする場合は、プロキシ クラスの実装に認証チケット管理用の追加サポートを含める必要があります。 SOAP API の使用および認証チケットの管理の詳細については、「カスタム セキュリティでの Web サービスの使用」を参照してください。  
  
## <a name="forms-authentication"></a>フォーム認証  
 フォーム認証は [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 認証の種類の 1 つであり、未認証ユーザーは HTML フォームにリダイレクトされます。 ユーザーが資格情報を入力すると、認証チケットを含むクッキーが発行されます。 以降の要求では、クッキーをチェックしてユーザーがレポート サーバーによって認証されているかどうかを確認します。  
  
 Reporting Services API から利用できるセキュリティ拡張機能インターフェイスを使用すると、フォーム認証をサポートするように [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] を拡張できます。 フォーム認証を使用するように [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] を拡張する場合は、レポート サーバーとのすべての通信に Secure Sockets Layer (SSL) を使用して、悪意のあるユーザーが別のユーザーのクッキーにアクセスすることを防止します。 SSL を使用した場合、クライアントとレポート サーバーが相互に認証でき、2 台のコンピューター間の通信内容を他のコンピューターから読み取ることができなくなります。 SSL 接続で送信されたすべてのデータが暗号化されるため、悪意のあるユーザーはレポート サーバーに送信されたパスワードやデータを傍受できません。  
  
 一般に、フォーム認証は、Windows 以外のプラットフォームでのアカウントおよび認証をサポートするために実装されます。 レポート サーバーへのアクセスを要求するユーザーにグラフィカル インターフェイスが表示され、入力した資格情報が認証のためにセキュリティ機関に送信されます。  
  
 フォーム認証では、ユーザーが資格情報を入力する必要があります。 Reporting Services Web サービスと直接通信する自動アプリケーションの場合は、フォーム認証とカスタム認証方法を併用する必要があります。  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] でフォーム認証が適しているのは、次のような場合です。  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows アカウントを持たないユーザーを格納および認証する必要がある場合。  
  
-   Web サイトの異なるページ間で、ログオン ページとしてユーザー インターフェイス フォームを提供する必要がある場合。  
  
 フォーム認証をサポートするカスタム セキュリティ拡張機能を記述する場合は、次のことを考慮してください。  
  
-   フォーム認証を使用する場合は、インターネット インフォメーション サービス (IIS) のレポート サーバー仮想ディレクトリで匿名アクセスを有効にする必要があります。  
  
-   [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 認証を Forms に設定する必要があります。 レポート サーバーの Web.config ファイルで [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 認証を構成してください。  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] では、Windows 認証またはカスタム認証を使用してユーザーを認証および承認できますが、両方を使用することはできません。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] では、複数のセキュリティ拡張機能を同時に使用できません。  
  
## <a name="see-also"></a>参照  
 [セキュリティ拡張機能の実装](../security-extension/implementing-a-security-extension.md)  
  
  
