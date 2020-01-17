---
title: リソース ガバナーの分類子関数 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, classifier function
- user-defined functions [SQL Server], classifier function
- classifier function [SQL Server]
- classifier function [SQL Server], overview
ms.assetid: 64c25012-7068-476f-afa2-0b4f3adde9a4
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: eeb3d08f0a14434fa5d071d88a3d26ec6fcaf6c9
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72903913"
---
# <a name="resource-governor-classifier-function"></a>リソース ガバナーの分類子関数
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リソース ガバナーの分類プロセスにより、着信セッションがセッションの特性に基づいてワークロード グループに割り当てられます。 分類ロジックは、分類子関数と呼ばれるユーザー定義関数を記述することで調整できます。  
  
## <a name="classification"></a>分類  
 リソース ガバナーでは、着信セッションの分類がサポートされます。 分類は、関数に含まれているユーザーが記述した一連の基準に基づいて行われます。 この関数ロジックの結果を使用して、リソース ガバナーは、セッションを既存のワークロード グループに分類します。  
  
> [!NOTE]  
>  内部ワークロード グループには、内部だけで使用される要求が格納されます。 要求のルーティングに使用される基準は変更できません。また、要求を内部ワークロード グループに分類することもできません。  
  
 着信セッションをワークロード グループに割り当てるロジックを含んだスカラー関数を作成することができます。 この関数を使用する前に、次の操作を完了する必要があります。  
  
-   ALTER RESOURCE GOVERNOR ステートメントを使用して、関数を作成し、登録します。 詳細については、「[ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)」を参照してください。  
  
-   RECONFIGURE パラメーターを指定した ALTER RESOURCE GOVERNOR ステートメントを使用して、リソース ガバナーの構成を更新します。  
  
 関数を作成して構成の変更を適用すると、この関数から返されたワークロード グループ名がリソース ガバナーの分類で使用されて、適切なワークロード グループに新しい要求が送信されます。  
  
> [!IMPORTANT]  
>  分類関数が指定のログイン タイムアウトまでに完了せずに、クライアント セッションがタイムアウトになることがあります。 ログイン タイムアウトはクライアントのプロパティであるため、サーバーはタイムアウトを認識しません。分類関数の実行時間が長いと、孤立した接続がサーバーに長時間残される可能性があります。 接続がタイムアウトになる前に実行が完了する分類関数を作成することが重要です。  
  
 ユーザー定義関数の特性と動作は次のとおりです。  
  
-   ユーザー定義関数は、接続プールが有効になっている場合でも、新しいセッションすべてに対して評価されます。  
  
-   ユーザー定義関数は、セッションにワークロード グループ コンテキストを割り当てます。 グループのメンバーシップが確定すると、セッションがその有効期間にわたってワークロード グループにバインドされます。  
  
-   ユーザー定義関数が NULL、既定値、または存在しないグループの名前を返した場合は、セッションに既定のワークロード グループ コンテキストが割り当てられます。 関数が何らかの理由で失敗した場合も、セッションに既定のコンテキストが割り当てられます。  
  
-   ユーザー定義関数は、サーバー スコープ (master データベース) で定義する必要があります。  
  
-   ユーザー定義の分類関数の指定は、ALTER RESOURCE GOVERNOR RECONFIGURE を実行するまで有効となりません。  
  
-   分類子として指定できるのは、一度に 1 つのユーザー定義関数だけです。  
  
-   ユーザー定義の分類関数は、分類子の状態が削除されない限り、削除または変更できません。  
  
-   ユーザー定義の分類関数がない場合は、すべてのセッションが既定のグループに分類されます。  
  
-   分類関数から返されたワークロード グループは、スキーマ バインド制限の対象外です。 たとえば、テーブルを削除することはできませんが、ワークロード グループは削除できます。  
  
> [!IMPORTANT]  
>  サーバー上で専用管理者接続 (DAC) を有効にすることをお勧めします。 DAC は、リソース ガバナーの分類の対象ではなく、分類関数の監視とトラブルシューティングに使用できます。 詳細については、「 [データベース管理者用の診断接続](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)」を参照してください。 トラブルシューティングに DAC を使用できない場合は、システムをシングル ユーザー モードで再起動します。 シングル ユーザー モードは分類の対象となりませんが、実行中のリソース ガバナーによる分類をこのモードで診断することはできません。  
  
### <a name="classification-process"></a>分類処理  
 リソース ガバナーのコンテキストでは、セッションのログイン プロセスが次の手順で実行されます。  
  
1.  ログイン認証  
  
2.  LOGON トリガー実行  
  
3.  分類  

 分類が開始されると、リソース ガバナーは分類子関数を実行し、関数から返された値を使用して適切なワークロード グループに要求を送信します。  
  
> [!NOTE]  
>  分類関数および LOGON トリガーの実行に関する情報は、 [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) および [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)」で公開されます。  
  
## <a name="classification-function-tasks"></a>分類関数のタスク  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|ユーザー定義の分類子関数を作成およびテストする方法について説明します。|[ユーザー定義の分類子関数の作成とテスト](../../relational-databases/resource-governor/create-and-test-a-classifier-user-defined-function.md)|  
  
## <a name="see-also"></a>参照  
 [リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)   
 [リソース ガバナーの有効化](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [リソース ガバナー リソース プール](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [リソース ガバナー ワークロード グループ](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [テンプレートを使用してリソース ガバナーを構成する](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)   
 [リソース ガバナー プロパティの表示](../../relational-databases/resource-governor/view-resource-governor-properties.md)  
  
  
