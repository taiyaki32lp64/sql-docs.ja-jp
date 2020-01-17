---
title: 統合を構成するサービスのサービス (SSIS サービス) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services service, configuring
- configuration files [Integration Services]
- service [Integration Services], configuring
- default configuration files
ms.assetid: 36d78393-a54c-44b0-8709-7f003f44c27f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 600858e3d7b2ea29a30541c559aa764b4085f7cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060496"
---
# <a name="configuring-the-integration-services-service-ssis-service"></a>Integration Services サービスの構成 (SSIS サービス)
    
> [!IMPORTANT]  
>  このトピックでは、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを管理するための Windows サービスである [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスについて説明します。 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] では、以前のリリースの [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]との互換性を維持するために、このサービスをサポートしています。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]以降では、Integration Services サーバー上のパッケージなどのオブジェクトを管理できます。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスの設定は、構成ファイルに基づきます。 既定では、この構成ファイルの名前は msdtssrvr.ini.xml ですと、ファイルは %ProgramFiles%\Microsoft SQL server \120\dts\binn、フォルダーにあります。  
  
 通常は、この構成ファイルに変更を加える必要も、この構成ファイルの既定の場所を変更する必要もありません。 ただし、パッケージが [!INCLUDE[ssDE](../includes/ssde-md.md)]の名前付きインスタンスまたはリモート インスタンス、あるいは [!INCLUDE[ssDE](../includes/ssde-md.md)]の複数のインスタンスに格納されている場合は、構成ファイルを変更する必要があります。 また、構成ファイルを既定の場所とは別の場所に移動する場合は、ファイルの場所を指定するレジストリ キーを変更する必要があります。  
  
## <a name="configuration-file-contents"></a>構成ファイルの内容  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]をインストールすると、セットアップ プロセスによって [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスの構成ファイルが作成およびインストールされます。 この構成ファイルには、次の設定が含まれます。  
  
-   サービスが停止すると、パッケージに中止コマンドが送信されます。  
  
-   [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のオブジェクト エクスプローラー内の [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] に表示するルート フォルダーは、[MSDB] および [ファイル システム] フォルダーです。  
  
-   ファイル システム内のパッケージを[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]サービス管理 %ProgramFiles%\Microsoft SQL Server\120\DTS\Packages にあります。  
  
 この構成ファイルは、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスが管理するパッケージを含む msdb データベースも指定します。 既定では、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスは、 [!INCLUDE[ssDE](../includes/ssde-md.md)] と同時にインストールされる [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]のインスタンスの msdb データベース内にあるパッケージを管理するように構成されます。 [!INCLUDE[ssDE](../includes/ssde-md.md)] のインスタンスが同時にインストールされない場合、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスは、 [!INCLUDE[ssDE](../includes/ssde-md.md)]のローカルの既定インスタンスの msdb データベース内にあるパッケージを管理するように構成されます。  
  
### <a name="default-configuration-file-example"></a>既定の構成ファイルの例  
 次の設定を含む既定の構成ファイルを以下の例に示します。  
  
-   [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスが停止すると、パッケージは実行を停止します。  
  
-   [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 内のパッケージ ストレージのルート フォルダーは、[MSDB] および [ファイル システム] フォルダーです。  
  
-   このサービスは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のローカルの既定インスタンスの msdb データベースに格納されるパッケージを管理します。  
  
-   このサービスは、ファイル システムの [パッケージ] フォルダーに格納されるパッケージを管理します。  
  
 **既定の構成ファイルの例**  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    <Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>.</ServerName>  
    </Folder>  
    <Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
## <a name="modification-of-the-configuration-file"></a>構成ファイルの変更  
 構成ファイルを変更することによって、サービスが停止した場合にパッケージを継続して実行できるようにしたり、オブジェクト エクスプローラー内に別のルート フォルダーを表示したり、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスが管理するファイル システム内に別のフォルダーまたは追加のフォルダーを指定することができます。 たとえば、`SqlServerFolder` 型の別のルート フォルダーを作成して、[!INCLUDE[ssDE](../includes/ssde-md.md)]の追加インスタンスの msdb データベースでパッケージを管理できます。  
  
> [!NOTE]  
>  一部の文字は、フォルダー名には無効です。 フォルダー名として有効な文字は、 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] クラスの **System.IO.Path** および **GetInvalidFilenameChars** フィールドによって決まります。 **GetInvalidFilenameChars** フィールドでは、 **Path** クラスのメンバーに渡されるパス文字列引数に指定できない、プラットフォーム固有の文字配列が指定されます。 無効な文字のセットは、ファイル システムによって異なる場合があります。 通常、無効な文字は、引用符 (")、小なり (<) 文字、およびパイプ (|) 文字です。  
  
 ただし、[!INCLUDE[ssDE](../includes/ssde-md.md)]の名前付きインスタンスまたはリモート インスタンスに格納されているパッケージを管理するには、構成ファイルを変更する必要があります。 構成ファイルを更新しないと、 **で** オブジェクト エクスプローラー [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を使用して名前付きインスタンスまたはリモート インスタンス上の msdb データベースに格納されているパッケージを表示することはできません。 **オブジェクト エクスプローラー** を使用してこのようなパッケージを表示しようとすると、次のエラー メッセージが返されます。  
  
 `Failed to retrieve data for this request. (Microsoft.SqlServer.SmoEnum)`  
  
 `The SQL Server specified in Integration Services service configuration is not present or is not available. This might occur when there is no default instance of SQL Server on the computer. For more information, see the topic "Configuring the Integration Services Service" in SQL Server 2008 Books Online.`  
  
 `Login Timeout Expired`  
  
 `An error has occurred while establishing a connection to the server. When connecting to SQL Server 2008, this failure may be caused by the fact that under the default settings SQL Server does not allow remote connections.`  
  
 `Named Pipes Provider: Could not open a connection to SQL Server [2]. (MsDtsSvr).`  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスの構成ファイルを変更するには、テキスト エディターを使用します。  
  
> [!IMPORTANT]  
>  サービス構成ファイルを変更したら、更新されたサービス構成を使用するためにサービスを再起動する必要があります。  
  
### <a name="modified-configuration-file-example"></a>変更された構成ファイルの例  
 変更された [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]の構成ファイルの例を次に示します。 このファイルは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] という名前のサーバー上で、 `InstanceName` と呼ばれる `ServerName`の名前付きインスタンス用のファイルです。  
  
 **SQL Server の名前付きインスタンス用構成ファイルの変更例**  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    <Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>ServerName\InstanceName</ServerName>  
    </Folder>  
    <Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
## <a name="modification-of-the-configuration-file-location"></a>構成ファイルの場所の変更  
レジストリ キー **hkey_local_machine \software\microsoft\microsoft SQL Server\120\SSIS\ServiceConfigFile**するファイルの場所と、構成の名前を指定します。[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]サービスで使用します。 レジストリ キーの既定値は**C:\Program files \microsoft SQL Server\120\DTS\Binn\MsDtsSrvr.ini.xml**します。 レジストリ キーの値を更新すると、構成ファイルに別の名前と場所を使用することができます。 パスにバージョン番号 (SQL Server の 120 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)]) は SQL Server のバージョンによって異なります。 
  
  
> [!CAUTION]  
>  レジストリの編集を誤ると、深刻な問題が発生し、オペレーティング システムの再インストールが必要になる場合があります。 [!INCLUDE[msCoName](../includes/msconame-md.md)] レジストリの誤った編集により発生した問題に関しては、一切責任を負わないものとします。 レジストリを編集する前に、重要なデータをすべてバックアップしてください。 レジストリのバックアップ、復元、および編集の方法については、 [!INCLUDE[msCoName](../includes/msconame-md.md)] サポート技術情報の記事「 [Microsoft Windows レジストリの説明](https://support.microsoft.com/kb/256986)」を参照してください。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスは、サービスの開始時に構成ファイルを読み込みます。 レジストリ エントリを変更した場合、サービスを再起動する必要があります。  
  
  
