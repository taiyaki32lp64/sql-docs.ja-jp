---
title: SQL Server Native Client のインストール |Microsoft Docs
ms.custom: ''
ms.date: 07/15/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
author: MightyPen
ms.author: genemi
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 677450c306cdd85f3fec34b09ab8da9b45181844
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73788448"
---
# <a name="installing-sql-server-native-client"></a>SQL Server Native Client のインストール
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]


  [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)]をインストールすると、Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 がインストールされます。 
 
 SQL Server 2016 Native Client がありません。 詳細については、「 [SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client.md)」を参照してください。 
 
SQL Server 2012 Feature Pack web ページから sqlncli を取得することもできます。 最新バージョンの SQL Server Native Client をダウンロードするには、 [Microsoft® SQL Server® 2012 Feature Pack](https://www.microsoft.com/download/confirmation.aspx?id=29065)」を参照してください。 SQL Server 2012 より前の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client がコンピューターにもインストールされている場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 は以前のバージョンとサイドバイサイドでインストールされます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client のファイル (sqlncli11.dll、sqlnclir11.rll、および s11ch_sqlncli.chm) は、次の場所にインストールされます。  
  
 `%SYSTEMROOT%\system32\`  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーと [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーのすべてのレジストリ設定は、インストール処理の一環として適切に行われます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ヘッダー ファイルとライブラリ ファイル (sqlncli.h と sqlncli11.lib) は、次の場所にインストールされます。  
  
 `%PROGRAMFILES%\Microsoft SQL Server\110\SDK`  
  
 インストールするだけでなく[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ネイティブ クライアントの一環として、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インストールもには、sqlncli.msi をという名前の再頒布可能パッケージのインストール プログラムがある、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]次の場所にインストール ディスク`%CD%\Setup\`。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は、sqlncli.msi を使用して配布できます。 アプリケーションを配置する場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client をインストールする必要があります。 チェイナーとブートストラップのテクノロジを使用すると、ユーザーが 1 回のインストール手順に従うだけで複数のパッケージをまとめてインストールできるようになります。 詳細については、「[Visual Studio 2005 用のカスタム ブートストラップ パッケージの作成](https://go.microsoft.com/fwlink/?LinkId=115667)」および「[カスタムの必須コンポーネントの追加](https://go.microsoft.com/fwlink/?LinkId=115668)」をご覧ください。  
  
 x64 バージョンと Itanium バージョンの sqlncli.msi では、32 ビット バージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client もインストールされます。 アプリケーションが、開発時に使用したものとは異なるプラットフォームを対象としている場合、Microsoft ダウンロード センターから x64、Itanium、および x86 用のバージョンの sqlncli.msi をダウンロードできます。  
  
 sqlncli.msi を呼び出すと、既定ではクライアント コンポーネントだけがインストールされます。 クライアントコンポーネントは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client を使用して開発されたアプリケーションの実行をサポートするファイルです。 SDK コンポーネントもインストールするには、コマンド ラインで `ADDLOCAL=All` を指定します。 例 :  
  
 `msiexec /i sqlncli.msi ADDLOCAL=ALL APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
## <a name="silent-install"></a>サイレント インストール  
 msiexec で /passive、/qn、/qb、または /qr オプションを指定する場合、IACCEPTSQLNCLILICENSETERMS=YES も指定して、使用許諾契約の条件に同意することを明示的に指定する必要があります。 このオプションは、すべて大文字で指定する必要があります。  
  
## <a name="uninstalling-sql-server-native-client"></a>SQL Server Native Client のアンインストール  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] server や [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ツールなどのアプリケーションは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client に依存しているため、すべての依存アプリケーションがアンインストールされるまで、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client をアンインストールしないことが重要です。 アプリケーションがネイティブクライアント [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に依存していることを警告する警告をユーザーに提供するには、次のように MSI で APPGUID インストールオプションを使用します。  
  
 `msiexec /i sqlncli.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
 APPGUID に渡す値は、特定の製品コードです。 Microsoft インストーラーを使用してアプリケーションのセットアップ プログラムをバンドルするときは、製品コードを作成する必要があります。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client  を使用したアプリケーションの構築](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [インストール方法に関するトピック](https://msdn.microsoft.com/library/59de41e7-557f-462a-8914-53ec35496baa)  
  
  
