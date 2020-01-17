---
title: ミラー化バックアップ メディア セット (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- recovery [SQL Server], mirrored backups
- mirrored media sets [SQL Server]
- backup mirrors [SQL Server]
- duplicate backup copies
- interchangeable backup copies [SQL Server]
- media sets [SQL Server], mirrored backup media sets
- backup media [SQL Server], mirrored media
ms.assetid: 05a0b8d1-3585-4f77-972f-69d1c0d4aa9b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ad183871e58f5dc64cf763c540e1629a09b4f320
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62876096"
---
# <a name="mirrored-backup-media-sets-sql-server"></a>ミラー化バックアップ メディア セット (SQL Server)
    
> [!NOTE]  
>  ミラー化バックアップ メディア セットは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の Enterprise Edition のみでサポートされています。  
  
 メディア セットをミラー化すると、バックアップ デバイスの誤動作の影響が小さくなるため、バックアップの信頼性が向上します。 バックアップはデータ損失に対する最後の防護策なので、このような誤動作は非常に深刻です。 データベースが大きくなるにつれて、バックアップ デバイスやメディアの障害によってバックアップを復元できなくなる可能性が高くなります。 バックアップ メディアをミラー化すると、冗長性によってバックアップの信頼性が向上します。  
  
> [!NOTE]  
>  メディア セットの概要については、「 [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)の Enterprise Edition のみでサポートされています。  
  
 **このトピックの内容**  
  
-   [ミラー化メディア セットの概要](#OverviewofMirroredMediaSets)  
  
-   [バックアップ ミラーのハードウェア要件](#HardwareReqs)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="OverviewofMirroredMediaSets"></a> ミラー化メディア セットの概要  
 メディアのミラー化は、メディア セットのプロパティです。 *ミラー化メディア セット* は、メディア セットの複数のコピー (*ミラー*) で構成されています。 メディア セットには、1 つ以上のメディア ファミリが含まれており、各メディア ファミリが 1 つのバックアップ デバイスに対応します。 たとえば、BACKUP DATABASE ステートメントの TO 句に 3 つのデバイスを指定する場合、BACKUP によって 1 つのデバイスにつき 3 つのメディア ファミリにデータが分散されます。 メディア ファミリとミラーの数は、メディア セットを作成するときに定義します (BACKUP DATABASE ステートメントで WITH FORMAT を指定します)。  
  
 ミラー化メディア セットには、2 ～ 4 つのミラーがあります。 各ミラーには、メディア セットのすべてのメディア ファミリが含まれます。 ミラーには、メディア ファミリ 1 つにつき、同数のデバイスが必要です。 各ミラーには、メディア ファミリごとに別のバックアップ デバイスが必要です。 たとえば、3 つのミラーを持つ 4 つのメディア ファミリで構成されるミラー化メディア セットには、12 台のバックアップ デバイスが必要です。 これらのデバイスはすべて同等であることが必要です。 たとえば、同じ製造元で同じモデル番号のテープ ドライブなどです。  
  
 次の図は、2 つのミラーを持つ 2 つのメディア ファミリで構成されるミラー化メディア セットの例を示しています。 各メディア ファミリには 3 つのメディア ボリュームがあり、ミラーごとに 1 回ずつバックアップされます。  
  
 ![ミラー化メディア セット: 2 つのミラーから成る 2 つのファミリ](../../database-engine/media/bnr-backup-media-mirror.gif "ミラー化メディア セット: 2 つのミラーから成る 2 つのファミリ")  
  
 ミラーの対応するボリュームは、同じ内容です。 これにより、復元時にボリュームを交換できます。 たとえば、上の図では、テープ 2 の 3 番目のボリュームは、テープ 0 の 3 番目のボリュームと交換可能です。  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] では、ミラー化メディアの内容がすべて同じになるように、デバイスへの書き込みの同期をとっています。 いずれかのミラーが満杯になると、同じことが同時にすべてのミラーに起こります。  
  
> [!IMPORTANT]  
>  ミラー化メディア セットは、ミラーを削除することによって暗黙的に分割できません。 ミラー内のいずれかのテープまたはディスクが損傷を受けたり再フォーマットされたりすると、そのミラーはその後のバックアップに使用できなくなります。 少なくとも 1 つのミラーが完全な状態になっていれば、メディア セットを読み取ることができます。 すべてのミラーで特定のメディア ファミリが失われると、そのメディア セットは使用できなくなります。  
  
 すべてのミラーが存在する必要があるかどうかは、バックアップ操作と復元操作で異なります。 ミラー化メディア セットを書き込む (作成または拡張する) バックアップ操作では、すべてのミラーが存在する必要があります。 一方、ミラー化メディア セットからバックアップを復元する場合は、各メディア ファミリに対して 1 つのミラーだけを指定できます。 ファミリ数よりも少ない数のデバイスからでも復元できますが、各メディア ファミリが処理されるのは 1 回だけです。 エラーが発生したとき、他に複数のミラーを用意しておくと復元に関する問題をすばやく解決できる場合があります。 損傷したメディア ボリュームは、別のミラーの対応するボリュームで代替できます。 これは、RESTORE および RESTORE VERIFYONLY によって、壊れたメディアと他のミラーの対応するバックアップ メディア ボリュームが置換されるためです。  
  
##  <a name="HardwareReqs"></a> バックアップ ミラーのハードウェア要件  
 ミラー化は、ディスクとテープの両方に適用されます (ディスクでは連続テープはサポートされていません)。 同一のバックアップ操作または復元操作に使用するバックアップ デバイスはすべて同じ種類、つまりディスクまたはテープのいずれかにする必要があります。  
  
 これらの大まかな種類の中では、同じプロパティを持つ同等のデバイスを使用する必要があります。 デバイスが同等でない場合は、エラー メッセージ (3212) が表示されます。 デバイスの不適合によって生じるリスクを回避するには、同じ製造元で同じモデル番号のドライブのみを使用するなど、同等のデバイスを使用してください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **ミラー化バックアップ デバイスにバックアップするには**  
  
-   [ミラー化メディア セットへのバックアップ &#40;Transact-SQL&#41;](back-up-to-a-mirrored-media-set-transact-sql.md)  
  
## <a name="see-also"></a>参照  
 [バックアップ中および復元中に発生する可能性があるメディア エラー &#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql)   
 [バックアップ デバイス &#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
