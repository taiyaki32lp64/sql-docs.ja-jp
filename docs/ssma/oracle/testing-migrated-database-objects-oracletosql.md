---
title: 移行されたデータベース オブジェクト (OracleToSQL) のテスト |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f03ef5e1-66e6-4c84-ada2-252dd5ada82f
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 858c564c965fe7105c86a3087923887097e4ddac
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266480"
---
# <a name="testing-migrated-database-objects-oracletosql"></a>移行されたデータベース オブジェクトのテスト (OracleToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for Oracle のテスト担当者 (SSMA テスター) は、データベース オブジェクトの変換と SSMA によって行われたデータの移行を自動的にテストします。 SSMA のすべての移行手順が完了したら後、は、SSMA Tester を使用して、変換されたオブジェクトが同じように動作し、すべてのデータが適切に転送されることを確認します。  
  
SSMA テスターでは、次のオブジェクトの種類をテストできます。  
  
-   テーブル  
  
-   パッケージ化されたプロシージャを含むストアド プロシージャ。  
  
-   ユーザー定義関数、関数を含むパッケージ。  
  
-   表示モード。  
  
-   スタンドアロンのステートメント。  
  
SSMA のテスト担当者は、Oracle との対応をテストするために選択したオブジェクトを実行します。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 その後、次の条件に従って結果を比較します。  
  
-   同じテーブルのデータで、その変更ですか。  
  
-   プロシージャと関数の出力パラメーターの値は同じですか。  
  
-   同じ結果を返す関数の操作を行いますか。  
  
-   結果セットと同じですか?  
  
> [!NOTE]  
> 注意してください。 実稼働システムでの SSMA Tester を使用しないでください。 テストの実行中に、送信元スキーマとデータは変更されます。 その一方で、元の状態の完全な復元はテストされるコードの種類によっては可能でない可能性があります。  
  
## <a name="prerequisites"></a>必須コンポーネント  
SSMA Tester を使用する場合は、SSMA Oracle 拡張機能パックをインストール、**テスター データベースのインストール**オプションがオンにします。  
  
結果として得られるテーブル データの比較を有効にするには次のように設定します。、**生成 ROWID 列**オプションを**はい**スキーマの変換を開始する前にします。 SSMA の実行中にすべてのテーブルに ROWID 列を追加するが、**スキーマの変換**コマンド。  
  
さらに、次を確認します。  
  
-   Oracle クライアント ツールは、コンピューターにインストールされている[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を実行します。  
  
-   共通言語ランタイム (CLR) 統合が有効になって、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース エンジン。  
  
SSMA のテスト担当者の現在のバージョン、同じソースまたはターゲット サーバー上、複数のユーザーによって並列実行がサポートしないことに注意してください。  
  
## <a name="getting-started"></a>作業の開始  
[テスト_ケースの作成&#40;OracleToSQL&#41;](../../ssma/oracle/creating-test-cases-oracletosql.md)  
  
## <a name="see-also"></a>関連項目  
[SQL Server での SSMA コンポーネントのインストール&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[プロジェクトの設定&#40;変換&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
