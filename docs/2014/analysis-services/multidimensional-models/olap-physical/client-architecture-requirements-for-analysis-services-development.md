---
title: Analysis Services Development のクライアントアーキテクチャの要件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- local mining models [Analysis Services]
- Analysis Services, architecture
- providers [Analysis Services]
- data pumps [Analysis Services]
- client architecture [Analysis Services]
- local cubes [Analysis Services]
ms.assetid: 03a8eb6b-159f-4a0a-afbe-06a2424b6090
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e91e1c7a1586c0b2aff3630bfd8a9a6cd60ef53c
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68889576"
---
# <a name="client-architecture-requirements-for-analysis-services-development"></a>Analysis Services 開発に関するクライアント アーキテクチャの要件
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、シンクライアントアーキテクチャをサポート[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]しています。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]計算エンジンは完全にサーバーベースであるため、すべてのクエリがサーバー上で解決されます。 つまり、クエリごとにクライアントとサーバー間での単一ラウンド トリップが必要です。この結果、クエリの複雑さが増すにつれてパフォーマンスが変化します。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] のネイティブ プロトコルは、XML for Analysis (XMLA) です。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] では、クライアント アプリケーション用のデータ アクセス インターフェイスがいくつか用意されていますが、これらのすべてのコンポーネントは XML for Analysis を使用して [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] のインスタンスと通信を行います。  
  
 異なるプログラミング言語をサポートするため、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ではいくつかの異なるプロバイダーが用意されています。 プロバイダーは、インターネット インフォメーション サービス (IIS) を通じて TCP/IP または HTTP で SOAP パケットの XML for Analysis を送受信することによって [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] サーバーと通信します。 IIS によってインスタンス化された、データ ポンプと呼ばれる COM オブジェクトを使用する HTTP 接続は、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] データのパイプとして機能します。 データ ポンプでは、HTTP ストリーム内に含まれる、基になるデータはまったく検証されません。また、基になるデータ構造はデータ ライブラリ内にあるコードではまったく使用できません。  
  
 ![Analysis Services の論理クライアントアーキテクチャ](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-clientarch9.gif "Analysis Services の論理クライアントアーキテクチャ")  
  
 Win32 クライアント アプリケーションから [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] サーバーへの接続には、OLE DB for OLAP インターフェイスまたは Microsoft Visual Basic® などのコンポーネント オブジェクト モデル (COM) オートメーション言語用の Microsoft® ActiveX® データ オブジェクト (ADO) オブジェクト モデルを使用できます。 .NET 言語で記述されたアプリケーションでは、ADOMD.NET を使用して [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] サーバーに接続できます。  
  
 既存のアプリケーションは、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] プロバイダーのいずれかを使用するだけで、変更しなくても [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] と通信できます。  
  
|プログラミング言語|データ アクセス インターフェイス|  
|--------------------------|---------------------------|  
|C++|OLE DB for OLAP (OLE DB for OLAP)|  
|Visual Basic 6|ADO MD (ADO MD)|  
|.NET 言語|ADO MD.NET|  
|SOAP をサポートするすべての言語|XML for Analysis (XML for Analysis)|  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] には、小規模な組織と大規模な組織の両方の配置に対応できる完全にスケーラブルな中間層を使用した Web アーキテクチャが装備されています。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] には、Web サービスへの広範な中間層のサポートが用意されています。 ASP アプリケーションは、OLAP および ADO MD の OLE DB でサポートされています。 ASP.NET アプリケーションは ADOMD.NET によってサポートされています。 次の図のように、中間層は、多数の同時ユーザーに対応できるスケーラブルな層です。  
  
 ![中間層アーキテクチャの論理図](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-midtierarch9.gif "中間層アーキテクチャの論理図")  
  
 クライアントおよび中間層アプリケーションは、いずれも、プロバイダーを使用せずに直接 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] と通信できます。 クライアントおよび中間層アプリケーションによっては、TCP/IP、HTTP、または HTTPS を使用して SOAP パケットで XML for Analysis を送信する場合もあります。 また、クライアントは SOAP をサポートする任意の言語を使用して記述されている場合もあります。 この場合、通信の管理には、TCP/IP を使用したサーバーへの直接接続が記述されている場合でも、HTTP を介したインターネット インフォメーション サービス (IIS) を使用する方法が最も管理が簡単です。 これが [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] に最適のシン クライアント ソリューションです。  
  
## <a name="analysis-services-in-tabular-or-sharepoint-mode"></a>テーブル モードまたは SharePoint モードの Analysis Services  
 で[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]は、表形式データベースの場合は xvelocity メモリ内分析エンジン (VertiPaq) モード、SharePoint サイトにパブリッシュ[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]されたブックの場合はサーバーを起動できます。  
  
 [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)] および [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] は、それぞれ SharePoint モードまたは表形式モードを使用するインメモリ データベースの作成とクエリがサポートされる、ただ 1 つのクライアント環境です。 Excel および[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]ツールを使用して作成した埋め込み PowerPivot データベースは、excel ブック内に格納され、excel .xlsx ファイルの一部として保存されます。  
  
 ただし、キューブ データをブックにインポートすると、従来のキューブに格納されたデータを [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] ブックで使用できます。 また、SharePoint サイトにパブリッシュされている場合、別の [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] ブックからデータをインポートすることもできます。  
  
> [!NOTE]  
>  [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] ブックのデータ ソースとしてキューブを使用する場合、キューブから取得するデータは、MDX クエリとして定義されます。ただし、データはフラット化スナップショットとしてインポートされます。 キューブのデータは、対話的に操作したり、更新したりすることはできません。  
  
### <a name="interfaces-for-powerpivot-client"></a>PowerPivot Client インターフェイス  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]では、Analysis Services に対して確立されたインターフェイスと言語を使用して、ブック内の xVelocity メモリ内分析エンジン (VertiPaq) ストレージエンジンと対話します。AMO と ADOMD.NET、および MDX と XMLA。 アドイン内では、メジャーは、Excel、Data Analysis Expressions (DAX) と同様の数式言語を使用して定義されます。 DAX の式は、インプロセス サーバーに送信される XMLA メッセージ内に埋め込まれます。  
  
### <a name="providers"></a>[プロバイダー]  
 と Excel [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]の間の通信では、MSOLAP OLEDB プロバイダー (バージョン 11.0) が使用されます。 MSOLAP プロバイダー内には、4 つの異なるモジュールまたはトランスポートがあり、クライアントとサーバー間のメッセージの送信に使用できます。  
  
 **TCP/IP**通常のクライアント/サーバー接続に使用されます。  
  
 **HTTP**SSAS データポンプサービスを介した HTTP 接続、または SharePoint PowerPivot Web サービス (WS) コンポーネントの呼び出しによって使用されます。  
  
 **INPROC**インプロセスエンジンへの接続に使用されます。  
  
 **チャネル**SharePoint ファーム内の PowerPivot System サービスとの通信のために予約されています。  
  
## <a name="see-also"></a>関連項目  
 [OLAP エンジンのサーバー コンポーネント](olap-engine-server-components.md)  
  
  
