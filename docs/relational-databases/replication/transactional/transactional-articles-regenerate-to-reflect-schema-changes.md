---
title: スキーマ変更のカスタム プロシージャの再生成 (トランザクション)
description: カスタム トランザクション ストアド プロシージャを再生成して、トランザクション レプリケーションに対するスキーマ変更を反映します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- custom procedures [SQL Server replication]
- transactional replication, replicating schema changes
- schemas [SQL Server replication], replicating changes
ms.assetid: ccf68a13-e748-4455-8168-90e6d2868098
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: e6a71e6591781f61560e4c997963571a49f816e5
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321435"
---
# <a name="transactional-articles---regenerate-to-reflect-schema-changes"></a>トランザクション アーティクル - 再生成によるスキーマ変更の反映
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  既定では、トランザクション レプリケーションがサブスクライバー上のデータを変更する際、パブリケーション内の各テーブル アーティクルに対して内部プロシージャが生成したストアド プロシージャが必ず使われます。 3 つのプロシージャ (挿入、更新、削除用に 1 つずつ) はサブスクライバーにコピーされ、挿入、更新、削除がサブスクライバーにレプリケートされた時点で実行されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] パブリッシャー上のテーブルでスキーマが変更されると、レプリケーションがスクリプト作成内部プロシージャの同じセットを呼び出すことで、これらのプロシージャが自動的に再生成され、新しいプロシージャと新しいスキーマが一致します (スキーマ変更のレプリケーションは、Oracle パブリッシャーではサポートされていません)。  
  
 カスタム プロシージャを指定して、1 つ以上の既定のプロシージャを置き換えることもできます。 スキーマ変更によってカスタム プロシージャが影響を受ける場合は、そのプロシージャを変更する必要があります。 たとえば、スキーマ変更によって削除される列をプロシージャが参照している場合には、その列への参照をプロシージャから削除する必要があります。 レプリケーションで新しいカスタム プロシージャをサブスクライバーに反映するには、2 つの方法があります。  
  
-   1 つ目のオプションは、カスタム スクリプト作成プロシージャを使用して、レプリケーションで使用する既定のプロシージャを置き換える方法です。  
  
    1.  [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) を実行する場合は、`@schema_option` の 0x02 ビットを確実に **true** にします。  
  
    2.  [sp_register_custom_scripting &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md) を実行し、`@type` パラメーターには値 "insert"、"update"、または "delete" を、`@value` パラメーターにはカスタム スクリプト作成プロシージャの名前を指定します。  
  
     次回にスキーマが変更されると、レプリケーションによってこのストアド プロシージャが呼び出され、新しくユーザーが定義したカスタム ストアド プロシージャの定義がスクリプト化されて、プロシージャが各サブスクライバーに反映されます。  
  
-   2 つ目のオプションは、新しいカスタム プロシージャの定義を含むスクリプトを使用する方法です。  
  
    1.  [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) を実行するときに、`@schema_option` の 0x02 ビットを **false** に設定し、レプリケーションによってカスタム プロシージャがサブスクライバーで自動的に生成されないようにします。  
  
    2.  各スキーマ変更の前に、新しいスクリプト ファイルを作成し、[sp_register_custom_scripting &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md) を実行してスクリプトをレプリケーションに登録します。 `@type` パラメーターの値として "custom_script" を指定し、`@value` パラメーターにパブリッシャー上のスクリプトのパスを指定します。  
  
     次回に関連スキーマが変更されると、各サブスクライバーでは、DDL コマンドと同じトランザクション内でこのスクリプトが実行されます。 スキーマ変更が完了すると、スクリプトの登録が解除されます。 以降のスキーマ変更でこのスクリプトを実行するには、スクリプトを再登録する必要があります。  
  
## <a name="see-also"></a>参照  
 [トランザクション アーティクルに変更を反映する方法の指定](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)   
 [パブリケーション データベースでのスキーマの変更](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  
