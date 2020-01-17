---
title: データベース ミラーリング セッションの Windows 認証 (SQL Server Management Studio) を使用して確立 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], sessions
ms.assetid: 7cb418d6-dce1-4a0d-830e-9c5ccfe3bd72
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 70d9b3f9d243531e13d3d5a46693c80288815881
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62806920"
---
# <a name="establish-a-database-mirroring-session-using-windows-authentication-sql-server-management-studio"></a>Windows 認証を使用してデータベース ミラーリング セッションを確立する (SQL Server Management Studio)
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] を使用してください。  
  
 データベース ミラーリング セッションを確立したり、特定のデータベースについてデータベース ミラーリングのプロパティを変更するには、 **[データベースのプロパティ]** ダイアログ ボックスの **[ミラーリング]** ページを使用します。 **[ミラーリング]** ページを使用してデータベース ミラーリングを構成する前に、次の要件を満たしていることをご確認ください。  
  
-   プリンシパル サーバー インスタンスおよびミラー サーバー インスタンスでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の同じエディション (Standard または Enterprise) を実行している必要があります。 また、ワークロードの処理能力が同程度のシステム上で運用することを強くお勧めします。  
  
    > [!NOTE]  
    >  ミラーリング監視サーバー インスタンスは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 エディションでサポートされている機能の一覧については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[機能は、SQL Server 2014 の各エディションでサポートされている](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)します。  
  
-   ミラー データベースが存在し、最新状態である必要があります。  
  
     ミラー データベースを作成するには、ミラー サーバー インスタンス上でプリンシパル データベースの最新のバックアップを (WITH NORECOVERY を使用して) 復元する必要があります。 また、完全バックアップの後に 1 つ以上のログ バックアップを取得し、(WITH NORECOVERY を使用して) これらのバックアップを順にミラー データベースに復元する必要もあります。 詳細については、「 [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)」を参照してください。  
  
-   サーバー インスタンスが別のドメイン ユーザー アカウントで実行されている場合、それぞれに他方のインスタンスの **master** データベースのログインが必要になります。 ログインが存在しない場合は、作成してからミラーリングを構成する必要があります。 詳細については、「 [Windows 認証を使用してデータベース ミラーリング エンドポイントへのネットワーク アクセスを許可する &#40;SQL Server&#41;](../database-mirroring-allow-network-access-windows-authentication.md)」を参照してください。  
  
### <a name="to-configure-database-mirroring"></a>データベース ミラーリングを構成するには  
  
1.  プリンシパル サーバー インスタンスに接続した後、オブジェクト エクスプローラーでサーバー名をクリックして、サーバー ツリーを展開します。  
  
2.  **[データベース]** を展開し、ミラー化するデータベースを選択します。  
  
3.  データベースを右クリックして **[タスク]** を選択し、 **[ミラー]** をクリックします。 **[データベースのプロパティ]** ダイアログ ボックスの **[ミラーリング]** ページが開きます。  
  
4.  ミラーリングの構成を開始するには、 **[セキュリティの構成]** をクリックして、データベース ミラーリング セキュリティ構成ウィザードを起動します。  
  
    > [!NOTE]  
    >  データベース ミラーリング セッションでは、このウィザードだけを使用して、ミラーリング監視サーバー インスタンスを追加または変更できます。  
  
5.  データベース ミラーリング セキュリティ構成ウィザードでは、各サーバー インスタンス上にデータベース ミラーリング エンドポイントが存在しない場合は自動的に作成され、サーバー インスタンスのロールに対応するフィールド ("**プリンシパル**"、" **ミラー**"、または " **ミラーリング監視**") にサーバー ネットワーク アドレスが入力されます。  
  
    > [!IMPORTANT]  
    >  エンドポイントを作成すると、データベース ミラーリング セキュリティ構成ウィザードでは、常に Windows 認証が使用されます。 証明書ベースの認証でウィザードを使用する前に、各サーバー インスタンスで証明書を使用するようにミラーリング エンドポイントを構成しておく必要があります。 また、ウィザードの **[サービス アカウント]** ダイアログ ボックスのフィールドはすべて空のままにしておく必要があります。 証明書を使用するデータベース ミラーリング エンドポイントの作成については、「[CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)」をご覧ください。  
  
6.  必要に応じて、動作モードを変更します。 特定の動作モードの可用性は、ミラーリング監視サーバーの TCP アドレスを指定したかどうかに依存します。 次のオプションがあります。  
  
    |オプション|ミラーリング監視サーバー|説明|  
    |------------|--------------|-----------------|  
    |**[高パフォーマンス (非同期)]**|Null (存在しても使用されませんが、セッションにクォーラムが必要になります)|最適なパフォーマンスを提供するために、ミラー データベースが常にプリンシパル データベースから多少遅延されます。完全に時間差がなくなることはありません。 ただし、データベース間の時間差は、通常はわずかです。 パートナーの損失による影響は次のとおりです。<br /><br /> ミラー サーバー インスタンスが使用できなくなった場合は、引き続きプリンシパル サーバー インスタンスが使用されます。<br /><br /> プリンシパル サーバー インスタンスが使用できなくなると、ミラー サーバー インスタンスは停止しますが、セッションにミラーリング監視サーバーがない場合 (推奨) やミラーリング監視サーバーがミラー サーバーに接続されている場合、ミラー サーバーはウォーム スタンバイとしてアクセスできます。つまり、データベース所有者は、ミラー サーバー インスタンスにサービスを強制できます (データ損失の可能性があります)。<br /><br /> <br /><br /> 詳細については、「 [データベース ミラーリング セッション中の役割の交代 &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)をダウンロードしてください。|  
    |**[自動フェールオーバーを伴わない高い安全性 (同期)]**|いいえ|コミットされているすべてのトランザクションは、ミラー サーバー上のディスクに書き込まれることが保証されています。<br /><br /> パートナーが相互に接続され、データベースが同期されると、手動フェールオーバーを開始できます。 パートナーの損失による影響は次のとおりです。<br /><br /> ミラー サーバー インスタンスが使用できなくなった場合は、引き続きプリンシパル サーバー インスタンスが使用されます。<br /><br /> プリンシパル サーバー インスタンスが使用できなくなると、ミラー サーバー インスタンスは停止しますが、ウォーム スタンバイとしてアクセスできます。データベース所有者は、ミラー サーバー インスタンスにサービスを強制できます (データ損失の可能性があります)。<br /><br /> 詳細については、「 [データベース ミラーリング セッション中の役割の交代 &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)のすべてのエディションで使用できるわけではありません。|  
    |**[自動フェールオーバーを伴う高い安全性 (同期)]**|指定あり (必須)|コミットされているすべてのトランザクションは、ミラー サーバー上のディスクに書き込まれることが保証されています。 自動フェールオーバーをサポートするミラーリング監視サーバー インスタンスを含めることによって、可用性は最大限に高まります。 **[自動フェールオーバーを伴う高い安全性 (同期)]** オプションを選択できるのは、最初にミラーリング監視サーバーのアドレスを指定した場合のみです。 パートナーが相互に接続され、データベースが同期されると、手動フェールオーバーを開始できます。<br /><br /> ミラーリング監視サーバーが存在する場合、パートナーの損失による影響は次のとおりです。<br /><br /> -プリンシパル サーバー インスタンスが使用できなくなった場合は、自動フェールオーバーが発生します。 ミラー サーバー インスタンスはプリンシパル サーバー インスタンスの役割に切り替わり、ミラー データベースがプリンシパル データベースとして提供されます。<br /><br /> -ミラー サーバー インスタンスが使用できなくなった場合は、プリンシパルが続行されます。<br /><br /> 詳細については、「 [データベース ミラーリング セッション中の役割の交代 &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)をダウンロードしてください。<br /><br /> **\*\* 重要 \*\*** ミラーリング監視サーバーが切断された場合、データベースを使用できるようにするには、パートナーが相互に接続されている必要があります。 詳細については、「[クォーラム: データベースの可用性にミラーリング監視サーバーが与える影響 (データベース ミラーリング)](quorum-how-a-witness-affects-database-availability-database-mirroring.md)」を参照してください。|  
  
7.  次のすべての条件に当てはまる場合は、 **[ミラーリングの開始]** をクリックしてミラーリングを開始します。  
  
    -   現在プリンシパル サーバー インスタンスに接続されています。  
  
    -   セキュリティが正しく構成されています。  
  
    -   プリンシパル サーバー インスタンスとミラー サーバー インスタンスの完全修飾 TCP アドレスが、( **[サーバー ネットワーク アドレス]** セクションで) 指定されています。  
  
    -   動作モードが **[自動フェールオーバーを伴う高い安全性 (同期)]** に設定されている場合、ミラーリング監視サーバー インスタンスの完全修飾 TCP アドレスも指定されています。  
  
8.  ミラーリングが開始された後でも、動作モードを変更して **[OK]** をクリックすることで変更を保存できます。 自動フェールオーバーを伴う高い安全性モードに切り替えることができるのは、先にミラーリング監視サーバーのアドレスを指定した場合のみです。  
  
    > [!NOTE]  
    >  ミラーリング監視サーバーを削除するには、 **[ミラーリング監視]** フィールドからそのサーバー ネットワーク アドレスを削除します。 自動フェールオーバーを伴う高い安全性モードから高パフォーマンス モードに切り替えると、 **[ミラーリング監視]** フィールドの内容は自動的に消去されます。  
  
## <a name="see-also"></a>関連項目  
 [データベース ミラーリング セッション中の役割の交代 &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)   
 [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)   
 [データベース プロパティ &#40;[ミラーリング] ページ&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [データベース ミラーリング セッションを一時停止または再開する &#40;SQL Server&#41;](pause-or-resume-a-database-mirroring-session-sql-server.md)   
 [TRUSTWORTHY プロパティを使用するようにミラー データベースを設定する方法 &#40;Transact-SQL&#41;](set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md)   
 [データベース ミラーリングを削除する &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [役割の交代後のログインとジョブの管理 &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)   
 [データベース ミラーリングの設定 &#40;SQL Server&#41;](setting-up-database-mirroring-sql-server.md)   
 [データベースを別のサーバー インスタンスで使用できるようにするときのメタデータの管理 &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)   
 [データベース ミラーリング監視サーバーを追加または置き換える方法 &#40;SQL Server Management Studio&#41;](../database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
  
