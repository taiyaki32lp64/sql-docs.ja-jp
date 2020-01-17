---
title: GenerateDatabaseRightsScript メソッド (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- GenerateDatabaseRightsScript (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- GenerateDatabaseRightsScript method
ms.assetid: f2e6dcc9-978f-4c2c-bafe-36c330247fd0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8714aee2b5bb33c84a1d9f11b626d3e21e06ed1f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65570966"
---
# <a name="configurationsetting-method---generatedatabaserightsscript"></a>ConfigurationSetting メソッド - GenerateDatabaseRightsScript
  レポート サーバー データベースおよびレポート サーバーの実行に必要なその他のデータベースに対してユーザー権限を付与する際に使用できる、SQL スクリプトを生成します。 呼び出し元は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース サーバーに接続して、スクリプトを実行する必要があります。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Sub GenerateDatabaseRightsScript(ByVal UserName As String, _  
    ByVal DatabaseName As String, ByVal IsRemote As Boolean, _  
    ByVal IsWindowsUser As Boolean, ByRef Script As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GenerateDatabaseRightsScript(string UserName, string DatabaseName, bool IsRemote, bool IsWindowsUser, out string Script,   
out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>パラメーター  
 *UserName*  
 スクリプトで権限を与えるユーザーのユーザー名または Windows セキュリティ識別子 (SID)。  
  
 *DatabaseName*  
 スクリプトによってユーザーにアクセス権が付与されるデータベース名。  
  
 *IsRemote*  
 データベースがレポート サーバーに対してリモートであるかどうかを示すブール値。  
  
 *IsWindowsUser*  
 指定されたユーザー名が Windows ユーザーか [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーかを示すブール値。  
  
 *[スクリプト]*  
 [out] 生成された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スクリプトを含む文字列。  
  
 *HRESULT*  
 [out] 呼び出しの成功または失敗を示す値。  
  
## <a name="return-value"></a>戻り値  
 メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値 0 は、メソッド呼び出しが成功したことを示します。 0 以外の値は、エラーが発生したことを示します。  
  
## <a name="remarks"></a>Remarks  
 *DatabaseName* が空の場合、 *IsRemote* は無視され、レポート サーバーの構成ファイルの値がデータベース名に使用されます。  
  
 *IsWindowsUser* を **true** に設定した場合、*UserName* は \<domain>\\<username\> 形式で指定する必要があります。  
  
 *IsWindowsUser* を **true**に設定した場合、生成されたスクリプトによって、レポート サーバー データベースが既定のデータベースとして設定され、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]へのログイン権限がユーザーに付与されます。また、レポート サーバー データベース、レポート サーバー一時データベース、master データベース、および MSDB システム データベースの **RSExec** ロールが付与されます。  
  
 *IsWindowsUser* を **true**に設定した場合、メソッドは入力として標準 Windows SID を受け取ります。 標準 Windows SID またはサービス アカウント名が指定されると、ユーザー名文字列に変換されます。 データベースがローカルである場合、アカウントはアカウントのローカライズされた正しい表現に変換されます。 データベースがリモートである場合、アカウントはコンピューターのアカウントとして表されます。  
  
 次の表は、変換されるアカウントとそのリモート表現を示しています。  
  
|変換されるアカウントまたは SID|共通名|リモート名|  
|---------------------------------------|-----------------|-----------------|  
|(S-1-5-18)|[ローカル システム]|\<Domain>\\<ComputerName\>$|  
|.\LocalSystem|[ローカル システム]|\<Domain>\\<ComputerName\>$|  
|ComputerName\LocalSystem|[ローカル システム]|\<Domain>\\<ComputerName\>$|  
|LocalSystem|[ローカル システム]|\<Domain>\\<ComputerName\>$|  
|(S-1-5-20)|Network Service|\<Domain>\\<ComputerName\>$|  
|NT AUTHORITY\NetworkService|Network Service|\<Domain>\\<ComputerName\>$|  
|(S-1-5-19)|Local Service|エラー - 下記参照。|  
|NT AUTHORITY\LocalService|Local Service|エラー - 下記参照。|  
  
 [!INCLUDE[win2kfamily](../../includes/win2kfamily-md.md)]では、組み込みアカウントを使用し、レポート サーバー データベースがリモートである場合、エラーが返されます。  
  
 **LocalService** 組み込みアカウントを指定し、レポート サーバー データベースがリモートである場合、エラーが返されます。  
  
 *IsWindowsUser* が true であり、 *UserName* に指定した値を変換する必要がある場合、WMI プロバイダーはレポート サーバー データベースが同じコンピューターにあるかリモート コンピューターにあるかを確認します。 インストールがローカルであるかどうかを確認するため、WMI プロバイダーは以下の値一覧に対して DatabaseServerName プロパティを評価します。 一致が見つかった場合、データベースはローカルです。 見つからなかった場合、リモートです。 比較では大文字小文字を区別しません。  
  
|DatabaseServerName の値|例|  
|---------------------------------|-------------|  
|"."||  
|"(local)"||  
|"LOCAL"||  
|localhost||  
|\<Machinename>|testlab14|  
|\<MachineFQDN>|example.redmond.microsoft.com|  
|\<IPAddress>|180.012.345,678|  
  
 *IsWindowsUser* を **true**に設定した場合、WMI プロバイダーは LookupAccountName を呼び出してアカウントの SID を取得し、次に LookupAccountSID を呼び出して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スクリプトに含める名前を取得します。 このようにすると、使用するアカウント名は必ず [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 検証に合格します。  
  
 *IsWindowsUser* を **false**に設定した場合、生成されたスクリプトによって、レポート サーバー データベース、レポート サーバー一時データベース、および MSDB データベースの **RSExec** ロールが付与されます。  
  
 *IsWindowsUser* を **false**に設定した場合、スクリプトの実行を成功させるには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に SQL Server ユーザーが既に存在している必要があります。  
  
 レポート サーバーにレポート サーバー データベースが指定されていない場合、GrantRightsToDatabaseUser を呼び出すとエラーが返されます。  
  
 生成されたスクリプトは、 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005、および [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]をサポートします。  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting メンバー](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
