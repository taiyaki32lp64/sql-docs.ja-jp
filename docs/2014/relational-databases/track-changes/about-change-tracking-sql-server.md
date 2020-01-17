---
title: 変更の追跡について (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- data changes [SQL Server]
- tracking data changes [SQL Server]
- change tracking [SQL Server], about change tracking
- change tracking [SQL Server]
- data [SQL Server], changing
ms.assetid: 5e0ef05a-8317-4c98-be20-b19d4cd78f12
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e2013a604c517ae93ee17640013e2260f50cf28e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62670928"
---
# <a name="about-change-tracking-sql-server"></a>変更の追跡について (SQL Server)
  変更の追跡は、アプリケーションの効率的な変更追跡メカニズムを提供する簡易ソリューションです。 一般に、データベース内のデータに対する変更のクエリをアプリケーションで実行し、その変更に関連する情報にアクセスできるようにするには、アプリケーション開発者がカスタムの変更追跡メカニズムを実装する必要がありました。 これらのメカニズムを作成、作業の手間は、通常、頻繁にトリガーの組み合わせを使用する必要がある`timestamp`列、追跡情報、およびカスタム クリーンアップ プロセスを格納する新しいテーブル。  
  
 変更に必要な情報量はアプリケーションの種類ごとに異なります。 アプリケーションでは、変更の追跡を使用して、ユーザー テーブルに加えられた変更に関する次の情報を取得することができます。  
  
-   ユーザー テーブルのどの行が変更されたか  
  
    -   行が変更されたという情報のみが必要で、行が変更された回数やその間に行われた変更の値は不要です。  
  
    -   最新のデータは、追跡されているテーブルから直接取得できます。  
  
-   行が変更されたか  
  
    -   同じトランザクションで変更が行われたときに、行が変更されたという情報とその変更に関する情報を取得でき、それらの情報が記録される必要があります。  
  
> [!NOTE]  
>  行われたすべての変更に関する情報や、変更されたデータの中間値についての情報が必要な場合は、変更の追跡ではなく変更データ キャプチャを使用できます。 詳細については、「[変更データ キャプチャについて &#40;SQL Server&#41;](../track-changes/about-change-data-capture-sql-server.md)」を参照してください。  
  
## <a name="one-way-and-two-way-synchronization-applications"></a>一方向および双方向の同期アプリケーション  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスとデータを同期する必要があるアプリケーションでは、変更に対するクエリを実行できる必要があります。 変更の追跡は、一方向および双方向の両方の同期アプリケーションの基礎として使用できます。  
  
### <a name="one-way-synchronization-applications"></a>一方向の同期アプリケーション  
 変更の追跡を使用するクライアントや中間層キャッシュ アプリケーションなどの一方向の同期アプリケーションを構築できます。 次の図に示すように、キャッシュ アプリケーションでは、データが [!INCLUDE[ssDE](../../includes/ssde-md.md)] に格納され、他のデータ ストアにキャッシュされる必要があります。 また、データベース テーブルに加えられた変更を含むように、キャッシュを最新の状態に保つ必要があります。 変更は [!INCLUDE[ssDE](../../includes/ssde-md.md)]に返されません。  
  
 ![一方向の同期アプリケーションを示す図](../../database-engine/media/one-waysync.gif "一方向の同期アプリケーションを示す図")  
  
### <a name="two-way-synchronization-applications"></a>双方向の同期アプリケーション  
 変更の追跡を使用する双方向の同期アプリケーションも構築できます。 このシナリオでは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスのデータが 1 つ以上のデータ ストアと同期されます。 これらのデータ ストアのデータは更新でき、変更は [!INCLUDE[ssDE](../../includes/ssde-md.md)]に返され、同期される必要があります。  
  
 ![双方向の同期アプリケーションを示す図](../../database-engine/media/two-waysync.gif "双方向の同期アプリケーションを示す図")  
  
 双方向の同期アプリケーションの好例として、常時接続でないアプリケーションが挙げられます。 この種のアプリケーションでは、クライアント アプリケーションによってローカル ストアに対するクエリおよび更新が行われます。 クライアントとサーバーの間で接続が確立されると、アプリケーションとサーバーが同期され、変更されたデータが双方向に送信されます。  
  
 双方向の同期アプリケーションでは、競合を検出できる必要があります。 同期から同期の間に、両方のデータ ストアで同じデータが変更されると、競合が発生します。 競合を検出できると、アプリケーションで変更が失われることがなくなります。  
  
## <a name="how-change-tracking-works"></a>変更の追跡のしくみ  
 変更の追跡を構成するには、DDL ステートメントまたは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用します。 詳細については、「 [変更の追跡の有効化と無効化 &#40;SQL Server&#41;](../track-changes/enable-and-disable-change-tracking-sql-server.md)」を参照してください。 変更を追跡するには、まずデータベースの変更の追跡を有効にして、次にそのデータベース内で追跡するテーブルの変更の追跡を有効にする必要があります。 テーブルの定義を変更する必要はなく、トリガーは作成されません。  
  
 テーブルの変更の追跡を構成すると、そのテーブルの行に影響する DML ステートメントが実行されるたびに、変更された各行の変更追跡情報が記録されます。 変更された行のクエリや、変更に関する情報の取得を行うには、 [変更追跡関数](/sql/relational-databases/system-functions/change-tracking-functions-transact-sql)を使用します。  
  
 変更情報と共に記録される追跡対象テーブルの情報は、主キー列の値だけです。 これらの値により、変更された行が識別されます。 それらの行の最新のデータを取得するには、アプリケーションでこの主キー列の値を使用して、ソース テーブルを追跡対象テーブルに結合します。  
  
 変更の追跡を使用して、各行に加えられた変更に関する情報を取得することもできます。 たとえば、変更を行った DML 操作の種類 (挿入、更新、または削除) や、更新操作の一環として変更された列などの情報を取得できます。  
  
## <a name="see-also"></a>参照  
 [変更の追跡の有効化と無効化 &#40;SQL Server&#41;](../track-changes/enable-and-disable-change-tracking-sql-server.md)   
 [変更の追跡のしくみ &#40;SQL Server&#41;](../track-changes/work-with-change-tracking-sql-server.md)   
 [変更の追跡の管理 &#40;SQL Server&#41;](../track-changes/manage-change-tracking-sql-server.md)   
 [データ変更の追跡 &#40;SQL Server&#41;](../track-changes/track-data-changes-sql-server.md)  
  
  
