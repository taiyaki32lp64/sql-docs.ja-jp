---
title: SetDatabaseConnection メソッド (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SetDatabaseConnection (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetDatabaseConnection method
ms.assetid: c040aa78-92b8-41e4-9ae2-eff9fcdddc5b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: af40d79d876edb8f0448bd5abaef5c173a6edce9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65572600"
---
# <a name="configurationsetting-method---setdatabaseconnection"></a>ConfigurationSetting メソッド - SetDatabaseConnection
  特定のレポート サーバー データベースへのレポート サーバー データベース接続を設定します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Sub SetDatabaseConnection(Server as String, _  
    DatabaseName as string, CredentialsType as Integer, _  
    Username as String, Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void BackupEncryptionKey(string Server,   
    string DatabaseName, Int32 CredentialsType,   
    string UserName, string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>パラメーター  
 *Server*  
 レポート サーバー データベースをホストするために使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前。  
  
 *DatabaseName*  
 レポート サーバー データベースの名前。  
  
 *CredentialsType*  
 接続に使用する資格情報の種類。 値は次のとおりです。  
  
-   0 : Windows  
  
-   1 : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   2 : Windows サービス  
  
 *UserName*  
 レポート サーバー データベースへの接続に使用するアカウント名。  
  
 *パスワード*  
 レポート サーバー データベースへの接続に使用するパスワード。  
  
 *HRESULT*  
 [out] 呼び出しの成功または失敗を示す値。  
  
## <a name="return-value"></a>戻り値  
 メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値 0 は、メソッド呼び出しが成功したことを示します。 0 以外の値は、エラーが発生したことを示します。  
  
## <a name="remarks"></a>Remarks  
 *CredentialsType* パラメーターを 0 (Windows) に設定する場合は、 *UserName* パラメーターと *Password* パラメーターを設定する必要があります。 *UserName* パラメーターは "domain\username" 形式で設定し、値は有効な Windows ログオンを表す必要があります。  
  
 *CredentialsType* パラメーターを 1 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) に設定する場合は、*UserName* パラメーターに渡される値が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン名の要件を満たしている必要があります。  
  
 *CredentialsType* パラメーターを 2 (Windows サービス) に設定する場合は、レポート サーバーがレポート サーバー データベースとの接続に統合セキュリティを使用し、 *UserName* パラメーターと *Password* パラメーターは無視されます。 Reporting Server Web サービスは、レポート サーバー データベースへのアクセスに、[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] アカウントまたはアプリケーション プール アカウントのいずれかと、Windows サービス アカウントを使用します。  
  
 SetDatabaseConnection メソッドを呼び出すと、資格情報とデータベース情報が暗号化され、指定されたレポート サーバーの構成ファイルに格納されます。  
  
 SetDatabaseConnection メソッドは、レポート サーバーが指定されたデータを使用してレポート サーバー データベースと接続できるかチェックしません。  
  
 ConnectionPoolSize プロパティを初めて設定する場合、その値は、ConnectionPoolSize = #Processors * 75 で算出されたプロセッサ数に基づいて設定されます。  
  
 SetDatabaseConnection メソッドは、指定されたアカウントに権限を付与しません。 レポート サーバー データベースへのアクセスを必要とするアカウントごとに [GenerateDatabaseRightsScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaserightsscript.md) メソッドを呼び出し、結果のスクリプトを実行する必要があります。  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting メンバー](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
