---
title: コマンド プロンプトでの Reporting Services SharePoint モードとネイティブ モードのインストール |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 048169b3-512c-41e4-895a-0416eff41268
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fc1e5ae5d17d45b937a5dd44ab3ea6fe5f8620eb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108775"
---
# <a name="command-prompt-installation-of-reporting-services-sharepoint-mode-and-native-mode"></a>Reporting Services のコマンド プロンプト インストール (SharePoint モードとネイティブ モード)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は、SQL Server セットアップ プログラムからのコマンド ライン インストールをサポートしています。 このトピックでは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]用のコマンド ラインからのインストール例をいくつか示します。 すべての SQL Server コンポーネントで使用できるコマンド ライン オプションの詳細については、次を参照してください。[コマンド プロンプトから SQL Server 2014 のインストール](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)します。 このトピックでは、SharePoint 製品用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインのコマンド ライン オプションについては説明していません。 アドインのコマンド インストールについては、「[rsSharePoint.msi インストール ファイルを使用したアドインのインストール](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md#bkmk_install_rssharepoint)」をご覧ください。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モード | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード  
  
## <a name="rsinstallmode-native-mode"></a>RSINSTALLMODE (ネイティブ モード)  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をインストールするための主な入力設定は、 **/RSINSTALLMODE** の入力設定です。 設定では、2 つのオプションがあります。**DefaultNativeMode**と**filesonlymode になります**  
  
 インストールに SQL Server データベース エンジンが含まれている場合、既定の RSINSTALLMODE は DefaultNativeMode です。インストールに SQL Server データベース エンジンが含まれていない場合、既定の RSINSTALLMODE は FilesOnlyMode です。インストールに SQL Server データベース エンジンが含まれていない場合に DefaultNativeMode を選択すると、そのインストールでは自動的に RSINSTALLMODE が FilesOnlyMode に変更されます。 入力の設定の詳細については、次を参照してください。[コマンド プロンプトから SQL Server 2014 のインストール](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)します。  
  
## <a name="rsshpinstallmode-sharepoint-mode"></a>RSSHPINSTALLMODE (SharePoint モード)  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を SharePoint モードでインストールするための入力設定は、 **/RSSHPINSTALLMODE**です。 入力の設定では、1 つのオプションがあります。SharePointFilesOnlyMode です。 このオプションにより、SharePoint モードに必要なすべてのファイルがインストールされますが、インストール後に構成が必要です。 追加の構成の手順は、SharePoint サーバーの全体管理を使用して行います。 詳細については、次を参照してください。 [Install Reporting Services SharePoint Mode for SharePoint 2010](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)します。  
  
## <a name="examples-of-sharepoint-mode-installation"></a>SharePoint モード インストールの例  
 次の例は、SQL Server のデータベース エンジン サービス、SharePoint モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 、および SharePoint 用の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドイン (RS_SHPWFE) をインストールします。  
  
```  
setup /q /ACTION=install /FEATURES=SQL, RS_SHP, RS_SHPWFE,TOOLS /INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /SQLSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /AGTSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE"  
```  
  
 次の例は、SharePoint モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のみをインストールします。  
  
```  
Setup.exe /q /ACTION="Install" /IACCEPTSQLSERVERLICENSETERMS /FEATURES="RS_SHP" /INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" /INSTALLSQLDATADIR="C:\Program Files\Microsoft SQL Server" /SECURITYMODE="SQL" /SAPWD="*****" /PID="[Your PID Value]" /SQLSYSADMINACCOUNTS="[Account Name]" "AutoSql Admin Group" /ASSYSADMINACCOUNTS="[Account Name]" /UPDATEENABLED="False"  
  
```  
  
 次の例は、すべての SQL Server 機能 (ネイティブ モードと SharePoint モードの両方の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を含む) をインストールします。  
  
```  
Setup.exe /q /ACTION="Install" /INSTANCENAME="MSSQLSERVER" /FEATURES="SQLEngine,Replication,SNAC,SNAC_SDK,Browser,Writer,AS,IS,MDS,Adv_SSMS,BC,BOL,Conn,SDK,DReplay_CTLR,DReplay_CLT, RS_SHP,RS_SHPWFE,DQC,BIDS,FullText, RS,DQ,SSMS" /INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" /INSTALLSQLDATADIR="C:\Program Files\Microsoft SQL Server" /SQLSVCACCOUNT="[Account Name]" /SQLSVCPASSWORD="********" /AGTSVCACCOUNT="[Account Nam]" /AGTSVCPASSWORD="********" /CTLRSVCACCOUNT="[Account Nam]" /CTLRSVCPASSWORD="********" /CLTSVCACCOUNT="[Account Nam]" /CLTSVCPASSWORD="********" /ASSVCACCOUNT="[Account Nam]" /ASSVCPASSWORD="********" /RSSVCACCOUNT="[Account Nam]" /RSSVCPASSWORD="********" /FTSVCACCOUNT="[Account Nam]" /FTSVCPASSWORD="********" /SECURITYMODE="SQL" /SAPWD="********" /PID="[Your PID Value]" /SQLSYSADMINACCOUNTS="[Account Nam]" "AutoSql Admin Group" /ASSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /RSSHPINSTALLMODE="SharePointFilesOnlyMode" /RSINSTALLMODE="DefaultNativeMode"  
```  
  
## <a name="examples-of-sharepoint-mode-upgrade"></a>SharePoint モード アップグレードの例  
 次の例は、SharePoint モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をアップグレードします。 **RSUPGRADEPASSWORD** は、既存のレポート サーバー サービス アカウントのパスワードです。 RSUPGRADEPASSWORD は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アカウントがビルトイン アカウントである場合を除いて、アップグレード シナリオの必須フィールドです。  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[PID value]" /FTSVCACCOUNT="[DOMAIN\ACCOUNT]" /FTSVCPASSWORD="[ACCOUNTPASSSWORD]" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /RSUPGRADEPASSWORD="******"  
```  
  
 次の例を使用すると、SharePoint 共有サービス アーキテクチャに基づく SharePoint モードのインストールをアップグレードできます。 この例は ALLOWUPGRADEFORSSRSSHAREPOINTMODE スイッチを使用します。 共有サービス アーキテクチャに基づいていない古いバージョンのアップグレードの場合、スイッチは必要ありません。  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[Your PID Value]" /FTSVCACCOUNT="[ACCOUNT Name]" /FTSVCPASSWORD="****" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /ALLOWUPGRADEFORSSRSSHAREPOINTMODE="True"  
```  
  
## <a name="examples-of-native-mode-installation"></a>ネイティブ モード インストールの例  
  
```  
Setup.exe /q /ACTION="Install" /INSTANCENAME="MSSQLSERVER" /FEATURES="SQLEngine,Replication,SNAC,SNAC_SDK,Browser,Writer,AS,IS,MDS,Adv_SSMS,BC,BOL,Conn,SDK,DReplay_CTLR,DReplay_CLT,DQC,BIDS,FullText, RS,DQ,SSMS" /INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" /INSTALLSQLDATADIR="C:\Program Files\Microsoft SQL Server" /SQLSVCACCOUNT="[Account Name]" /SQLSVCPASSWORD="********" /AGTSVCACCOUNT="[Account Nam]" /AGTSVCPASSWORD="********" /CTLRSVCACCOUNT="[Account Nam]" /CTLRSVCPASSWORD="********" /CLTSVCACCOUNT="[Account Nam]" /CLTSVCPASSWORD="********" /ASSVCACCOUNT="[Account Nam]" /ASSVCPASSWORD="********" /RSSVCACCOUNT="[Account Nam]" /RSSVCPASSWORD="********" /FTSVCACCOUNT="[Account Nam]" /FTSVCPASSWORD="********" /SECURITYMODE="SQL" /SAPWD="********" /PID="[Your PID Value]" /SQLSYSADMINACCOUNTS="[Account Nam]" "AutoSql Admin Group" /ASSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /RSINSTALLMODE="DefaultNativeMode"  
```  
  
## <a name="see-also"></a>参照  
 [コマンド プロンプトから SQL Server 2014 をインストールします。](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [SysPrep パラメーター](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#SysPrep)   
 [コマンド プロンプトからの PowerPivot のインストール](../../sql-server/install/install-powerpivot-from-the-command-prompt.md)  
  
  
