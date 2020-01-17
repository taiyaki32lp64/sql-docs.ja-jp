---
title: SQL Server データベース エンジンのインスタンスの非表示 | Microsoft Docs
ms.custom: ''
ms.date: 08/19/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], hiding instances
- hiding instances of Database Engine
ms.assetid: 392de21a-57fa-4a69-8237-ced8ca86ed1d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 631d55e1f8921601f25f2b2d8a14f00d11bd0947
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62782007"
---
# <a name="hide-an-instance-of-sql-server-database-engine"></a>SQL Server データベース エンジンのインスタンスの非表示
  このトピックでは、SQL Server 構成マネージャーを使用して [!INCLUDE[ssDE](../../includes/ssde-md.md)] で [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のインスタンスを非表示にする方法について説明します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスを使用して、コンピューターにインストールされている [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスを列挙します。 この機能により、クライアント アプリケーションはサーバーを参照できるようになり、クライアントは、同じコンピューター上にある [!INCLUDE[ssDE](../../includes/ssde-md.md)] の複数のインスタンスを区別できるようになります。 次の手順に従い、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] [参照] **ボタンを使用してこの** インスタンスを表示しようとするクライアント コンピューターに対して、SQL Server Browser サービスがそのインスタンスを公開しないようにできます。  
  
##  <a name="SSMSProcedure"></a> SQL Server 構成マネージャーの使用  
  
#### <a name="to-hide-an-instance-of-the-sql-server-database-engine"></a>SQL Server データベース エンジンのインスタンスを非表示にするには  
  
1.  **SQL Server 構成マネージャー**で、 **[SQL Server ネットワークの構成]** を展開し、 *\<server instance>* の**プロトコル**を右クリックします。次に **[プロパティ]** を選びます。  
  
2.  **[フラグ]** タブで **[HideInstance]** ボックスの一覧の **[はい]** を選択し、 **[OK]** をクリックしてダイアログ ボックスを閉じます。 この変更は、新しい接続ですぐに有効になります。  
  
## <a name="remarks"></a>コメント  
 名前付きインスタンスを非表示にする場合、ブラウザー サービスが実行中でも、非表示のインスタンスに接続するための接続文字列でポート番号を提供する必要があります。 名前付きの非表示のインスタンスに対しては、動的ポートではなく静的ポートを利用することをお勧めします。  
  詳細については、「[特定の TCP ポートで受信待ちするようにサーバーを構成する方法 &#40;SQL Server 構成マネージャー&#41;](configure-a-server-to-listen-on-a-specific-tcp-port.md)」を参照してください。  
  
### <a name="clustering"></a>クラスター  
 クラスター化された名前付きインスタンスを非表示にすると、クラスター サービスは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続できないことがあります。 これにより、クラスター インスタンスの **IsAlive** のチェックが失敗し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がオフラインになります。 インスタンス用に構成した静的ポートを反映するように、クラスター化されたインスタンスのすべてのノードで別名を作成することをお勧めします。  
 詳細については、「[クライアントが使用するサーバーの別名の作成または削除 &#40;SQL Server 構成マネージャー&#41;](create-or-delete-a-server-alias-for-use-by-a-client.md)」を参照してください。  
  
 クラスター化された名前付きインスタンスを非表示にすると、**LastConnect** レジストリ キー (**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI11.0\LastConnect**) のポートが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のリッスンしているポートと異なる場合、クラスター サービスは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続できなくなる可能性があります。 クラスター サービスが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続できない場合、次のようなエラーが表示されることがあります:  
**イベント ID:1001:イベント名:フェールオーバー クラスタ リング リソース デッドロックします。**  
  
## <a name="see-also"></a>関連項目  
 [サーバー ネットワークの構成](server-network-configuration.md)   
 [SQL 仮想サーバーのクライアント接続の説明](https://support.microsoft.com/kb/273673)   
 [SQL Server 名前付きインスタンスに静的ポートを割り当て、一般的な落とし穴を回避する方法](https://blogs.msdn.com/b/arvindsh/archive/2012/09/08/how-to-assign-a-static-port-to-a-sql-server-named-instance-and-avoid-a-common-pitfall.aspx)  
  
  
