---
title: リモートテーブルコピーを受信するように SQL Server を構成する
description: 並列データウェアハウスからリモートテーブルのコピーを受信するように外部 SMP SQL Server インスタンスを構成する方法について説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3e5475e86582ede2e6fa7ca5a302bba7ee74faa3
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401324"
---
# <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies---parallel-data-warehouse"></a>リモートテーブルコピーを受信するための外部 SMP SQL Server の構成-並列データウェアハウス
並列データウェアハウスからリモートテーブルのコピーを受信するように外部 SQL Server インスタンスを構成する方法について説明します。  

このトピックでは、リモートテーブルのコピーを構成するための構成手順の1つについて説明します。 すべての構成手順の一覧については、「[リモートテーブルのコピー](remote-table-copy.md)」を参照してください。  
  
## <a name="before-you-begin"></a>開始する前に  
外部 SQL Server を構成する前に、次のことを行う必要があります。  
  
-   SQL Server 2008 Enterprise Edition またはそれ以降のバージョンの Windows システムがインストールされているか、インストール済みであることが必要です。 [「InfiniBand を使用してリモートテーブルのコピーを受信するように外部 Windows システムを構成](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)する」の手順に従って、windows システムを構成する必要があります。  
  
-   SQL Server インスタンスと Windows システムを構成する機能を持つ Windows 管理者アカウント。  
  
-   SQL Server ログインアカウント (SQL Server が既にインストールされている場合)。ログインを作成し、転送先データベースに対する権限を付与する機能があります。  
  
## <a name="HowToSQLServer"></a>リモートテーブルコピーを受信するための外部 SMP SQL Server の構成  
リモートテーブルのコピー機能では、SQL Server PDW アプライアンスから、Windows システムで実行されている外部 SMP SQL Server データベースにテーブルをコピーします。 リモートテーブルのコピーを受信するように外部 Windows システムを構成した後、次の手順では SQL Server を Windows システムにインストールして構成します。  
  
SQL Server を構成するには、次の手順に従います。  
  
1.  Windows システムに SQL Server 2008 Enterprise Edition 以降のバージョンをインストールします。 これを SMP SQL Server と呼びます。  
  
2.  固定 TCP ポートで TCP/IP 接続を受け入れるように SQL Server を構成します。 この構成は既定で無効になっており、SQL Server PDW が SMP SQL Server に接続できるようにするには、この構成を有効にする必要があります。  
  
3.  Windows ファイアウォールを無効にするか、SMP SQL Server TCP ポートを構成して、Windows ファイアウォールが有効になっていることをご利用ください。  
  
4.  SQL Server 認証モードを許可するように SQL Server を構成します。 並列データエクスポートでは、常に認証に SQL Server アカウントが使用されます。  
  
5.  認証に使用される SMP SQL Server の SQL Server アカウントを決定します。 並列データエクスポート操作のために、対象のデータベースのテーブルにデータを作成、削除、および挿入する権限をそのアカウントに付与します。  
  
## <a name="BPSQLConfig"></a>リモートテーブルコピー用の SMP SQL Server 構成のベストプラクティス  
リモートテーブルのコピーを受信するように SMP SQL Server を構成する場合は、次のベストプラクティスに従ってパフォーマンスを向上させてください。  
  
1.  SQL Server の製品ドキュメントに記載されているベストプラクティスに従ってください。 たとえば、データの暗号化を有効にします。 SQL Server のセキュリティ保護の詳細については、MSDN の「 [SQL Server のセキュリティ保護](../relational-databases/security/securing-sql-server.md)」を参照してください。  
  
2.  一括ログ復旧モデルまたは単純復旧モデルを使用します。  
  
    並列データのエクスポート操作中に、新しく作成された変換先テーブルにデータが一括挿入されます。 一括挿入時のパフォーマンスを最大にするには、一括ログ復旧モデルまたは単純復旧モデルを使用するように転送先データベースを設定します。  
  
3.  Batch_size オプションを使用して、ログ領域を解放します。  
  
    一括ログ復旧モデルまたは単純復旧モデルでは、一括挿入されたデータに対して最小ログ記録が使用されますが、一部のログ記録は引き続き実行されます。 ログファイルが大きくなりすぎないようにするには、SQL Server batch_size オプションを使用して、ログ領域を定期的に再利用します。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
