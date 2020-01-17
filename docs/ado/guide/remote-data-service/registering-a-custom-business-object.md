---
title: カスタム ビジネス オブジェクトを登録する |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- custom business object in RDS [ADO]
- registering custom business objects in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: e9032ad8-d14c-42e3-ba13-cb5f00084a79
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f998463e0f8190aa040b801d2fd29c732bb31dce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922364"
---
# <a name="registering-a-custom-business-object"></a>カスタム ビジネス オブジェクトの登録
Web サーバー経由 (.dll または .exe) は、カスタム ビジネス オブジェクトが正常に起動するにはこの手順で説明したように、ビジネス オブジェクトの ProgID レジストリに入力する必要があります。 この RDS 機能は、承認された実行可能ファイルだけを実行して、Web サーバーのセキュリティを保護します。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
> [!NOTE]
>  MDAC 2.0 およびそれ以降、Windows DAC、既定のビジネス オブジェクトの[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)MDAC/Windows DAC のインストール時に既定で登録されていません。 ただし場合、 **RDSServer.DataFactory**登録された新しいインストールのレジストリ エントリが保持がインストールの前に、コンピューター上で実行も安全だと、します。  
  
### <a name="to-register-a-custom-business-object"></a>カスタム ビジネス オブジェクトを登録するには。  
  
1.  クリックして**開始**順にクリックします**実行**します。  
  
2.  型**RegEdit**  をクリック**OK**します。  
  
3.  レジストリ エディターに移動、 **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch**レジストリ キー。  
  
4.  選択、 **ADCLaunch**キー、し、**編集**メニューで、**新規** をクリック**キー**します。  
  
5.  カスタム ビジネス オブジェクトの ProgID を入力し、クリックして**Enter**します。 ままに、**値**空白エントリ。


