---
title: SQL ライター サービス | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- VDI [SQL Server]
- restoring [SQL Server], SQL Writer Service
- backups [SQL Server], while SQL Server running
- Volume Shadow Copy Service
- volume backups while running [SQL Server]
- Virtual Backup Device Interface [SQL Server]
- SQL Writer Service
- services [SQL Server], SQL Writer
- MSDE Writer
- VSS
ms.assetid: 0f299867-f499-4c2a-ad6f-b2ef1869381d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 79b0ba2bad207b92e0227ed5c8d3999dab335df6
ms.sourcegitcommit: ffb87aa292fc9b545c4258749c28df1bd88d7342
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2019
ms.locfileid: "71816672"
---
# <a name="sql-writer-service"></a>SQL ライター サービス
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL ライター サービスは、ボリューム シャドウ コピー サービス フレームワークを通じて、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバックアップと復元に関する追加機能を提供します。  
  
 SQL ライター サービスは、自動的にインストールされます。 SQL ライター サービスは、ボリューム シャドウ コピー サービス (VSS) アプリケーションがバックアップまたは復元を要求したときに動作している必要があります。 SQL ライター サービスを構成するには、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows サービス アプレットを使用します。 SQL ライター サービスは、すべてのオペレーティング システムにインストールできます。  
  
## <a name="purpose"></a>用途  
 SQL ライター サービスが実行されている場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] はデータ ファイルをロックして排他アクセス権を取得します。 SQL ライター サービスが実行されていない場合、Windows で実行中のバックアップ プログラムはデータ ファイルにアクセスできないため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバックアップ機能を使用してバックアップを実行する必要があります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の実行中に Windows のバックアップ プログラムが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ ファイルをコピーできるようにするには、SQL ライター サービスを使用します。  
  
## <a name="volume-shadow-copy-service"></a>ボリューム シャドウ コピー サービス  
 VSS は、システム上のアプリケーションがボリュームへの書き込みを続行している間に、ボリューム バックアップを実行できるようにするためのフレームワークとなる COM API セットです。 VSS には、一貫性のあるインターフェイスが用意されており、ディスク上のデータを更新するユーザー アプリケーション (ライター) とアプリケーションをバックアップするユーザー アプリケーション (リクエスター) 間の連携が可能になります。  
  
 VSS は、実行中のシステム (特にサーバー) で提供されているサービスのパフォーマンスや安定性を必要以上に低下させることなく、これらのシステム上で安定したバックアップ イメージをキャプチャしてコピーします。 VSS の詳細については、Windows ドキュメントを参照してください。  

> [!NOTE]
> VSS を使用して、基本的な可用性グループをホストしている仮想マシンをバックアップする際に、その仮想マシンがセカンダリ状態にあるデータベースを現在ホストしている場合、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 CU2 および [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU9 以降では、これらのデータベースは仮想マシンと共にバックアップ*されません*。  この理由は、基本的な可用性グループではセカンダリ レプリカ上にあるデータベースのバックアップがサポートされていないためです。  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のこれらのバージョン以前では、バックアップはエラーとなって失敗します。
  
## <a name="virtual-backup-device-interface-vdi"></a>Virtual Backup Device Interface (VDI)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、Virtual Backup Device Interface (VDI) と呼ばれる API が用意されています。これにより、独立系ソフトウェア ベンダーは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を独自の製品に統合して、バックアップおよび復元操作のサポートを提供できます。 これらの API は、最高の信頼性とパフォーマンスを提供するほか、ホット バックアップ機能やスナップショット バックアップ機能など、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のあらゆるバックアップおよび復元機能をサポートするように設計されています。 サードパーティ ベンダーのアプリケーションからスナップショット (VSS) バックアップが要求された場合、SQL ライター サービスでは、実際のバックアップを実行するために VDI API 関数が呼び出されます。 VDI API は VSS から独立しているため、VSS API を採用していないソフトウェア ソリューションで頻繁に使用されることに注意してください。
  
## <a name="permissions"></a>アクセス許可  
 SQL ライター サービスは、 **ローカル システム** アカウントで実行する必要があります。 SQL ライター サービスは、 **に接続するために** NT Service\SQLWriter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインを使用します。 **NT Service\SQLWriter** ログインを使用すると、SQL ライター プロセスは **ログインなし**と指定されたアカウントを通じた低い特権レベルで実行され、その結果、脆弱性を制限することになります。 SQL ライター サービスが無効になっている場合は、System Center Data Protection Manager や他のいくつかのサード パーティ製品のように VSS スナップショットに依存する任意のユーティリティは動作に失敗するか、より悪い場合は、一貫性のないデータベースのバックアップを取得するリスクが生じます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を実行するシステムと、ホスト システム (仮想マシンの場合) のどちらも、 [!INCLUDE[tsql](../../includes/tsql-md.md)] によるバックアップのみを必要とし、それ以外のバックアップを何も必要としない場合は、SQL ライター サービスを無効にしてログインを削除しても安全です。  バックアップが直接的なスナップショット ベースであるかどうかにかかわりなく、SQL ライター サービスはシステム レベルとボリューム レベルどちらのバックアップからも開始できることに注意してください。 いくつかのシステム バックアップ製品は、開いているファイルやロックされているファイルがブロックされることを防止するために VSS を使用します。 SQL ライター サービスは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのすべての I/O を短時間にわたって停止するため、自らが動作する目的で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内で昇格された権限を必要とします。  
  
## <a name="features"></a>[機能]  
 SQL ライターは次の機能をサポートしています。  
  
-   フルテキスト カタログなど、データベースの完全バックアップおよび復元  
  
-   差分バックアップおよび復元  
  
-   移動を伴う復元  
  
-   データベースの名前変更  
  
-   コピーのみのバックアップ  
  
-   データベース スナップショットの自動復旧  
  
 SQL ライターは次の機能をサポートしていません。  
  
-   ログのバックアップ  
  
-   ファイルとファイル グループのバックアップ  
  
-   ページ復元  
  
## <a name="remarks"></a>Remarks
SQL ライター サービスは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エンジンとは異なるサービスです。これは、同じサーバー上にあるさまざまなバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] や、さまざまな [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス全体で共有されます。  SQL ライター サービス ファイルは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール パッケージに含まれ、付属する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エンジンと同じバージョン番号が付けられます。  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新しいインスタンスをサーバーにインストールするか、既存のインスタンスをアップグレードするときに、インストールまたはアップグレードするインスタンスのバージョン番号が現在サーバー上にある SQL ライター サービスのバージョン番号よりも大きい場合、そのファイルはインストール パッケージに含まれるファイルに置き換えられます。  サービス パックまたは累積更新プログラムによって SQL ライター サービスが更新されており、RTM バージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールしようとしている場合、インストールがより大きいメジャー バージョン番号を持っていれば、新しいバージョンの SQL ライター サービスを古いバージョンで置き換えることができます。  たとえば、SQL ライター サービスが [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 CU2 で更新されているとします。  そのインスタンスを [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] RTM にアップグレードする場合、更新された SQL ライター サービスは古いバージョンに置き換えられます。  この場合、新しいバージョンの SQL ライター サービスを取得するために、新しいインスタンスに最新の CU を適用する必要があります。

