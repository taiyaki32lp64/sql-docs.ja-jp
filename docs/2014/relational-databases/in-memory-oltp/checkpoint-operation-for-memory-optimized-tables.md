---
title: メモリ最適化テーブルのチェックポイント操作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 47975bd5-373f-43cd-946a-da8e8088b610
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: ddcdec0f624c1d6f70c57e593eaf9da66cbe0419
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63065530"
---
# <a name="checkpoint-operation-for-memory-optimized-tables"></a>メモリ最適化テーブルのチェックポイント操作
  データ ファイルとデルタ ファイルのメモリ最適化データに対してチェックポイントを定期的に作成して、トランザクション ログのアクティブな部分を進める必要があります。 チェックポイントにより、メモリ最適化テーブルでは最後に正常終了したチェックポイントまで復元および復旧することができ、トランザクション ログのアクティブな部分が適用されてメモリ最適化テーブルが更新され、復旧が完了します。 ディスク ベース テーブルとメモリ最適化テーブルのチェックポイント操作は個別の操作です。 ディスク ベース テーブルとメモリ最適化テーブルに関する各シナリオとチェックポイント動作について、次に説明します。  
  
## <a name="manual-checkpoint"></a>手動チェックポイント  
 手動でチェックポイントを作成すると、ディスク ベース テーブルおよびメモリ最適化テーブルの両方のチェックポイントが閉じられます。 アクティブなデータ ファイルは、一部分しか入力されていない場合でも閉じられます。  
  
## <a name="automatic-checkpoint"></a>自動チェックポイント  
 自動チェックポイントは、ディスク ベース テーブルとメモリ最適化テーブルではデータの保存方法が異なるため、実装方法が異なります。  
  
 ディスクベースのテーブルの場合、recovery interval 構成オプションに基づいて自動チェックポイントが取得されます (詳細については、「[データベースのターゲットの復旧時間の変更 &#40;SQL Server&#41;](../logs/change-the-target-recovery-time-of-a-database-sql-server.md)」を参照してください)。  
  
 メモリ最適化テーブルでは、最後のチェックポイントから 512 MB より大きいトランザクション ログ ファイルになったとき、自動チェックポイントは取得されます。 512 MB には、両方は、ディスク ベースおよびメモリ最適化テーブルのトランザクション ログ レコードが含まれています。  
  
## <a name="see-also"></a>参照  
 [メモリ最適化オブジェクト用ストレージの作成と管理](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
