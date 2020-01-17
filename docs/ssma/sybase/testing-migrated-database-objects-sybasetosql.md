---
title: 移行されたデータベース オブジェクト (SybaseToSQL) のテスト |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4937f6b4-86bd-4070-88df-3d216306c33a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 6fb469dfcaaec33a03681bfb64f411851df0400e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020913"
---
# <a name="testing-migrated-database-objects-sybasetosql"></a>移行されたデータベース オブジェクトのテスト (SybaseToSQL)
Microsoft SQL Server Migration Assistant for Sybase のテスト担当者 (SSMA テスター) が自動的にテスト データベース オブジェクトの変換と SSMA によって行われたデータの移行。 SSMA のすべての移行手順が完了したら後、は、SSMA Tester を使用して、変換されたオブジェクトが同じように動作し、すべてのデータが適切に転送されることを確認します。  
  
> [!NOTE]  
> Azure への接続の場合は、テスト担当者のコンポーネントが無効です。  
  
SSMA テスターでは、次のオブジェクトの種類をテストできます。  
  
-   テーブル  
  
-   ストアド プロシージャ  
  
-   表示モード。  
  
-   スタンドアロンのステートメント。  
  
SSMA のテスト担当者は、Sybase との対応する SQL Server でのテストを選択したオブジェクトを実行します。 その後、次の条件に従って結果を比較します。  
  
-   同じテーブルのデータで、その変更ですか。  
  
-   プロシージャと関数の出力パラメーターの値は同じですか。  
  
-   同じ結果を返す関数の操作を行いますか。  
  
-   結果セットと同じですか?  
  
> [!NOTE]  
> 注意してください。 実稼働システムでの SSMA Tester を使用しないでください。 テストの実行中に、送信元スキーマとデータは変更されます。 その一方で、元の状態の完全な復元はテストされるコードの種類によっては可能でない可能性があります。  
  
## <a name="prerequisites"></a>必須コンポーネント  
SSMA Tester を使用する場合は、SSMA Sybase 拡張機能パックをインストール、**テスター データベースのインストール**オプションがオンにします。  
  
さらに、次を確認します。  
  
-   Sybase OLE DB プロバイダーは、コンピューターにインストールされている[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を実行します。  
  
-   共通言語ランタイム (CLR) 統合が有効になって、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース エンジン。  
  
SSMA のテスト担当者の現在のバージョン、同じソースまたはターゲット サーバー上、複数のユーザーによって並列実行がサポートしないことに注意してください。  
  
## <a name="getting-started"></a>作業の開始  
[テスト_ケースの作成&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-test-cases-sybasetosql.md)  
  
## <a name="see-also"></a>関連項目  
[SQL Server での SSMA コンポーネントのインストール&#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[プロジェクトの設定&#40;変換&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
