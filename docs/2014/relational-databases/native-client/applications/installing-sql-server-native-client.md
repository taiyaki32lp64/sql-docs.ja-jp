---
title: SQL Server Native Client のインストール |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, uninstalling
- SQLNCLI, installing
- SQLNCLI, uninstalling
- Setup [SQL Server Native Client]
- uninstalling SQL Server Native Client
- data access [SQL Server Native Client], uninstalling SQL Server Native Client
- installing SQL Server Native Client
- SQL Server Native Client, installing
- data access [SQL Server Native Client], installing SQL Server Native Client
- removing SQL Server Native Client
ms.assetid: c6abeab2-0052-49c9-be79-cfbc50bff5c1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f832c4b55c8a039de440b08e6d2ed3350175e2a6
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75231810"
---
# <a name="installing-sql-server-native-client"></a>SQL Server Native Client のインストール
  Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 は、のインストール[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]時にインストールされます。 
  [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Native Client は存在しません。 詳細については、「 [SQL Server Native Client の新機能](../sql-server-native-client.md)」を参照してください。 SQL Server 2012 Feature Pack web ページから sqlncli を取得することもできます。 SQL Server Native Client の最新バージョンをダウンロードするには、Microsoft にアクセスしてください。 [SQL Server。。2012 SP2 Feature Pack](https://www.microsoft.com/download/details.aspx?id=43339)。 SQL Server 2012 より前のバージョン[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の native client もコンピューターにインストールされている場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] native client 11.0 は以前のバージョンとサイドバイサイドでインストールされます。  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client のファイル (sqlncli11.dll、sqlnclir11.rll、および s11ch_sqlncli.chm) は、次の場所にインストールされます。  
  
 `%SYSTEMROOT%\system32\`  
  
> [!NOTE]  
>  
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーと [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーのすべてのレジストリ設定は、インストール処理の一環として適切に行われます。  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ヘッダー ファイルとライブラリ ファイル (sqlncli.h と sqlncli11.lib) は、次の場所にインストールされます。  
  
 `%PROGRAMFILES%\Microsoft SQL Server\110\SDK`  
  
 Native [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client を[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インストールの一部としてインストールすることに加えて、sqlncli という再配布可能なインストールプログラムもあります。これ[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]は、のインストールディスクにあり`%CD%\Setup\`ます。  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は、sqlncli.msi を使用して配布できます。 アプリケーションを配置する場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client をインストールする必要があります。 チェイナーとブートストラップのテクノロジを使用すると、ユーザーが 1 回のインストール手順に従うだけで複数のパッケージをまとめてインストールできるようになります。 詳細については、「[Visual Studio 2005 用のカスタム ブートストラップ パッケージの作成](https://go.microsoft.com/fwlink/?LinkId=115667)」および「[カスタムの必須コンポーネントの追加](https://go.microsoft.com/fwlink/?LinkId=115668)」をご覧ください。  
  
 x64 バージョンと Itanium バージョンの sqlncli.msi では、32 ビット バージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client もインストールされます。 アプリケーションが、開発時に使用したものとは異なるプラットフォームを対象としている場合、Microsoft ダウンロード センターから x64、Itanium、および x86 用のバージョンの sqlncli.msi をダウンロードできます。  
  
 sqlncli.msi を呼び出すと、既定ではクライアント コンポーネントだけがインストールされます。 クライアントコンポーネントは、Native Client を使用して[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]開発されたアプリケーションの実行をサポートするファイルです。 SDK コンポーネントもインストールするには、コマンド ラインで `ADDLOCAL=All` を指定します。 例:  
  
 `msiexec /i sqlncli.msi ADDLOCAL=ALL APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
## <a name="silent-install"></a>サイレント インストール  
 msiexec で /passive、/qn、/qb、または /qr オプションを指定する場合、IACCEPTSQLNCLILICENSETERMS=YES も指定して、使用許諾契約の条件に同意することを明示的に指定する必要があります。 このオプションは、すべて大文字で指定する必要があります。  
  
## <a name="uninstalling-sql-server-native-client"></a>SQL Server Native Client のアンインストール  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]サーバーや[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ツールなどのアプリケーションは、native client [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]に依存しているため、すべての[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]依存アプリケーションがアンインストールされるまでは、native client をアンインストールしないことが重要です。 アプリケーションが Native Client に[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]依存しているという警告がユーザーに提供されるようにするには、次のように MSI で appguid インストールオプションを使用します。  
  
 `msiexec /i sqlncli.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
 APPGUID に渡す値は、特定の製品コードです。 Microsoft インストーラーを使用してアプリケーションのセットアップ プログラムをバンドルするときは、製品コードを作成する必要があります。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client を使用したアプリケーションの構築](installing-sql-server-native-client.md)   
 [インストール方法に関するトピック](../../../sql-server/install/installation-how-to-topics.md)  
  
  
