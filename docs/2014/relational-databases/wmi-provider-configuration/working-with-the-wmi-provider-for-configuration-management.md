---
title: WMI Provider for Configuration Management の使用 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- permissions [WMI]
- connection strings [WMI]
- security [WMI]
- WMI Provider for Configuration Management, connection strings
- WMI Provider for Configuration Management, security
- late binding [WMI]
- WMI Provider for Configuration Management, late binding
- binding [WMI]
ms.assetid: 34daa922-7074-41d0-9077-042bb18c222a
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9d9f3ab9f80c6f2c77153439cf554f0ae8598586
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68195772"
---
# <a name="working-with-the-wmi-provider-for-configuration-management"></a>WMI Provider for Configuration Management の操作
  WMI Provider for Computer Management を使用したプログラミングを行う前に、次の点について考慮してください。  
  
## <a name="binding"></a>Binding  
 WMI Provider for Configuration Management は、COM オブジェクト モデルであり、事前バインドも遅延バインドもサポートしています。 遅延バインドを行う場合、VBScript などのスクリプト言語を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス、ネットワーク設定、別名をプログラムで操作することができます。  
  
 スクリプト言語を使用して WMI プロバイダーの実装のプログラミングの詳細については、次を参照してください。、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] MSDN [Web サイト](https://go.microsoft.com/fwlink/?linkid=15426)します。  
  
## <a name="specifying-a-connection-string"></a>接続文字列を指定します。  
 アプリケーションは、プロバイダーによって定義された WMI 名前空間に接続することで、WMI Provider for Configuration Management を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにダイレクトします。 Windows WMI サービスは、この名前空間をプロバイダー DLL にマップし、これをメモリに読み込みます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスはすべて、1 つの WMI 名前空間で表されます。 名前空間の既定値は次のとおりです。  
  
```  
\\.\root\Microsoft\SqlServer\ComputerManagement12\instance_name  
```  
  
 `instance_name` の既定値は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインストール内の `MSSQLSERVER` になります。  
  
 **注:** Windows ファイアウォール経由で接続する場合は、コンピューターが適切に構成されているかどうかを確認する必要があります。 Windows Management Instrumentation のドキュメントの「Windows ファイアウォール経由の接続」記事を参照してください[!INCLUDE[msCoName](../../includes/msconame-md.md)]MSDN [Web サイト](https://go.microsoft.com/fwlink/?linkid=15426)します。  
  
## <a name="permissions-and-server-authentication"></a>権限とサーバー認証  
 WMI Provider for Configuration Management にアクセスするには、クライアント WMI 管理スクリプトが、ターゲット コンピューター上の管理者のコンテキストで実行されている必要があります。 アクセスするユーザーは、管理するコンピューターのローカル Windows 管理者グループのメンバーである必要があります。  
  
 管理者は、グループ ポリシーを設定して、WMI プロバイダーへのユーザー アクセスを制御することができます。 グループ ポリシーの設定の詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーのヘルプの「グループ ポリシーと MMC」を参照してください。  
  
 WMI 管理スクリプトを使用すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスが実行されるアカウントを更新することができます。  
  
 WMI Provider for Configuration Management では、セキュリティ証明書がサポートされています。 証明書の詳細については、次を参照してください。[暗号化階層](../security/encryption/encryption-hierarchy.md)します。  
  
## <a name="see-also"></a>参照  
 [SQL Server 構成マネージャー](../sql-server-configuration-manager.md)  
  
  
