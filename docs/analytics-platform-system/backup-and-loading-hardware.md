---
title: ハードウェアの読み込み & バックアップ
description: 並列データウェアハウス (PDW) を使用して、Analytics Platform System (APS) にエンドツーエンドのデータウェアハウスソリューションをデプロイするには、データウェアハウスをバックアップしてデータを読み込む計画を作成する必要があります。 このガイダンスを使用して、ビジネス要件を満たすバックアップサーバーと読み込みサーバーを取得して構成します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4dd4fba91b1507f711a66a88f40b2fa2ea35e1ae
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401358"
---
# <a name="backup-and-loading-hardware-overview---parallel-data-warehouse"></a>ハードウェアのバックアップと読み込みの概要-並列データウェアハウス
並列データウェアハウス (PDW) を使用して、Analytics Platform System (APS) にエンドツーエンドのデータウェアハウスソリューションをデプロイするには、データウェアハウスをバックアップしてデータを読み込む計画を作成する必要があります。 このガイダンスを使用して、ビジネス要件を満たすバックアップサーバーと読み込みサーバーを取得して構成します。  
  
## <a name="acquire-and-configure-backup-servers"></a>バックアップサーバーの取得と構成  
![バックアップ プロセス](media/backup-process.png "バックアップ プロセス")  
  
PDW データベースをバックアップするには、1つまたは複数のバックアップサーバーが必要です。 既存のハードウェアを使用することも、新しいハードウェアを購入することもできます。 詳細については、「[バックアップサーバーの取得と構成](acquire-and-configure-backup-server.md)」を参照してください。 これらの手順には、backup [server の容量計画ワークシート](backup-capacity-planning-worksheet.md)が含まれており、バックアップのための適切なソリューションを計画するのに役立ちます。  
  
## <a name="acquire-and-configure-loading-servers"></a>読み込み中のサーバーの取得と構成  
![処理の読み込み](media/loading-process.png "処理の読み込み")  
  
データを読み込むには、1つまたは複数の読み込みサーバーが必要です。 独自の既存の ETL や他のサーバーを使用することも、新しいサーバーを購入することもできます。 詳細については、「[読み込みサーバーの取得と構成](acquire-and-configure-loading-server.md)」を参照してください。 これらの手順には、読み込みのための適切なソリューションを計画する際に役立つ、[サーバー容量計画の読み込みワークシート](loading-server-capacity-planning-worksheet.md)が含まれています。  
  
## <a name="see-also"></a>参照  
[バックアップと復元の概要](backup-and-restore-overview.md)  
[読み込みの概要](load-overview.md)  
  
