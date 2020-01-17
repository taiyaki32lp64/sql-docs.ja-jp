---
title: カスタム アセンブリの配置 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- deploying custom assemblies [Reporting Services]
- custom assemblies [Reporting Services], deploying
- custom assemblies [Reporting Services], updating
- updating custom assemblies
ms.assetid: c6674cd8-0de7-4a5a-9e7c-12ffa49f6fd2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: abaa60d696975616631aea210c32bfcea63f6767
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63264730"
---
# <a name="deploying-a-custom-assembly"></a>カスタム アセンブリの配置
  カスタム アセンブリを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] に配置するには、レポート デザイナーとレポート サーバーの両方のアプリケーション フォルダーにアセンブリを入れます。 既定では、カスタム アセンブリには [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の `Execution` 権限が付与されます。 カスタム アセンブリに Execute アクセス許可よりも上位のアクセス許可を付与するには、レポート サーバーの rssrvpolicy.config 構成ファイルとレポート デザイナー プレビュー ウィンドウの rspreviewpolicy.config 構成ファイルを編集する必要があります。 または、グローバル アセンブリ キャッシュ (GAC) にカスタム アセンブリをインストールできます。  
  
> [!NOTE]  
>  レポート デザイナーには 2 種類のプレビュー モードがあります。1 つは [プレビュー] タブ。もう 1 つは、レポート プロジェクトを `DebugLocal` モードで開始したときに起動されるポップアップ プレビュー ウィンドウです。 [プレビュー] タブでは、`FullTrust` 権限セットを使用してすべてのレポート式を実行します。セキュリティ ポリシー設定は適用しません。 レポート サーバー機能のシミュレーションを目的としているプレビュー ウィンドウには、ポリシー構成ファイルが備わっています。レポート デザイナーでカスタム アセンブリを使用する場合、ユーザーまたは管理者はこの構成ファイルを変更する必要があります。 また、このポップアップ プレビュー ウィンドウでは、カスタム アセンブリがロックされます。 したがって、カスタム アセンブリ コードを変更または更新するには、プレビュー ウィンドウを閉じる必要があります。  
  
###### <a name="to-deploy-a-custom-assembly-in-reporting-services"></a>カスタム アセンブリを Reporting Services に配置するには  
  
1.  カスタム アセンブリを構築場所からレポート サーバーの bin フォルダーまたはレポート デザイナーのフォルダーにコピーします。 レポート サーバーの bin フォルダーの既定の場所は、%ProgramFiles%\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin です。 レポート デザイナー フォルダーの既定の場所は、%ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies です。  
  
     カスタム アセンブリをレポート サーバーの bin フォルダーに配置した場合は、このカスタム アセンブリを参照するレポートをパブリッシュできます。レポート デザイナー フォルダーに配置した場合は、このカスタム アセンブリを参照するレポートをレポート デザイナーで実行およびデバッグできます。  
  
     カスタム アセンブリ コードに既定の実行権限よりも上位の権限を付与するには、次の操作を行います。  
  
2.  適切な構成ファイルを開きます。 rssrvpolicy.config の既定の場所は、%ProgramFiles%\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer です。 rspreviewpolicy.config の既定の場所は、%ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies です。  
  
3.  カスタム アセンブリのコード グループを追加します。 詳細については、「[セキュリティで保護された配置 &#40;Reporting Services&#41;](../extensions/secure-development/secure-development-reporting-services.md)」を参照してください。  
  
## <a name="updating-custom-assemblies"></a>カスタム アセンブリの更新  
 ある時点では、パブリッシュされた複数のレポートが参照するカスタム アセンブリのバージョンの更新が必要なことがあります。 このようなアセンブリがレポート サーバーまたはレポート デザイナーの bin ディレクトリに既に存在し、アセンブリのバージョン番号が何らかの方法で増加するか変わった場合は、現在パブリッシュされているレポートが適切に機能しなくなります。 レポート定義の `CodeModules` 要素で参照されているアセンブリのバージョンを更新し、レポートを再度パブリッシュする必要があります。 カスタム アセンブリを頻繁に更新することがあらかじめわかっていて、現在パブリッシュされているレポートが新しいアセンブリを参照する必要がある場合は、特定のアセンブリのすべての更新に同じバージョン番号を使用することを検討してください。  
  
 現在パブリッシュされているレポートがアセンブリの新バージョンを参照する必要がない場合は、カスタム アセンブリをグローバル アセンブリ キャッシュに配置できます。 グローバル アセンブリ キャッシュは同じアセンブリのバージョンを複数保持できるため、現在のレポートがアセンブリの旧バージョンを参照し、新しくパブリッシュされたレポートが更新されたアセンブリを参照できます。 別の方法として、レポート サーバーのリダイレクトのバインドを設定し、旧アセンブリの全要求を新しいアセンブリに強制的にリダイレクトすることもできます。 レポート サーバーの Web.config ファイルとレポート サーバーの ReportService.exe.config ファイルを変更する必要があります。 エントリは、次のようになります。  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
            <bindingRedirect oldVersion="1.0.0.0"  
                             newVersion="2.0.0.0"/>  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>参照  
 [レポートでのカスタム アセンブリの使用](using-custom-assemblies-with-reports.md)   
 [アセンブリとグローバル アセンブリ キャッシュの使用](https://go.microsoft.com/fwlink/?LinkId=63912)  
  
  
