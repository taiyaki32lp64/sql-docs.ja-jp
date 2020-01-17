---
title: Azure 仮想マシンにインストールする
description: Azure クラウドの SQL Server 仮想マシンで、R と Python のデータ サイエンス ソリューションおよび機械学習ソリューションを実行できます。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/09/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: aeec25b561822e8083b89e03f0f7e74f40660f7b
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727616"
---
# <a name="install-sql-server-machine-learning-services-with-r-and-python-on-an-azure-virtual-machine"></a>Azure 仮想マシンに R および Python を使用した SQL Server Machine Learning Services をインストールする
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Azure の SQL Server 仮想マシンに、Machine Learning Services と R および Python の統合をインストールできます。これにより、インストールと構成のタスクが不要になります。 仮想マシンがデプロイされると、機能を使用する準備が整います。
 
詳細な手順については、「[Azure portal で Windows SQL Server 仮想マシンをプロビジョニングする方法](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision)」を参照してください。

「[SQL Server 設定の構成](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#3-configure-sql-server-settings)」ステップで、インスタンスに機械学習を追加します。

<a name="firewall"></a>

## <a name="unblock-the-firewall"></a>ファイアウォールのブロックを解除する

既定では、Azure 仮想マシン上のファイアウォールには、ローカル ユーザー アカウントのネットワーク アクセスをブロックする規則が含まれます。

リモートのデータ サイエンス クライアントから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスにアクセスできるようにするために、この規則を無効にする必要があります。  このようにしないと、仮想マシンのワークスペースを使用するコンピューティング コンテキストで機会学習コードを実行できなくなります。

リモートのデータ サイエンス クライアントからのアクセスを有効にするには、次の手順に従います。

1. 仮想マシン で、[セキュリティが強化された Windows ファイアウォール] を開きます。
2. **[送信の規則]** を選択します
3. 次の規則を無効にします。
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
## <a name="enable-odbc-callbacks-for-remote-clients"></a>リモート クライアントの ODBC コールバックを有効にする

サーバーを呼び出すクライアントから、機械学習ソリューションの一部として ODBC クエリを発行する必要がある場合は、リモート クライアントの代わりに Launchpad から ODBC 呼び出しを実行できるようにする必要があります。 

これを行うには、スタート パッドによって使用される SQL ワーカー アカウントがインスタンスにログインするできるようにする必要があります。 詳細については、[データベース ユーザーとしての SQLRUserGroup の追加](../security/create-a-login-for-sqlrusergroup.md)に関する記事を参照してください。

<a name="network"></a>

## <a name="add-network-protocols"></a>ネットワーク プロトコルを追加する

+ 名前付きパイプを有効にする
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] では、クライアントとサーバー コンピューター間の接続 (および一部の内部接続) に、名前付きパイプ プロトコルが使用されます。 名前付きパイプが有効になっていない場合は、Azure 仮想マシンと、サーバーに接続するデータ サイエンス クライアントの両方に名前付きパイプをインストールし、有効化する必要があります。
  
+ TCP/IP を有効にする

  TCP/IP は、ループバック接続に必要です。 "DBNETLIB; SQL Server が存在しないか、アクセスが拒否されました" というエラーが発生した場合、インスタンスをサポートする仮想マシンで TCP/IP を有効にしてください。