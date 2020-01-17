---
title: プロジェクト オプション (OracleToSQL) の設定 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Configuration Options and Modes
ms.assetid: a324d07d-cfdf-43bd-98a0-acf332c5a4db
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 6947a51b731b22b28ffbaa509f7cd38be5e7ebc5
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266528"
---
# <a name="setting-project-options-oracletosql"></a>プロジェクト オプションの設定 (OracleToSQL)
SSMA プロジェクトごとに、プロジェクト レベルのオプションを設定できます。 これらのオプションは、オブジェクトへの変換、オブジェクトの読み込み、ユーザー インターフェイスとデータ移行の設定を指定します。 オブジェクトを変換する前に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]にデータを移行または[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、構成オプションが、プロジェクトの適切なことを確認します。  
  
SSMA では、すべてのプロジェクトの既定のオプションを構成できます。 これらのオプションは、作成した新しいプロジェクトに適用されます。 各プロジェクトのオプションをカスタマイズできます。  
  
## <a name="configuration-options-and-modes"></a>構成オプションとモード  
SSMA では、プロジェクトの設定の 5 つのセットがあります。  
  
-   プロジェクト情報  
  
-   全般 (変換、移行、オブジェクトの読み込み)  
  
-   Synchronization  
  
-   GUI  
  
-   型のマッピング  
  
これらの設定を構成するための 4 つのモードもあります。  
  
-   既定  
  
-   オプティミスティック  
  
-   [完全]  
  
-   カスタム  
  
ほとんどのユーザーには、既定のモードを使用することをお勧めします。 オプティミスティック モードでは、現在の Oracle の構文の詳細を保持しが読みやすくします。 ただし、現在の構文を維持することができない正確です。 Oracle の構文と同等に変換する必要がある場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]構文、完全なモードが、最も包括的な変換を実行しますが、結果のコードが読みにくくなる可能性があります。 カスタム モードでは、オプションを設定します。  
  
設定と各モードで、設定を適用する方法の詳細については、次のトピックを参照してください。  
  
-   [プロジェクトの設定&#40;変換&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
-   [プロジェクトの設定&#40;移行&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-migration-oracletosql.md)  
  
-   [プロジェクトの設定&#40;同期&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md)  
  
-   [プロジェクトの設定&#40;GUI&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-gui-oracletosql.md)  
  
-   [プロジェクトの設定&#40;の種類のマッピング&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md)  
  
## <a name="setting-project-options"></a>プロジェクト オプションの設定  
SSMA では、すべてのプロジェクトの既定の設定を構成できます。 これらの設定は SSMA の構成ファイルに保存し、作成した新しいプロジェクトに適用します。  
  
**既定のプロジェクトのオプションを設定するには**  
  
1.  **ツール** メニューのをクリックして**プロジェクト設定の既定の**します。  
  
2.  **プロジェクト設定の既定の**ダイアログ ボックスで、次の手順のいずれかを使用します。  
  
    -   設定は表示または変更に必要な移行プロジェクトの種類を選択します**移行ターゲット バージョン**をクリックしてドロップダウン**全般**変換を選択し、左側のウィンドウの下部にあるまたは。移行します。  
  
    -   定義済みのモードを選択する、**モード**ドロップダウン ボックスで、**既定**、 **Optimistic**、または**完全**します。  
  
    -   カスタム設定を指定するには、選択するか、新しい設定または値を入力します。  
  
3.  クリックして**OK**設定を保存します。  
  
現在のプロジェクトの設定をカスタマイズすることもできます。 これらの設定は、現在のプロジェクト ファイルに保存されます。  
  
**現在のプロジェクトの設定をカスタマイズするには**  
  
1.  **ツール** メニューのをクリックして**プロジェクト設定**します。  
  
2.  **プロジェクト設定**ダイアログ ボックスで、次の手順のいずれかを使用します。  
  
    -   定義済みのモードを選択する、**モード**ドロップダウン ボックスで、**既定**、 **Optimistic**、または**完全**します。  
  
    -   カスタムのモードを指定する、**モード**ボックスで、**カスタム**、適切なプロジェクト設定を選択します。  
  
3.  クリックして**OK**設定を保存します。  
  
## <a name="next-steps"></a>次の手順  
移行の次の手順は、プロジェクトのニーズによって異なります。  
  
-   ソースとターゲットのデータ型のマッピングをカスタマイズするを参照してください。[マッピング Oracle および SQL Server データ型&#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)します。  
  
-   Oracle データベース オブジェクトの定義を変換する場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オブジェクト定義します。 詳細については、次を参照してください。 [Oracle スキーマの変換&#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md)します。  
  
## <a name="see-also"></a>参照  
[Oracle と SQL Server データ型のマッピング&#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)  
  
