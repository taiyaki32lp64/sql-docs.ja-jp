---
title: カスタム接続マネージャーの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom connection managers [Integration Services], creating
ms.assetid: e83f8e02-ace4-42e0-b979-2f6be1460985
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2fced98b5844105aa0f333a691cb747656112c10
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768928"
---
# <a name="creating-a-custom-connection-manager"></a>カスタム接続マネージャーの作成
  カスタム接続マネージャーを作成するために必要な手順は、[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] の他のカスタム オブジェクトの作成手順と同様です。  
  
-   基本クラスを継承する新しいクラスを作成します。 接続マネージャー用の基本クラスは <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase> です。  
  
-   クラスに、オブジェクトの種類を識別する属性を適用します。 接続マネージャー用の属性は <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute> です。  
  
-   基本クラスのメソッドとプロパティの実装をオーバーライドします。 接続マネージャーでは、<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ConnectionString%2A> プロパティ、<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A> メソッド、および <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ReleaseConnection%2A> メソッドが対象です。  
  
-   必要に応じて、カスタム ユーザー インターフェイスを開発します。 その場合、接続マネージャーでは、<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI> インターフェイスを実装するクラスが必要です。  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] に組み込まれているタスク、変換元、および変換先の多くは、組み込みの接続マネージャーの特定の種類でのみ機能します。 そのため、これらのサンプルは組み込みのタスクおよびコンポーネントではテストできません。  
  
## <a name="getting-started-with-a-custom-connection-manager"></a>カスタム接続マネージャーの概要  
  
### <a name="creating-projects-and-classes"></a>プロジェクトおよびクラスの作成  
 すべてのマネージド接続マネージャーは <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase> 基本クラスから派生するため、カスタム接続マネージャーを作成するには、最初に任意のマネージド プログラミング言語でクラス ライブラリ プロジェクトを作成してから、基本クラスを継承するクラスを作成します。 この派生クラスで、基本クラスのメソッドとプロパティをオーバーライドして、カスタム機能を実装します。  
  
 同じソリューション内に、もう 1 つのクラス ライブラリ プロジェクトをカスタム ユーザー インターフェイス用に作成します。 配置を容易にするため、ユーザー インターフェイス用に別個のアセンブリを使用することをお勧めします。そうすれば、接続マネージャーやそのユーザー インターフェイスの更新や再配置を個別に行うことができます。  
  
 どちらのプロジェクトも、アセンブリに署名するよう構成します。アセンブリは、厳密な名前のキー ファイルを使用して、ビルド時に生成されます。  
  
### <a name="applying-the-dtsconnection-attribute"></a>DtsConnection 属性の適用  
 作成したクラスに <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute> 属性を適用して、そのクラスが接続マネージャーとして識別されるようにします。 この属性には、接続マネージャーの名前、説明、および接続の種類など、デザイン時の情報を指定します。 <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute.ConnectionType%2A>と`Description`プロパティに対応、**型**と`Description`に表示される列、 **SSIS 接続マネージャーの追加**ダイアログ ボックスで、あるときに表示されます。パッケージの接続を構成する[!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]します。  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute.UITypeName%2A> プロパティを使用して、接続マネージャーをそのカスタム ユーザー インターフェイスにリンクします。 このプロパティに必要な公開キー トークンを取得するには、**sn.exe -t** を使用して、ユーザー インターフェイス アセンブリへの署名に使用するキー ペア (.snk) ファイルから公開キー トークンを表示します。  
  
```vb  
<DtsConnection(ConnectionType:="SQLVB", _  
  DisplayName:="SqlConnectionManager (VB)", _  
  Description:="Connection manager for Sql Server", _  
  UITypeName:="SqlConnMgrUIVB.SqlConnMgrUIVB,SqlConnMgrUIVB,Version=1.0.0.0,Culture=neutral,PublicKeyToken=<insert public key token here>")> _  
Public Class SqlConnMgrVB  
  Inherits ConnectionManagerBase  
  . . .  
End Class  
```  
  
```csharp  
[DtsConnection(ConnectionType = "SQLCS",  
  DisplayName = "SqlConnectionManager (CS)",  
  Description = "Connection manager for Sql Server",  
  UITypeName = "SqlConnMgrUICS.SqlConnMgrUICS,SqlConnMgrUICS,Version=1.0.0.0,Culture=neutral,PublicKeyToken=<insert public key token here>")]  
public class SqlConnMgrCS :  
ConnectionManagerBase  
{  
  . . .  
}  
```  
  
## <a name="building-deploying-and-debugging-a-custom-connection-manager"></a>カスタム接続マネージャーのビルド、配置、およびデバッグ  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のカスタム接続マネージャーをビルド、配置、およびデバッグする手順は、他の種類のカスタム オブジェクトの手順と同様です。 詳細については、「[カスタム オブジェクトのビルド、配置、デバッグ](../building-deploying-and-debugging-custom-objects.md)」を参照してください。  
  
![Integration Services のアイコン (小)](../../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>関連項目  
 [カスタム接続マネージャーのコーディング](coding-a-custom-connection-manager.md)   
 [カスタム接続マネージャー用ユーザー インターフェイスの開発](developing-a-user-interface-for-a-custom-connection-manager.md)  
  
  
