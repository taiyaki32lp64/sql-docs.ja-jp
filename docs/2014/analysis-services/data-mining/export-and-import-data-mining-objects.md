---
title: エクスポートし、データ マイニング オブジェクトのインポート |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [Analysis Services]
- exporting mining models
- exporting mining structures
- mining structures [Analysis Services], creating
- mining structures [DMX], exporting
- mining models [Analysis Services], migration
ms.assetid: 10a83b13-2640-4ff5-80c8-a35e1d692908
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c2f79f8bf9a1d0ff01ba97d29662fab026d4adcd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084468"
---
# <a name="export-and-import-data-mining-objects"></a>データ マイニング オブジェクトのエクスポートおよびインポート
  SQL Server データ マイニングでは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] に用意されている、ソリューションをバックアップ、復元、および移行するための機能に加えて、データ マイニング拡張機能 (DMX) を使用して異なるサーバー間でデータ マイニング構造およびデータ マイニング モデルをすばやく転送する機能を提供しています。  
  
 データ マイニング ソリューションで多次元データベースではなくリレーショナル データを使用している場合は、データベースの復元を使用したりソリューション全体を配置したりするよりも、`EXPORT` と `IMPORT` を使用した方がすばやく簡単にモデルを転送できます。  
  
 このセクションでは、DMX ステートメントを使用してデータ マイニング構造およびデータ マイニング モデルを転送する方法の概要について説明します。 構文の詳細と例については、「[EXPORT (DMX)](/sql/dmx/export-dmx)」および「[IMPORT (DMX)](/sql/dmx/import-dmx)」を参照してください。  
  
> [!NOTE]  
>  Microsoft SQL Server Analysis Services データベースからオブジェクトをエクスポートまたはインポートするには、データベースまたはサーバーの管理者である必要があります。  
  
## <a name="exporting-data-mining-structures"></a>データ マイニング構造のエクスポート  
 マイニング構造をエクスポートすると、EXPORT ステートメントによって関連するすべてのモデルが自動的にエクスポートされます。 エクスポートするオブジェクトを制御する場合は、各オブジェクトの名前を指定する必要があります。  
  
 マイニング構造が処理されて結果がキャッシュされた場合 (既定の動作) に、マイニング構造をエクスポートすると、定義には、構造の基になっているデータの概要が含まれます。 この概要を削除するには、`Process Clear Structure` 操作を実行して、マイニング構造に関連するキャッシュを消去する必要があります。 詳細については、「 [マイニング構造の処理](process-a-mining-structure.md)」を参照してください。  
  
### <a name="exporting-data-mining-models"></a>データ マイニング モデルのエクスポート  
 `WITH DEPENDENCIES` キーワードを使用すると、マイニング モデルとその構造と共に、データ ソース定義およびデータ ソース ビュー定義をエクスポートできます。  
  
 依存関係をエクスポートせずにマイニング モデルをエクスポートすると、EXPORT ステートメントによってマイニング モデルとそのマイニング構造の定義がエクスポートされますが、データ ソースの定義はエクスポートされません。 そのため、モデルのインポート後は、直ちにモデルを参照できますが、ターゲット サーバーでマイニング モデルを再処理する場合や、基になるデータに対してクエリを実行する場合は、宛先サーバーに、対応するデータ ソースを作成する必要があります。  
  
## <a name="importing-data-mining-structures-and-models"></a>データ マイニング構造とデータ マイニング モデルのインポート  
 データ マイニング オブジェクトをインポートする場合、IMPORT ステートメントの実行時に接続しているサーバーまたはデータベースにオブジェクトがインポートされます。 サーバー上に存在しないデータベースがインポート ファイルに含まれている場合は、そのデータベースが作成されます。  
  
 `Restore` コマンドを使用して、マイニング構造またはマイニング モデルをインポートすることもできます。 モデルや構造は、エクスポート元のデータベースと同じ名前のデータベースに復元されます。 詳細については、「 [復元オプション](../multidimensional-models/restore-options.md)」を参照してください。  
  
## <a name="remarks"></a>解説  
 同じ名前のモデルや構造がインポート先のサーバーに既に存在する場合は、モデルや構造をインポートできません。 また、データ マイニング オブジェクトをエクスポートしてから、エクスポート ファイルに含まれるオブジェクトの名前を変更することもできません。 したがって、名前の競合が予想される場合は、ターゲット サーバー上のデータ マイニング オブジェクトを削除するか、定義をエクスポートする前にデータ マイニング オブジェクトの名前を変更する必要があります。  
  
## <a name="see-also"></a>参照  
 [データ マイニング ソリューションおよびオブジェクトの管理](management-of-data-mining-solutions-and-objects.md)  
  
  
