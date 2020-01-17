---
title: WMI Provider for Configuration Management の理解 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management, operations supported
ms.assetid: 92323972-7943-4208-bbf4-050774fb6027
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b224868d4d9fc111cdbf9482282767420b6adcc8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63205150"
---
# <a name="understanding-the-wmi-provider-for-configuration-management"></a>WMI Provider for Configuration Management について
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成管理用 WMI プロバイダーを提供します。 これにより、WMI (Windows Management Instrumentation) を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のクライアントおよびサーバーのネットワーク設定、およびサーバー別名を管理することができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス、ネットワーク設定、および別名は、\microsoft\sqlserver\computermanagement WMI オブジェクトによって表される*nn*コンピューターの名前空間。 指定されたコンピューター上で WMI プロバイダーを使用して接続が確立された後、サービス、ネットワーク設定、別名は、WQL またはスクリプティング言語を使用してクエリを行うことができます。  
  
 WMI プロバイダーは、インスタンス プロバイダーです。 インスタンスを提供、 [WMI クラス](../wmi-provider-configuration-classes/wmi-provider-for-configuration-management-classes.md)次の非同期操作をサポートしています。  
  
 インスタンスの取得  
 特定のクラス型インスタンスの取得です。  
  
 列挙値  
 クラス型のすべてのインスタンスの列挙です。  
  
 変更  
 クラス型の特定のインスタンスの変更です。  
  
 クラスには、クラスのプロパティの変更を許可するメソッドがあります。  
  
 削除  
 クラス型の特定のインスタンスの削除です。  
  
 クエリ処理  
 フィルターに基づいたクラス型のインスタンスの列挙です。  
  
 構成管理用 WMI プロバイダーを使用して管理アプリケーションの例については、次を参照してください。 [WQL を使用して、WMI Provider for Configuration Management でのスクリプト言語](using-wql-and-scripting-languages-with-the-wmi-provider.md)します。  
  
 WMI プロバイダーを使用して管理アプリケーションのプログラミングの詳細については、WMI のドキュメントを参照してください、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework SDK。  
  
## <a name="see-also"></a>参照  
 [WMI Provider for Configuration Management の使用](working-with-the-wmi-provider-for-configuration-management.md)   
 [WQL およびスクリプティング言語での WMI Provider for Configuration Management の使用](using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
