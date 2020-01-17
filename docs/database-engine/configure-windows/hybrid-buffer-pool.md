---
title: ハイブリッド バッファー プール | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ''
author: briancarrig
ms.author: brcarrig
ms.openlocfilehash: d03c66219330df3cca892bd005d1e9a456959c83
ms.sourcegitcommit: af5e1f74a8c1171afe759a4a8ff2fccb5295270a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2019
ms.locfileid: "71823572"
---
# <a name="hybrid-buffer-pool"></a>ハイブリッド バッファー プール
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

ハイブリッド バッファー プールにより、データベース エンジンから永続メモリ (PMEM) デバイスに格納されているデータベース ファイル内のデータ ページに直接アクセスできるようになります。 この機能は [!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)] で導入されています。

PMEM のない従来のシステムでは、SQL Server によってデータ ページがバッファー プールにキャッシュされます。 ハイブリッド バッファー プールを使用すると、SQL Server では、バッファー プールの DRAM ベースの部分にページのコピーを実行することをスキップし、代わりに PMEM デバイスにあるデータベース ファイル上で直接ページにアクセスします。 ハイブリッド バッファー プール用の PMEM デバイス上のデータ ファイルへの読み取りアクセスは、PMEM デバイス上のデータ ページへのポインターに従って直接実行されます。  

PMEM デバイスで直接アクセスできるのは、クリーン ページのみです。 ページがダーティとマークされている場合、ページは DRAM バッファー プールにコピーされてから、最終的に PMEM デバイスに書き戻されて再びクリーンとしてマークされます。 これは通常のチェックポイント操作中に発生します。 ファイルを PMEM デバイスから DRAM にコピーするメカニズムはダイレクト メモリ マッピング I/O (MMIO) であり、SQL Server 内のデータ ファイルの*エンライトメント*とも呼ばれます。


ハイブリッド バッファー プール機能は、Windows と Linux の両方で使用できます。 PMEM デバイスは、DAX (DirectAccess) をサポートするファイル システムでフォーマットする必要があります。 XFS、EXT4、NTFS のすべてのファイル システムで、DAX がサポートされています。 SQL Server では、データ ファイルが適切にフォーマットされた PMEM デバイス上に存在するかどうかが自動的に検出され、ユーザーの領域内でのメモリ マッピングが実行されます。 このマッピングは、新しいデータベースがアタッチ、復元、作成されるか、ハイブリッド バッファー プール機能がデータベースに対して有効化されると、起動時に行われます。

Windows Server の PMEM に対するサポートの詳細については、[Windows Server での永続メモリの配置](/windows-server/storage/storage-spaces/deploy-pmem/)に関するページを参照してください。

PMEM デバイス用に Linux 上で SQL Server を構成する方法については、[永続メモリの配置](../../linux/sql-server-linux-configure-pmem.md)に関するページを参照してください。

## <a name="enable-hybrid-buffer-pool"></a>ハイブリッド バッファー プールを有効にする

[!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)] では、ハイブリッド バッファー プールを管理するための動的データ言語 (DDL) が導入されています。

次の例では、SQL Server のインスタンス用にハイブリッド バッファー プールを有効にします。

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = ON;
```

既定では、ハイブリッド バッファー プールはインスタンスのスコープで無効に設定されます。 設定の変更を有効にするためには、SQL Server インスタンスを再起動する必要があることに注意してください。 サーバー上の合計 PMEM 容量を考慮するために十分なハッシュ ページの割り当てを容易にするためには、再起動が必要です。

次の例では、特定のデータベース用にハイブリッド バッファー プールを有効にします。

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = ON;
```

既定では、ハイブリッド バッファー プールはデータベースのスコープで有効に設定されます。

## <a name="disable-hybrid-buffer-pool"></a>ハイブリッド バッファー プールを無効にする

次の例では、SQL Server のインスタンス用にハイブリッド バッファー プールを無効にします。

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = OFF;
```

既定では、ハイブリッド バッファー プールはインスタンスのスコープで無効に設定されます。 設定の変更を有効にするためには、SQL Server インスタンスを再起動する必要があることに注意してください。 サーバー上の PMEM 容量は考慮する必要がないため、ハッシュページの超過割り当てを防ぐためには再起動が必要です。

次の例では、特定のデータベース用にハイブリッド バッファー プールを無効にします。

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = OFF;
```

既定では、ハイブリッド バッファー プールはデータベースのスコープで有効に設定されます。

## <a name="view-hybrid-buffer-pool-configuration"></a>ハイブリッド バッファー プールの構成を表示する

次の例では、SQL Server のインスタンス用のハイブリッド バッファー プールのシステム構成について、現在の状態が返されます。

```sql
SELECT * FROM
sys.server_memory_optimized_hybrid_buffer_pool_configuration;
```

次の例では、2 つのテーブルが返されます。

- 1 つ目には、SQL Server のインスタンス用のハイブリッド バッファー プールのシステム構成について、現在の状態が示されます。
- 2 つ目には、データベースと、ハイブリッド バッファー プールのデータベース レベルの設定 (`is_memory_optimized_enabled`) が表示されます。

```sql
SELECT * FROM sys.configurations WHERE name = 'hybrid_buffer_pool';

SELECT name, is_memory_optimized_enabled FROM sys.databases;
```

## <a name="best-practices-for-hybrid-buffer-pool"></a>ハイブリッド バッファー プールのベスト プラクティス

Windows 上でご利用の PMEM デバイスをフォーマットする場合、NTFS に利用できる最大のアロケーション ユニット サイズ (Windows Server 2019 では 2 MB) を使用して、デバイスが DAX (Direct Access) 用に確実にフォーマットされているようにします。

最適なパフォーマンスを得るには、Windows 上で [[メモリ内のページのロック]](./enable-the-lock-pages-in-memory-option-windows.md) を有効にします。

ファイル サイズは 2 MB の倍数である必要があります (剰余 2 MB はゼロと等しい)。

ハイブリッド バッファー プールのサーバー スコープ設定が無効に設定されている場合、ハイブリッド バッファー プールはどのユーザー データベースでも使用されません。

ハイブリッド バッファーのサーバー スコープ設定が有効になっている場合、個々のユーザー データベースに対してハイブリッド バッファー プールの使用を無効にすることができます。そのためには、それらのユーザー データベースに対してデータベース スコープ レベルでのハイブリッド バッファー プールを無効にする手順に従います。
