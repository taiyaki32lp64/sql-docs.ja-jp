---
title: SQL Server Native Client のサポート ポリシー |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 09c80cf4-23e6-4027-a24f-cdb9c87af811
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4e5c7a01cc2a9569dd8c05316a2aa3314959e894
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046527"
---
# <a name="support-policies-for-sql-server-native-client"></a>SQL Server Native Client のサポート ポリシー
  ここでは、さまざまなデータ アクセス コンポーネントを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client で使用する方法について説明します。  
  
## <a name="server-support"></a>サーバー サポート  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 への接続をサポートしている[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]、および[!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]します。  
  
## <a name="supported-operating-system-versions"></a>サポートされるオペレーティング システムのバージョン  
 次の表に、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client をサポートするオペレーティング システムの一覧を示します。  
  
|SQL Server Native Client のバージョン|サポートされるオペレーティング システム|  
|--------------------------------------|---------------------------------|  
|SQL Server Native Client (SQL Server 2005)|Microsoft Windows 2000 Service Pack 4 以降<br />Microsoft Windows Server 2003 またはそれ以降<br />Microsoft Windows XP Service Pack 1 またはそれ以降<br />Microsoft Windows Vista (必要[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Service Pack 2 以降)<br />Microsoft Windows Server 2008 (必要[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Service Pack 2 以降)|  
|SQL Server Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)])|Microsoft Windows Server 2003 Service Pack 2、またはそれ以降<br />Microsoft Windows XP Service Pack 2 またはそれ以降<br />Microsoft Windows Vista<br />-   Microsoft Windows Server 2008|  
|SQL Server Native Client 10.5 ([!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)])|Microsoft Windows Server 2003 Service Pack 2、またはそれ以降<br />Microsoft Windows XP Service Pack 2 またはそれ以降<br />Microsoft Windows Vista<br />-   Microsoft Windows Server 2008<br />-   Microsoft Windows 7|  
|SQL Server Native Client 11.0 ([!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] および [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)])|Microsoft Windows Vista<br />-   Microsoft Windows Server 2008<br />-   Microsoft Windows 7<br />Microsoft Windows 8<br />Microsoft Windows Server 2012|  
  
## <a name="ado-support-policies"></a>ADO サポート ポリシー  
 ADO アプリケーションでは、[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降の機能を必要としない場合に、Windows に付属している SQLOLEDB OLE DB プロバイダーを使用できます。  
  
 ADO アプリケーションでのバージョンを使用できます[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]でネイティブ クライアントが含まれている[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]します。 また、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に含まれている [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Native Client 11.0 も使用できますが、これを使用する場合は、接続文字列に `DataTypeCompatibility=80` を指定する必要があります。 `DataTypeCompatibility=80` が接続文字列に含まれている場合は、[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] の機能しか使用できません。  
  
## <a name="bcp-support-policies"></a>BCP サポート ポリシー  
 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 以降では、bcp.exe は、bcp.exe が提供された [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のバージョンより 3 バージョン前までの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のデータ ファイルをサポートします。  
  
## <a name="odbc-support-policies"></a>ODBC サポート ポリシー  
 アプリケーションは、Windows オペレーティング システムに付属している [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ODBC ドライバーを使用する必要があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、アプリケーションが特定のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client との互換性が保証されている場合に使用できます。  
  
## <a name="ole-db-support-policies"></a>OLE DB サポート ポリシー  
 アプリケーションは Windows オペレーティング システムに付属している [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB プロバイダーを使用する必要があります。 アプリケーションと特定のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client との互換性が保証されている場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーを使用することができます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client との互換性が保証されていない OLE DB アプリケーションでは、接続文字列に `DataTypeCompatibility=80` を指定すると、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client を使用できます。  
  
 OLE DB サービス コンポーネントを使用している OLE DB アプリケーションでは、接続文字列に `DataTypeCompatibility=80` を指定した場合のみ、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client を使用できます。 ただし、機能の後に追加[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]ここで提供されます。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client を使用したアプリケーションのビルド](building-applications-with-sql-server-native-client.md)  
  
  
