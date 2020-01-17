---
title: サーバーのプロパティ ([データベースの設定] ページ) | Microsoft Docs
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.databasesettings.f1
ms.assetid: 1cebdbd3-cbfd-4a02-bba6-a5addf4e3ada
author: MikeRayMSFT
ms.author: mikeray
ms.custom: ''
ms.date: 05/23/2019
ms.openlocfilehash: bdefcbbfe6d5987de4ac69ab60d1e80b004a5db6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68025455"
---
# <a name="server-properties---database-settings-page"></a>サーバーのプロパティ - [データベースの設定] ページ

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このページを使用すると、データベースの設定を表示したり、変更したりできます。  
  
## <a name="options"></a>オプション

### <a name="default-index-fill-factor"></a>[既定のインデックス FILL FACTOR]

既存のデータを使用して新しいインデックスを作成する際に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 全体で各ページを作成する方法を指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では各ページを埋めるときにページの分割に時間がかかるため、FILL FACTOR で指定する割合はパフォーマンスに影響します。
  
既定値は 0 です。有効な値の範囲は 0 ～ 100 です。 FILL FACTOR が 0 または 100 の場合、クラスター化インデックスと完全なデータ ページ、および非クラスター化インデックスと完全なリーフ ページが作成されますが、インデックス ツリーの上位レベルにはスペースが少し残されます。 FILL FACTOR 値 0 と 100 は、すべての面でまったく同じ結果になります。
  
FILL FACTOR の値を小さくすると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でのインデックスの作成時に充てん率の低いページが数多く作成されます。 各インデックスに必要な保存領域が大きくなりますが、以降の挿入に使用できる領域は大きくなり、ページ分割は不要になります。
  
### <a name="wait-indefinitely"></a>[ロードされるまで待つ]

新しいバックアップ テープが用意されるまでの間、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がタイムアウトしないように指定します。  

### <a name="try-once"></a>[一度だけ再試行する]

バックアップ テープが必要なときに使用できない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がタイムアウトするように指定します。

### <a name="try-for-minutes"></a>[試行期間]

指定された時間内にバックアップ テープが使用できなかった場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がタイムアウトするように指定します。  

### <a name="default-backup-media-retention-in-days"></a>[バックアップ メディアの既定の保有期間 (日)]

データベースまたはトランザクション ログのバックアップに使用した各バックアップ メディアの保有期間を日数で指定します。ここで指定した日数は、システム全体での保有期間の既定値になります。 このオプションを利用して、指定した日数が経過するまでバックアップが上書きされないように保護できます。  

#### <a name="compress-backup"></a>[バックアップを圧縮する]

[!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (またはそれ以降のバージョン) での、 **backup compression default** オプションの現在の設定を示します。 このオプションによって、バックアップの圧縮についてのサーバー レベルの既定値が次のように決定されます。

- **[バックアップを圧縮する]** チェック ボックスがオフの場合、既定では新しいバックアップは圧縮されません。

- **[バックアップを圧縮する]** チェック ボックスがオンの場合、既定で新しいバックアップが圧縮されます。
  
    > [!IMPORTANT]
    >  既定の設定では、圧縮によって CPU 使用率が著しく増加し、圧縮処理によって CPU がさらに消費されるために、同時に実行される操作が悪影響を受ける場合があります。 このため、 [リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)によって CPU 使用率が制限されるセッションでは、優先度の低い圧縮バックアップを作成することができます。 詳細については、[「リソース ガバナーを使用してバックアップの圧縮による CPU 使用率を制限する方法 &#40;Transact-SQL&#41;」](../.. relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)を参照してください。
  
**sysadmin** 固定サーバー ロールまたは **serveradmin** 固定サーバー ロールのメンバーである場合は、 **[バックアップを圧縮する]** ボックスをオンにして設定を変更できます。  
  
詳細については、「[backup compression default サーバー構成オプションの表示または構成](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)」および「[バックアップの圧縮 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md)」を参照してください。  

#### <a name="backup-checksum"></a>バックアップのチェックサム

このオプションを使用すると、"*バックアップ チェックサムの既定値*" に対する sp_configure の設定を切り替えることができます。 この機能により、バックアップ チェックサムの既定値を簡単に有効にできるようになります。

### <a name="recovery-interval-minutes"></a>[復旧間隔 (分単位)]

データベースごとに、データベースの復旧にかける最長時間を分単位で設定します。 既定値は 0 です。0 の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によって自動的に構成されます。 実際には、復旧時間が 1 分未満で、アクティブなデータベースのチェックポイントは約 1 分間隔になります。 詳細については、「 [recovery interval サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)」を参照してください。  
  
### <a name="data"></a>data

データ ファイルの既定の位置を指定します。 参照ボタンをクリックして、新しい既定の位置を指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再起動するまでは、有効になりません。  
  
### <a name="log"></a>Log
  
ログ ファイルの既定の位置を指定します。 参照ボタンをクリックして、新しい既定の位置を指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再起動するまでは、有効になりません。  
  
### <a name="configured-values"></a>構成した値

このペインの各オプションに構成されている値を表示します。 これらの値を変更した場合は、 **[実行中の値]** をクリックして、変更後の値が反映されているかどうかを確認してください。 そうなっていない場合は、先に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを再指定する必要があります。  
  
### <a name="running-values"></a>実行中の値

このペイン上のオプションの、現在実行中の値を表示します。 これらの値は読み取り専用です。  
  
## <a name="see-also"></a>参照

- [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)

- [インデックスの FILL FACTOR の指定](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)