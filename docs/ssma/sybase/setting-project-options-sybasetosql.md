---
title: プロジェクト オプション (SybaseToSQL) の設定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Project Options Setting
ms.assetid: 97b70fc8-1f68-4f15-8e22-db5b784ea4ec
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 2c8d074db2fc1e8a9d29ecf5fdc0405524e9bb1a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020922"
---
# <a name="setting-project-options-sybasetosql"></a>プロジェクト オプションの設定 (SybaseToSQL)
SSMA プロジェクトごとに、プロジェクト レベルのオプションを設定することができます。 これらのオプションは、オブジェクトへの変換、オブジェクトの読み込み、SQL azure、ユーザー インターフェイス、およびデータ移行の設定を指定します。 オブジェクトを変換する前に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure にデータを移行または[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure、構成オプションが、プロジェクトの適切なことを確認します。  
  
SSMA では、すべてのプロジェクトの既定のオプションを構成できます。 これらのオプションは、作成する新しいプロジェクトに適用されます。 各プロジェクトのオプションをカスタマイズできます。  
  
## <a name="configuration-options-and-modes"></a>構成オプションとモード  
SSMA では、プロジェクトの設定の 5 つのセットがあります。  
  
1.  プロジェクト情報  
  
2.  一般 (変換、移行とデータの収集)。  
  
3.  Synchronization  
  
4.  GUI  
  
5.  型のマッピング  
  
これらの設定を構成するための 4 つのモードもあります。  
  
1.  既定  
  
2.  オプティミスティック  
  
3.  [完全]  
  
4.  カスタム  
  
ほとんどのユーザーには、既定のモードを使用することをお勧めします。 オプティミスティック モードでは、Sybase Adaptive Server Enterprise (ASE) の現在の構文の詳細を保持し、読みやすきます。 ただし、現在の構文を維持することができない正確です。 ASE の構文と同等に変換する必要がある場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure の構文、完全なモード、完全な変換を実行しますが、結果のコードが読みにくくなる可能性があります。 カスタム モードでは、オプションを設定します。  
  
設定は、このドキュメントのユーザー インターフェイス リファレンス セクションで説明します。 設定と各モードで、設定を適用する方法の詳細については、次のトピックを参照してください。  
  
-   [プロジェクトの設定&#40;変換&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
-   [プロジェクトの設定&#40;移行&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md)  
  
-   [プロジェクトの設定&#40;同期&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md)  
  
-   [プロジェクトの設定&#40;GUI&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md)  
  
-   [プロジェクトの設定&#40;の種類のマッピング&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)  
  
-   [プロジェクトの設定&#40;Azure SQL DB &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md)  
  
## <a name="setting-project-options"></a>プロジェクト オプションの設定  
SSMA では、すべてのプロジェクトの既定の設定を構成できます。 これらの設定は SSMA の構成ファイルに保存し、作成した新しいプロジェクトに適用します。  
  
**既定のプロジェクトのオプションを設定するには**  
  
1.  **ツール**メニューの **プロジェクト設定の既定の**します。  
  
2.  **プロジェクト設定の既定の**ダイアログ ボックスで、次の手順のいずれかを使用します。  
  
    -   設定は表示または変更に必要な移行プロジェクトの種類を選択します。**移行ターゲット バージョン**ドロップ ダウン左側のウィンドウの下部にある [全般] をクリックし、変換または移行または SQL Azure を選択します。  
  
    -   定義済みのモードを選択する、**モード**ドロップダウン ボックスで、**既定**、 **Optimistic**、または**完全**します。  
  
    -   カスタム設定を指定するには、選択か、新しい設定または値を入力します。  
  
3.  クリックして**OK**設定を保存します。  
  
現在のプロジェクトの設定をカスタマイズすることもできます。 これらの設定は、現在のプロジェクト ファイルに保存されます。  
  
**現在のプロジェクトの設定をカスタマイズするには**  
  
1.  **ツール**メニューの **プロジェクト設定**します。  
  
2.  **プロジェクト設定**ダイアログ ボックスで、次の手順のいずれかを使用します。  
  
    -   定義済みのモードを選択する、**モード**ドロップダウン ボックスで、**既定**、 **Optimistic**、または**完全**します。  
  
    -   カスタムのモードを指定する、**モード**ドロップダウン ボックスで、**カスタム**、左側のウィンドウでオプションを選択、設定または右側のウィンドウで値をクリックし選択するか、新しい設定または値を入力します。  
  
3.  クリックして**OK**設定を保存します。  
  
## <a name="next-steps"></a>次の手順  
移行の次の手順は、プロジェクトのニーズによって異なります。  
  
-   カスタム ソースとターゲットのデータ型のマッピングを参照してください[マッピング Sybase ASE と SQL Server データ型&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)します。  
  
-   Sybase データベース オブジェクト定義を変換する場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のオブジェクトの定義。 詳細については、次を参照してください。 [Sybase ASE データベース オブジェクトの変換&#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)します。  
  
## <a name="see-also"></a>参照  
[SQL Server - Azure SQL DB への Sybase ASE データベース移行&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
