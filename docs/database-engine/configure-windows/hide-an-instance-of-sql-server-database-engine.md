---
title: SQL Server データベース エンジンのインスタンスの非表示 | Microsoft Docs
ms.custom: ''
ms.date: 08/19/2015
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], hiding instances
- hiding instances of Database Engine
ms.assetid: 392de21a-57fa-4a69-8237-ced8ca86ed1d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 28d7a01ce3c11ce332de7e7af70ff0c57746e840
ms.sourcegitcommit: 445842da7c7d216b94a9576e382164c67f54e19a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "71682099"
---
# <a name="hide-an-instance-of-sql-server-database-engine"></a>SQL Server データベース エンジンのインスタンスの非表示
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、SQL Server 構成マネージャーを使用して [!INCLUDE[ssDE](../../includes/ssde-md.md)] で [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のインスタンスを非表示にする方法について説明します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスを使用して、コンピューターにインストールされている [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスを列挙します。 この機能により、クライアント アプリケーションはサーバーを参照できるようになり、クライアントは、同じコンピューター上にある [!INCLUDE[ssDE](../../includes/ssde-md.md)] の複数のインスタンスを区別できるようになります。 次の手順に従い、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] [参照] **ボタンを使用してこの** インスタンスを表示しようとするクライアント コンピューターに対して、SQL Server Browser サービスがそのインスタンスを公開しないようにできます。  
  
##  <a name="SSMSProcedure"></a> SQL Server 構成マネージャーの使用  
  
#### <a name="to-hide-an-instance-of-the-sql-server-database-engine"></a>SQL Server データベース エンジンのインスタンスを非表示にするには  
  
1.  **SQL Server 構成マネージャー**で、 **[SQL Server ネットワークの構成]** を展開し、 *\<server instance>* の**プロトコル**を右クリックします。次に **[プロパティ]** を選びます。  
  
2.  **[フラグ]** タブで **[HideInstance]** ボックスの一覧の **[はい]** を選択し、 **[OK]** をクリックしてダイアログ ボックスを閉じます。 この変更は、新しい接続ですぐに有効になります。  
  
## <a name="remarks"></a>Remarks  
 名前付きインスタンスを非表示にする場合、ブラウザー サービスが実行中でも、非表示のインスタンスに接続するための接続文字列でポート番号を提供する必要があります。 名前付きの非表示のインスタンスに対しては、動的ポートではなく静的ポートを利用することをお勧めします。  
  詳細については、「[特定の TCP ポートで受信待ちするようにサーバーを構成する方法 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)」を参照してください。  
  
### <a name="clustering"></a>クラスター  
 クラスター化されたインスタンスまたは可用性グループ名を非表示にすると、クラスター サービスが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続できないことがあります。 これにより、クラスター インスタンスの **IsAlive** のチェックが失敗し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がオフラインになります。 
 
これを回避するには、インスタンス用に構成した静的ポートを反映するように、クラスター化されたインスタンスのすべてのノードまたは可用性グループ レプリカをホストするすべてのインスタンスに別名を作成します。  たとえば、2 つのレプリカを持つ可用性グループでは、`node-two\instancename` のように、ノード 1 にノード 2 インスタンスの別名を作成します。 ノード 2 で、`node-one\instancename` という別名を作成します。 フェールオーバーを正常に行うには、別名が必要です。 
 
 詳細については、「[クライアントが使用するサーバーの別名の作成または削除 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)」を参照してください。  
  
 クラスター化された名前付きインスタンスを非表示にすると、**LastConnect** レジストリ キー (**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI11.0\LastConnect**) のポートが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のリッスンしているポートと異なる場合、クラスター サービスは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続できなくなる可能性があります。 クラスター サービスが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続できない場合、次のようなエラーが表示されることがあります:  
**イベント ID:1001:イベント名:フェールオーバー クラスタリング リソース デッドロック。**  
  
## <a name="see-also"></a>参照  
 [サーバー ネットワークの構成](../../database-engine/configure-windows/server-network-configuration.md)   
 [SQL 仮想サーバーのクライアント接続の説明](https://support.microsoft.com/kb/273673)   
 [SQL Server 名前付きインスタンスに静的ポートを割り当て、一般的な落とし穴を回避する方法](https://blogs.msdn.com/b/arvindsh/archive/2012/09/08/how-to-assign-a-static-port-to-a-sql-server-named-instance-and-avoid-a-common-pitfall.aspx)  
  
  
