---
title: テスト_ケース (SybaseToSQL) の作成 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester component,Test Case Wizard
ms.assetid: b52dfd93-95af-4299-bc8f-83f2a7a6a518
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: b3f54a38ae995dd2c83fd36647393f81b802fde2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948450"
---
# <a name="creating-test-cases-sybasetosql"></a>テスト ケースの作成 (SybaseToSQL)
テストを作成するのにには、テスト_ケースのウィザードを使用します。 このウィザードを使用して、テストおよび検証オブジェクトを選択し、テストのパラメーターを指定して、テスト_ケースを作成できます。  
  
## <a name="starting-the-test-case-wizard"></a>テスト_ケースのウィザードを開始します。  
テスト_ケースのウィザードを起動する **新しいテスト...ケース** から、 **テスター** メニュー。  
  
起動すると、ウィザードは、データベース ssmatester2005db または元の Sybase サーバーで (プロジェクトの種類に応じて ssmatester2008db を検索します。 テスト担当者拡張機能のスキーマの補助オブジェクトの格納に使用することをお勧めします。 テスト_ケースが見つかりません。 ssmatester2005db または ssmatester2008db、テスト担当者の拡張機能のデータベースを作成することを提案する ダイアログ ウィンドウが表示されます。 (そのような状況通常発生 SSMA テスターの最初の実行中にします。)  
  
ダイアログ ウィンドウが表示された場合にクリックします**はい**Sybase テスト担当者データベース移行元サーバーを作成します。 新しいダイアログ ウィンドウでは、テスト担当者の新しいデータベースを配置する 1 つまたは複数のデバイスを追加する必要があるされます。 クリックして**追加**デバイスを追加します。 **テスト担当者のデータベースの割り当て領域**ダイアログは、デバイスを選択し、テスト担当者のデータベースで使用されるサイズを指定します。 さらに、データベースのログを別のデバイスを設定することができます。 データベースを作成するには Sybase 特権がありますに注意してください。  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>ウィザードを使用してテスト_ケースの作成の概要  
テスト_ケースの作成のプロセスは、5 つの手順で構成されます。  
  
1.  [テスト_ケースの初期化&#40;SybaseToSQL&#41;](../../ssma/sybase/initializing-test-cases-sybasetosql.md)します。  
  
2.  [選択し、テストするオブジェクトを構成する&#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)します。  
  
3.  [影響を受けるオブジェクトの選択と構成&#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)します。  
  
4.  [呼び出し順序のカスタマイズ&#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md)します。  
  
5.  [テスト_ケースの準備の終了&#40;SybaseToSQL&#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md)します。  
  
## <a name="see-also"></a>関連項目  
[移行されたデータベース オブジェクトのテスト&#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
