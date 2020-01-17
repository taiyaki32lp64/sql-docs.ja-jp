---
title: GenerateDatabaseRightsScript メソッド (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- GenerateDatabaseRightsScript (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- GenerateDatabaseRightsScript method
ms.assetid: f2e6dcc9-978f-4c2c-bafe-36c330247fd0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 575eab878e0ef9b4357c09a0a3deedf143c237b9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66098480"
---
# <a name="generatedatabaserightsscript-method-wmi-msreportserverconfigurationsetting"></a>GenerateDatabaseRightsScript メソッド (WMI MSReportServer_ConfigurationSetting)
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
  
## <a name="remarks"></a>コメント  
 *DatabaseName* が空の場合、 *IsRemote* は無視され、レポート サーバーの構成ファイルの値がデータベース名に使用されます。  
  
 場合*IsWindowsUser*に設定されている`true`、 *UserName*形式にする必要があります\<ドメイン >\\< ユーザー名\>します。  
  
 ときに*IsWindowsUser*に設定されている`true`、生成されるスクリプトのユーザーへのログイン権限を付与する、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、許可が既定のデータベースとして、レポート サーバー データベースを設定、 **RSExec** 、レポート サーバー データベース、レポート サーバー一時データベース、master データベースおよび MSDB システム データベースの役割。  
  
 ときに*IsWindowsUser*に設定されている`true`メソッドは入力として標準 Windows Sid を受け取ります。 標準 Windows SID またはサービス アカウント名が指定されると、ユーザー名文字列に変換されます。 データベースがローカルである場合、アカウントはアカウントのローカライズされた正しい表現に変換されます。 データベースがリモートである場合、アカウントはコンピューターのアカウントとして表されます。  
  
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
  
 `LocalService` 組み込みアカウントを指定し、レポート サーバー データベースがリモートである場合、エラーが返されます。  
  
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
  
 ときに*IsWindowsUser*に設定されている`true`、WMI プロバイダーは、アカウントの SID を取得する LookupAccountName の呼び出しし、に配置する名前を取得する LookupAccountSID を呼び出して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スクリプト。 このようにすると、使用するアカウント名は必ず [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 検証に合格します。  
  
 ときに*IsWindowsUser*に設定されている`false`、付与のスクリプトを生成、 **RSExec**レポート サーバー データベース、レポート サーバー一時データベースおよび MSDB データベース ロール。  
  
 ときに*IsWindowsUser*に設定されている`false`、SQL Server のユーザーに既に存在する必要があります、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スクリプトを正常に実行します。  
  
 レポート サーバーにレポート サーバー データベースが指定されていない場合、GrantRightsToDatabaseUser を呼び出すとエラーが返されます。  
  
 生成されたスクリプトは、 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005、および [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]をサポートします。  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting メンバー](msreportserver-configurationsetting-members.md)  
  
  
