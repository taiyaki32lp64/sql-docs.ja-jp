---
title: サーバーのプロパティ ([データベースの設定] ページ) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.serverproperties.databasesettings.f1
ms.assetid: 1cebdbd3-cbfd-4a02-bba6-a5addf4e3ada
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 21731b1b99c29257700393b5b7713a723c35dbac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62809534"
---
# <a name="server-properties-database-settings-page"></a>[サーバーのプロパティ] ([データベースの設定] ページ)
  このページを使用すると、データベースの設定を表示したり、変更したりできます。  
  
## <a name="options"></a>および  
 **[既定のインデックス FILL FACTOR]**  
 既存のデータを使用して新しいインデックスを作成する際に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 全体で各ページを作成する方法を指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では各ページを埋めるときにページの分割に時間がかかるため、FILL FACTOR で指定する割合はパフォーマンスに影響します。  
  
 既定値は 0 です。有効な値の範囲は 0 ～ 100 です。 FILL FACTOR が 0 または 100 の場合、クラスター化インデックスと完全なデータ ページ、および非クラスター化インデックスと完全なリーフ ページが作成されますが、インデックス ツリーの上位レベルにはスペースが少し残されます。 FILL FACTOR 値 0 と 100 は、すべての面でまったく同じ結果になります。  
  
 FILL FACTOR の値を小さくすると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でのインデックスの作成時に充てん率の低いページが数多く作成されます。 各インデックスに必要な保存領域が大きくなりますが、以降の挿入に使用できる領域は大きくなり、ページ分割は不要になります。  
  
 **[ロードされるまで待つ]**  
 新しいバックアップ テープが用意されるまでの間、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がタイムアウトしないように指定します。  
  
 **[一度だけ再試行する]**  
 バックアップ テープが必要なときに使用できない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がタイムアウトするように指定します。  
  
 **[試行期間]**  
 指定された時間内にバックアップ テープが使用できなかった場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がタイムアウトするように指定します。  
  
 **[バックアップ メディアの既定の保有期間 (日)]**  
 データベースまたはトランザクション ログのバックアップに使用した各バックアップ メディアの保有期間を日数で指定します。ここで指定した日数は、システム全体での保有期間の既定値になります。 このオプションを利用して、指定した日数が経過するまでバックアップが上書きされないように保護できます。  
  
 **[バックアップを圧縮する]**  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (またはそれ以降のバージョン) での、 **backup compression default** オプションの現在の設定を示します。 このオプションによって、バックアップの圧縮についてのサーバー レベルの既定値が次のように決定されます。  
  
-   **[バックアップを圧縮する]** チェック ボックスがオフの場合、既定では新しいバックアップは圧縮されません。  
  
-   **[バックアップを圧縮する]** チェック ボックスがオンの場合、既定で新しいバックアップが圧縮されます。  
  
    > [!IMPORTANT]  
    >  既定の設定では、圧縮によって CPU 使用率が著しく増加し、圧縮処理によって CPU がさらに消費されるために、同時に実行される操作が悪影響を受ける場合があります。 このため、 [リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)によって CPU 使用率が制限されるセッションでは、優先度の低い圧縮バックアップを作成することができます。 詳細については、[「リソース ガバナーを使用してバックアップの圧縮による CPU 使用率を制限する方法 &#40;Transact-SQL&#41;」](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)を参照してください。  
  
 **sysadmin** 固定サーバー ロールまたは **serveradmin** 固定サーバー ロールのメンバーである場合は、 **[バックアップを圧縮する]** ボックスをオンにして設定を変更できます。  
  
 詳細については、「[backup compression default サーバー構成オプションの表示または構成](view-or-configure-the-backup-compression-default-server-configuration-option.md)」および「[バックアップの圧縮 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md)」を参照してください。  
  
 **[復旧間隔 (分単位)]**  
 データベースごとに、データベースの復旧にかける最長時間を分単位で設定します。 既定値は 0 です。0 の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によって自動的に構成されます。 実際には、復旧時間が 1 分未満で、アクティブなデータベースのチェックポイントは約 1 分間隔になります。 詳細については、「 [recovery interval サーバー構成オプションの構成](configure-the-recovery-interval-server-configuration-option.md)」を参照してください。  
  
 **Data**  
 データ ファイルの既定の位置を指定します。 参照ボタンをクリックして、新しい既定の位置を指定します。 変更内容を有効にするには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再起動する必要があります。  
  
 **Log**  
 ログ ファイルの既定の位置を指定します。 参照ボタンをクリックして、新しい既定の位置を指定します。 変更内容を有効にするには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再起動する必要があります。  
  
 **[構成した値]**  
 このペインの各オプションに構成されている値を表示します。 これらの値を変更した場合は、 **[実行中の値]** をクリックして、変更後の値が反映されているかどうかを確認してください。 値が反映されていない場合、先に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを再指定する必要があります。  
  
 **[実行中の値]**  
 このペイン上のオプションの、現在実行中の値を表示します。 これらの値は読み取り専用です。  
  
## <a name="see-also"></a>参照  
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [インデックスの FILL FACTOR の指定](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)  
  
  
