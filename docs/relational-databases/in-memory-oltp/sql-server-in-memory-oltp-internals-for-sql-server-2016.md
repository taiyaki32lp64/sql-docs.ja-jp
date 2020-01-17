---
title: SQL Server のインメモリ OLTP 内部
ms.custom: seo-dt-2019
ms.date: 09/14/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: b14da361-a6b8-4d85-b196-7f2f13650f44
author: jodebrui
ms.author: jodebrui
ms.openlocfilehash: d741f06741972637f7f9e6576a8dc5a21dabc681
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412559"
---
# <a name="sql-server-in-memory-oltp-internals-for-sql-server-2016"></a>SQL Server 2016 の SQL Server インメモリ OLTP 内部
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**概要:** インメモリ OLTP (コードネームの "Hekaton" で呼ばれることが多い) は SQL Server 2014 で導入されました。
この強力なテクノロジでは、大量のメモリと多数のコアを利用して、OLTP 操作のパフォーマンスを最大で 30 倍から 40 倍まで高めることができます。 SQL Server 2016 では、SQL Server 2014 で見られた多くの制限を取り除き、内部処理アルゴリズムを強化し、インメモリ OLTP によるさらなる改善に向けて、継続的にインメモリ OLTP への投資を行っています。 本書では、SQL Server 2016 RTM 版の時点での SQL Server 2016 のインメモリ OLTP テクノロジの実装について説明します。 インメモリ OLTP を使用して、テーブルを 'メモリ最適化' として宣言し、インメモリ OLTP の機能を有効にすることができます。 メモリ最適化テーブルは完全なトランザクション テーブルであり、Transact-SQL を使用してアクセスできます。 Transact-SQL ストアド プロシージャ、トリガーおよびスカラー UDF は、メモリ最適化テーブルでのパフォーマンスをさらに向上させるために、マシン語コードにコンパイルできます。 エンジンは、ブロッキングが発生しない高レベルのコンカレンシーを実現するために設計されています。    
  
**ライター:** Kalen Delaney  
  
**レビューアー:** Sunil Agarwal および Jos de Bruijn  
  
**公開日:** 2016 年 6 月  
  
**適用対象:** SQL Server 2016  
  
ドキュメントを確認する場合は、「 [SQL Server 2016 の SQL Server インメモリ OLTP 内部](https://download.microsoft.com/download/8/3/6/8360731A-A27C-4684-BC88-FC7B5849A133/SQL_Server_2016_In_Memory_OLTP_White_Paper.pdf) 」ドキュメントをダウンロードしてください。   
