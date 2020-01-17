---
title: OLE DB Provider for Internet Publishing |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
ms.assetid: 4869aafa-7401-4ce1-93ce-45406a60274f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 80a373196f98a964bc3e522cc9329907a3392b95
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923902"
---
# <a name="the-ole-db-provider-for-internet-publishing"></a>OLE DB Provider for Internet Publishing
ADO[レコード](../../../ado/reference/ado-api/record-object-ado.md)と[Stream](../../../ado/reference/ado-api/stream-object-ado.md)オブジェクトで使える Microsoft OLE DB Provider for Internet Publishing (インターネット発行プロバイダー) にアクセスして、リソースを操作する Web フォルダーやファイルなどMicrosoft FrontPage によって処理されます。 ADO では、ソースを指定することができます、**レコード**、 **Stream**、または[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) url。 ことができますし、アップロード、ダウンロード、移動、コピー、およびリソースを削除またはリソース プロパティを直接操作します。  
  
 使用するコード例**レコード**と**ストリーム**公開インターネット プロバイダーは、次を参照してください。、[インターネットによる公開シナリオ](../../../ado/guide/data/internet-publishing-scenario.md)します。  
  
 インターネット公開プロバイダーは、Microsoft Windows 2000 と共にインストールされます。 以前のバージョンのインターネット発行プロバイダーでは、Microsoft Office 2000 および Microsoft Internet Explorer 5.0 で入手できます。  
  
 ADO をパブリッシング用プロバイダー、インターネットに接続するための 3 つの方法はあります。  
  
-   指定"URL ="接続文字列にします。 以下に例を示します。  
  
    ```  
    objConn.Open "URL=https://servername"  
    ```  
  
-   指定の Msdaipp.dso、*プロバイダー*接続文字列のキーワード。 以下に例を示します。  
  
    ```  
    objConn.Open "provider=MSDAIPP.DSO;data source=https://servername"  
    ```  
  
-   指定の Msdaipp.dso、[プロバイダー](../../../ado/reference/ado-api/provider-property-ado.md)のプロパティ、[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト。 以下に例を示します。  
  
    ```  
    objConn.Provider = "MSDAIPP.DSO"  
    objConn.Open "https://servername"  
    ```  
  
> [!NOTE]
>  Msdaipp.dso がいずれかで、プロバイダーの値として明示的に指定されている場合、*プロバイダー*接続文字列キーワード、または**プロバイダー**プロパティは使用できません"URL ="接続文字列にします。 この場合、エラーが発生します。 前述のように、URL を単に指定代わりに、します。  
  
 インターネット公開プロバイダーの詳細については、次を参照してください[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)、またはプロバイダーのドキュメントがソース アプリケーションに付属の OLE DB プロバイダー。Internet Publishing がインストールされました。Windows 2000、Office 2000、または Internet Explorer 5.0 です。
