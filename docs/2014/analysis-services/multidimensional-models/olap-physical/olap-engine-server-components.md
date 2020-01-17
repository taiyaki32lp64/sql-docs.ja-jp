---
title: OLAP エンジンサーバーコンポーネント |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- Analysis Services, architecture
- ports [Analysis Services]
- XML/A listener
- server architecture [Analysis Services]
ms.assetid: 5193c976-9dcd-459c-abba-8c3c44e7a7f2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0537be8bda9c367fc381140183b10ddf383cf16a
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68889523"
---
# <a name="olap-engine-server-components"></a>OLAP エンジンのサーバー コンポーネント
  の[!INCLUDE[msCoName](../../../includes/msconame-md.md)] サーバー[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]コンポーネントは、Windows サービスとして実行される msmdsrv.exe アプリケーションです。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] このアプリケーションは、セキュリティ コンポーネント、XML for Analysis (XMLA) リスナー コンポーネント、クエリ プロセッサ コンポーネント、および次の機能を実行するその他多くの内部コンポーネントで構成されています。  
  
-   クライアントから受信したステートメントの解析  
  
-   メタデータの管理  
  
-   トランザクションの処理  
  
-   計算の処理  
  
-   ディメンションおよびセル データの格納  
  
-   集計の作成  
  
-   クエリのスケジュール設定  
  
-   オブジェクトのキャッシュ  
  
-   サーバー リソースの管理  
  
## <a name="architectural-diagram"></a>アーキテクチャの図  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] のインスタンスはスタンドアロン サービスとして実行され、サービスとの通信は、HTTP または TCP を使用して XML for Analysis (XMLA) 経由で行われます。 AMO は、ユーザー アプリケーションと [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] インスタンスの間のレイヤーです。 このレイヤーは、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 管理オブジェクトへのアクセスを提供します。 AMO は、クライアント アプリケーションからコマンドを受け取り、それを [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] インスタンス用の XMLA メッセージに変換するクラス ライブラリです。 AMO は、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] インスタンス オブジェクトをクラスとして、エンド ユーザー アプリケーションに提示します。このクラスには、コマンドを実行するメソッド メンバーと、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] オブジェクトのデータを持つプロパティ メンバーが含まれます。  
  
 次の図は、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] コンポーネントのアーキテクチャを示しており、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] インスタンス内で実行されるすべての主要な要素と、インスタンスと連携するすべてのユーザー コンポーネントを含んでいます。 また、この図は、XML for Analysis (XMLA) リスナーと、HTTP または TCP のいずれかを使用する以外に、インスタンスにアクセスする方法がないことも示しています。  
  
 ![Analysis Services システムのアーキテクチャの図](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/analysisservicessystemarchitecture.gif "Analysis Services システムのアーキテクチャの図")  
  
## <a name="xmla-listener"></a>XMLA リスナー  
 XMLA リスナー コンポーネントでは、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] とそのクライアントの間のすべての XMLA 通信が処理されます。 Msmdsrv.exe ファイルの[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]構成設定を使用して、インスタンスがリッスンするポートを指定できます。 `Port` [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] このファイルの 0 の値は、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] が既定のポートをリッスンすることを示します。 特に指定がなければ、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] では次の既定の TCP ポートが使用されます。  
  
|Port|説明|  
|----------|-----------------|  
|2383|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]の既定のインスタンスです。|  
|2382|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]の他のインスタンスのリダイレクターです。|  
|サーバーの起動時に動的に割り当てられます。|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]の名前付きインスタンスです。|  
  
 詳細については[、「Analysis Services アクセスを許可するための Windows ファイアウォールの構成」を](../../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)参照してください。  
  
## <a name="see-also"></a>関連項目  
 [オブジェクトの名前&#40;付け規則 Analysis Services&#41;](object-naming-rules-analysis-services.md)   
 [物理アーキテクチャ &#40;Analysis Services - 多次元データ&#41;](understanding-microsoft-olap-physical-architecture.md)   
 [論理アーキテクチャ&#40;Analysis Services-多次元データ&#41;](../olap-logical/understanding-microsoft-olap-logical-architecture.md)  
  
  
