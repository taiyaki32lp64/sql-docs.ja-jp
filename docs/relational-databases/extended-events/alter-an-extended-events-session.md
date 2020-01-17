---
title: 拡張イベント セッションの変更
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
ms.assetid: 114ec05b-7eca-4c87-b276-25e37b84be39
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 32a57c46cebb17df257f2002c25ab5f1d7107379
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75255769"
---
# <a name="alter-an-extended-events-session"></a>拡張イベント セッションの変更

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  拡張イベント セッションを作成したら、 **SQL Server 拡張イベント ウィザード**を使用して、必要に応じて拡張イベント セッションを変更できます。  
  
## <a name="before-you-begin"></a>開始する前に  
 アクティブなセッションおよび非アクティブなセッションのターゲットを変更することはできません。また、アクティブなセッションの詳細プロパティの構成を変更することはできません。  
  
 アクティブなイベント セッションと非アクティブなイベント セッションの両方に対して、次の変更を実行できます。  
  
-   セッションのイベントの追加または削除、および、イベントの構成 (イベントのフィールド、フィルター、アクションなど) の変更。  
  
-   イベント セッションのターゲットの追加または削除。  
  
-   **[サーバーの起動時にイベント セッションを開始する]** オプションの有効化。  
  
 非アクティブなイベント セッションに対しては、次の変更も実行できます。  
  
-   **[イベント間のリレーションシップの追跡]** オプションの有効化。  
  
-   詳細プロパティの構成の変更。  
  
> [!NOTE]  
>  **SQL Server 拡張イベント ウィザード** では、イベント セッションの変更はサポートされていません。  
  
## <a name="how-to-alter-an-extended-events-session-using-the-sql-server-extended-events-wizard"></a>SQL Server 拡張イベント ウィザードを使用して拡張イベント セッションを変更する方法  
  
-   オブジェクト エクスプローラーで **[管理]** を展開し、 **[拡張イベント]** を展開して、 **[セッション]** を展開します。  
  
-   変更するセッションを右クリックし、 **[プロパティ]** をクリックします。  
  
-   **[プロパティ]** ダイアログ ボックスで、必要な変更を行い、 **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [クエリ エディターを使用した拡張イベント セッションの作成](quick-start-extended-events-in-sql-server.md)  
  
  
