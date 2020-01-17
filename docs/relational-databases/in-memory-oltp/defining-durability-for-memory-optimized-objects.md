---
title: メモリ最適化オブジェクトの持続性の定義 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 0fe85fbf-8e8d-4983-96fd-d04b3c7d6d65
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 764824a74480b6d17c890f57714b0df9221bf523
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68219872"
---
# <a name="defining-durability-for-memory-optimized-objects"></a>メモリ最適化オブジェクトの持続性の定義
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  メモリ最適化テーブルには持続性のオプションが 2 つあります。  
  
 SCHEMA_AND_DATA (既定)  
 このオプションは、スキーマとデータの両方の持続性を提供します。 データ持続性のレベルは、完全に持続性があるトランザクションと持続性に遅延が生じているトランザクションのどちらとしてコミットするかによって異なります。 完全に持続性があるトランザクションでは、ディスク ベース テーブルの場合と同様に、データとスキーマに対して同じ持続性が保証されます。 遅延した持続性ではパフォーマンスが向上しますが、サーバー クラッシュまたはフェールオーバー時にデータが失われる場合があります。 (遅延持続性の詳細については、「 [コントロールのトランザクションの持続性](../../relational-databases/logs/control-transaction-durability.md)」を参照してください。)  
  
 SCHEMA_ONLY  
 このオプションは、テーブル スキーマの持続性を確認します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が再起動するか、Azure SQL Database で再構成が行われるとき、テーブル スキーマは残りますが、テーブルのデータは失われます。 (これは tempdb のテーブルとは異なり、テーブルとテーブルのデータはどちらも再起動時に失われます)。持続性のないテーブルを作成するための一般的なシナリオは、ETL プロセスのステージング テーブルなどの一時的なデータを格納することです。 SCHEMA_ONLY の持続性により、トランザクションのログ記録とチェックポイントの両方が回避されるため、I/O 操作が大幅に減少します。  
  
 既定の SCHEMA_AND_DATA テーブルを使用するとき、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、ディスクベースのテーブルの場合と同様の耐久性を保証します。  
  
 トランザクションの持続性  
 メモリ最適化テーブルに対して (DDL または DML の) 変更を行った完全に持続性があるトランザクションをコミットする場合、持続性のあるメモリ最適化テーブルに対して行った変更は永久保存されます。  
  
 メモリ最適化テーブルに対して遅延した持続性トランザクションをコミットする場合、トランザクションは、インメモリ トランザクション ログがディスクに保存された後にのみ持続可能になります。 (遅延持続性の詳細については、「 [コントロールのトランザクションの持続性](../../relational-databases/logs/control-transaction-durability.md)」を参照してください。)  
  
 再起動の持続性  
 クラッシュまたは計画シャットダウンの後で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が再起動する場合、持続性のあるメモリ最適化テーブルは再インスタンス化されて、シャットダウンやクラッシュの前の状態に復元されます。  
  
 メディア障害の持続性  
 失敗または破損したディスクに、持続性のあるメモリ最適化オブジェクトの保存されたコピーが 1 つ以上保持されている場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバックアップおよび復元機能により、新しいメディアのメモリ最適化テーブルが復元されます。  
  
## <a name="see-also"></a>参照  
 [メモリ最適化オブジェクト用ストレージの作成と管理](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
