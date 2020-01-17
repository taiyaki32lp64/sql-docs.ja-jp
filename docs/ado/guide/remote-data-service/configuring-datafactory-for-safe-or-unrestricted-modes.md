---
title: 安全または無制限モード用の DataFactory の構成 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory configuration in RDS [ADO]
ms.assetid: 8ff24805-dc7a-42ae-b600-5bad0e3f51b8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 92e3b029d2b18065faf50dcd0343f64b7b01654e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922940"
---
# <a name="configuring-datafactory-for-safe-or-unrestricted-modes"></a>安全または無制限モード用の DataFactory の構成
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
 既定では、ADO は"safe"と共にインストール[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)構成します。 RDS サーバー コンポーネントのセーフ モードでは、次の項目が該当することを意味します。  
  
1.  ハンドラーは、(これがレジストリ キー設定が必須) RDSServer.DataFactory の必要があります。  
  
2.  既定のハンドラー、msdfmap.handler、登録されている、safe ハンドラーの一覧で存在し、既定のハンドラーとしてマークされています。  
  
3.  Msdfmap.ini ファイルは、Windows ディレクトリにインストールされます。 3 層のモードで RDS を使用する前に、必要に応じてこのファイルを構成する必要があります。  
  
 必要に応じて、構成できます、無制限**DataFactory**インストールします。 **DataFactory**直接カスタム ハンドラーがないことができます。 接続文字列を変更することで、カスタム ハンドラーを使用できますが、必須ではありません。 使用する場合の詳細については、 **RDSServer.DataFactory**オブジェクトを参照してください[RDS アプリケーションのセキュリティで保護する](../../../ado/guide/remote-data-service/securing-rds-applications.md)します。  
  
 安全な構成のハンドラーのレジストリ エントリを設定するには、レジストリ ファイル handsafe.reg を用意されています。 セーフ モードで実行するには、handsafe.reg を実行します。  
  
 Handsafe.reg を実行した後は、停止し、コマンド プロンプト ウィンドウで、次のコマンドを入力して、Web サーバー上の World Wide Web 発行サービスを再起動する必要があります。"NET STOP W3SVC"と"NET 開始 W3SVC"。  
  
## <a name="see-also"></a>関連項目  
 [DataFactory のカスタマイズ](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [RDS の基礎](../../../ado/guide/remote-data-service/rds-fundamentals.md)



