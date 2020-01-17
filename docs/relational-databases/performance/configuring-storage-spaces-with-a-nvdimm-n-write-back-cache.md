---
title: 記憶域の構成 - NVDIMM-N ライト バック キャッシュ
ms.custom: seo-dt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 861862fa-9900-4ec0-9494-9874ef52ce65
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: e19b164b0efe6d92a9bae0e6f7362ac5fd56f202
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165986"
---
# <a name="configuring-storage-spaces-with-a-nvdimm-n-write-back-cache"></a>NVDIMM-N ライトバック キャッシュを使った記憶域スペースの構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Windows Server 2016 は、超高速の入出力 (I/O) 操作を可能にする NVDIMM-N デバイスをサポートします。 そのようなデバイスを使用する魅力的な方法の 1 つは、書き込みの低待機時間を実現するためのライトバック キャッシュです。 このトピックでは、ミラー化された NVDIMM-N ライトバック キャッシュを使用して、SQL Server トランザクション ログを格納するための仮想ドライブとしてミラー化された記憶域スペースをセットアップする方法について説明します。 この記憶域スペースをデータ テーブルまたは他のデータを格納するためにも活用する場合は、記憶域プールにディスクを追加するか、分離が重要な場合は複数のプールを作成します。  
  
 この手法を使用して Channel 9 のビデオを視聴するには、「 [Windows Server 2016 でブロック記憶域として不揮発性メモリ (NVDIMM-N) を使用する](https://channel9.msdn.com/Events/Build/2016/P466)」をご覧ください。  
  
## <a name="identifying-the-right-disks"></a>適切なディスクを識別する  
 特に高度な機能 (ライトバック キャッシュなど) を使用した Windows Server 2016 の記憶域スペースのセットアップは、PowerShell で最も簡単に達成できます。 最初の手順として、仮想ディスクが作成される記憶域スペース プールの一部とする必要のあるディスクを識別します。 NVDIMM-N には、メディア型とバス型の SCM (記憶域クラス メモリ) があります。これらについては、Get-PhysicalDisk PowerShell コマンドレットを使用してクエリを実行できます。  
  
```  
Get-PhysicalDisk | Select FriendlyName, MediaType, BusType  
```  
  
 ![Get-PhysicalDisk](../../relational-databases/performance/media/get-physicaldisk.png "Get-PhysicalDisk")  
  
> [!NOTE]  
>  NVDIMM-N デバイスを使用すると、ライトバック キャッシュの対象になるデバイスを具体的に選択する必要がなくなります。  
  
 ミラー化されたライトバック キャッシュを使用してミラー化された仮想ディスクを構築するには、少なくとも 2 つの NVDIMM-N に加えて他の 2 つのディスクが必要です。 プールの構築前に、必要な物理ディスクを変数に割り当てることによって、処理が簡単になります。  
  
```  
$pd =  Get-PhysicalDisk | Select FriendlyName, MediaType, BusType | WHere-Object {$_.FriendlyName -like 'MK0*' -or $_.FriendlyName -like '2c80*'}  
```  
  
 このスクリーンショットには、$pd 変数と、2 つの SSD および 2 つの NVDIMM-N が示されています。これらは、次の PowerShell コマンドレットを使用して戻り値に割り当てられます。  
  
```  
$pd | Select FriendlyName, MediaType, BusType  
```  
  
 ![Select FriendlyName](../../relational-databases/performance/media/select-friendlyname.png "Select FriendlyName")  
  
## <a name="creating-the-storage-pool"></a>記憶域プールの作成  
 PhysicalDisks を含む $pd 変数を使用すると、New-StoragePool PowerShell コマンドレットを使用して記憶域プールを構築するのが容易になります。  
  
```  
New-StoragePool -StorageSubSystemFriendlyName "Windows Storage*" -FriendlyName NVDIMM_Pool -PhysicalDisks $pd  
```  
  
 ![New-StoragePool](../../relational-databases/performance/media/new-storagepool.png "New-StoragePool")  
  
## <a name="creating-the-virtual-disk-and-volume"></a>仮想ディスクとボリュームの作成  
 プールが作成されたら、次に仮想ディスクを切り出して、書式設定します。 次のケースでは、仮想ディスクは 1 つだけ作成され、New-Volume PowerShell コマンドレットを使用してこのプロセスを効率化することができます。  
  
```  
New-Volume -StoragePool (Get-StoragePool -FriendlyName NVDIMM_Pool) -FriendlyName Log_Space -Size 300GB -FileSystem NTFS -AccessPath S: -ResiliencySettingName Mirror  
```  
  
 ![New-Volume](../../relational-databases/performance/media/new-volume.png "New-Volume")  
  
 仮想ディスクが作成、初期化され、NTFS でフォーマットされます。 次の画面キャプチャは、サイズが 300 GB で、書き込みキャッシュが 1 GB であり、NVDIMM-N でホストされることを示しています。  
  
 ![Get-VirtualDisk](../../relational-databases/performance/media/get-virtualdisk.png "Get-VirtualDisk")  
  
 サーバーで表示されるこの新しいボリュームが確認できるようになりました。 SQL Server トランザクション ログに対してこのドライブを使用できます。  
  
 ![Log_Space ドライブ](../../relational-databases/performance/media/log-space-drive.png "Log_Space ドライブ")  
  
## <a name="see-also"></a>参照  
 [Windows 10 の Windows 記憶域スペース](https://windows.microsoft.com/windows-10/storage-spaces-windows-10)   
 [Windows 2012 R2 の Windows 記憶域スペース](https://technet.microsoft.com/library/hh831739.aspx)   
 [トランザクション ログ &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [データ ファイルとログ ファイルの既定の場所の表示または変更 &#40;SQL Server Management Studio&#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md)  
  
  
