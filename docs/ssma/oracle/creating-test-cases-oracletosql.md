---
title: テスト_ケース (OracleToSQL) の作成 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Test Case Wizard
ms.assetid: 22f38901-ec35-4707-a911-784e6ad8dafb
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 697f7049a60aa7ae2b8c89d1fb6c5ce8e3d29312
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266132"
---
# <a name="creating-test-cases-oracletosql"></a>テスト ケースの作成 (OracleToSQL)
テストを作成するのにには、テスト_ケースのウィザードを使用します。 このウィザードを使用して、テストおよび検証オブジェクトを選択し、テストのパラメーターを指定して、テスト_ケースを作成できます。  
  
## <a name="starting-the-test-case-wizard"></a>テスト_ケースのウィザードを開始します。  
テスト_ケースのウィザードを起動する **新しいテスト_ケース** から、 **テスター** メニュー。  
  
起動すると、ウィザードは、ソース Oracle サーバー上のスキーマ SSMATESTER_ORACLE を検索します。 テスト担当者拡張機能のスキーマの補助オブジェクトの格納に使用することをお勧めします。 テスト_ケースのウィザードでは、SSMATESTER_ORACLE を見つけられない場合は、スキーマを作成することを提案する ダイアログ ウィンドウが表示されます。 (そのような状況通常発生 SSMA テスターの最初の実行中にします。)  
  
ダイアログ ウィンドウが表示された場合は、クリックして**はい**移行元サーバーで SSMATESTER_ORACLE スキーマを作成します。 新しいユーザーを作成し、このユーザーのスキーマでオブジェクトを作成する Oracle の権限がありますに注意してください。  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>ウィザードを使用してテスト_ケースの作成の概要  
テスト_ケースの作成のプロセスは、5 つの手順で構成されます。  
  
1.  [テスト_ケースの初期化&#40;OracleToSQL&#41;](../../ssma/oracle/initializing-test-cases-oracletosql.md)  
  
2.  [選択し、テストするオブジェクトを構成する&#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
  
3.  [影響を受けるオブジェクトの選択と構成&#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
4.  [呼び出し順序のカスタマイズ&#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
5.  [テスト_ケースの準備の終了&#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
## <a name="see-also"></a>関連項目  
[移行されたデータベース オブジェクトのテスト&#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
