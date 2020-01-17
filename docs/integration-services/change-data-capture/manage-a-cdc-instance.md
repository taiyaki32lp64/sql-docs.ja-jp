---
title: CDC インスタンスの管理 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- manIns
ms.assetid: cfed22c8-c666-40ca-9e73-24d93e85ba92
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f145b536072314594af473488bc0b933c443230e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294690"
---
# <a name="manage-a-cdc-instance"></a>CDC インスタンスの管理

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  CDC デザイナー コンソールを使用して、作成したインスタンスに関する情報を表示し、インスタンスの操作を管理することができます。  
  
 インスタンスに関する情報を表示するには、左ペインでインスタンスの名前をクリックします。  
  
> [!NOTE]  
>  左ペインでサービスを選択すると、CDC デザイナー コンソールの中央に、使用可能なインスタンスの一覧も表示されます。 このセクションでいずれかのインスタンスを選択すると、右側のペインでタスクを実行できます。ただし、プロパティ タブの情報を表示することはできません。  
  
## <a name="what-you-can-do-when-you-display-the-cdc-instance-information"></a>CDC インスタンスの情報を表示しているときに実行できるタスク  
 次の操作を右側のペインから実行します。  
  
 **[開始]**  
 選択した CDC インスタンスについて変更のキャプチャを開始するには、 **[開始]** をクリックします。  
  
 **[停止]**  
 選択した CDC インスタンスについて変更のキャプチャを停止するには、 **[停止]** をクリックします。 CDC インスタンスを停止すると、その時点までにキャプチャされた変更は失われず、CDC インスタンスが再開されたときに伝達されます。  
  
 **リセット**  
 CDC インスタンスを初期 (空) の状態にリセットするには、 **[リセット]** をクリックします。 このオプションは、CDC インスタンスが停止しているときに使用できます。 変更テーブル内のすべての変更および CDC インスタンスの内部状態が削除されます。 CDC インスタンスが後から開始されると、変更キャプチャはその時点から開始され、CDC インスタンスの開始後に開始されたトランザクションのみがキャプチャの対象となります。  
  
 CDC インスタンスをリセットし、変更テーブルに書き込まれた変更を削除することを確認するには、確認のダイアログ ボックスで **[OK]** をクリックします。  
  
 **削除**  
 CDC インスタンスを完全に削除するには、 **[削除]** をクリックします。 このオプションは、CDC インスタンスが停止しているときにのみ使用できます。  
  
 CDC インスタンスを削除することを確認するには、確認のダイアログ ボックスで **[OK]** をクリックします。  
  
 **[Oracle ログ スクリプト]**  
 このリンクをクリックすると、Oracle 補足ログ スクリプトが表示された [Oracle ログ スクリプト] ダイアログ ボックスが表示されます。 このダイアログ ボックスで実行できる操作の詳細については、「 [Oracle Supplemental Logging Script](../../integration-services/change-data-capture/oracle-supplemental-logging-script.md)」を参照してください。  
  
> [!NOTE]  
>  補足ログ スクリプトを実行すると、[スクリプトを実行するための Oracle 資格情報] ダイアログ ボックスが表示されます。このダイアログ ボックスで、有効な Oracle ユーザー名とパスワードを指定します。 適切な Oracle 資格情報を指定する方法については、「 [Oracle Credentials for Running Script](../../integration-services/change-data-capture/oracle-credentials-for-running-script.md)」を参照してください。  
  
 **[CDC インスタンス配置スクリプト]**  
 このリンクをクリックすると、CDC インスタンス配置スクリプトを表示する [CDC インスタンス配置スクリプト] ダイアログ ボックスが表示されます。 このダイアログ ボックスの詳細については、「 [CDC Instance Deployment Script](../../integration-services/change-data-capture/cdc-instance-deployment-script.md)」を参照してください。  
  
 **Properties**  
 このリンクをクリックすると、プロパティ エディターが表示されます。 CDC インスタンスの構成はプロパティ エディターを使用して編集します。 CDC インスタンスのプロパティの編集の詳細については、「 [Edit Instance Properties](../../integration-services/change-data-capture/edit-instance-properties.md)」を参照してください。  
  
 **ビューアーのタブ**  
  
 CDC インスタンスの情報を表示するときは、次に示すビューアーのタブを使用できます。 これらのタブに表示される情報は読み取り専用です。  
  
 **ステータス**  
 このタブには、CDC インスタンスの現在の状態に関する情報と統計が表示されます。 このタブには、次の情報が含まれています。  
  
-   **状態**: CDC インスタンスの現在の状態を示すアイコンです。 これらの状態を次に示します。  
  
    |||  
    |-|-|  
    |![エラー](../../integration-services/change-data-capture/media/error.gif "エラー")|**エラー**: 再試行できないエラーが発生したため、Oracle CDC インスタンスは実行されていません。 次の副状態が利用できます。<br /><br /> **間違った構成**: 手動の介入を必要とする構成エラーが発生しました。<br /><br /> **パスワードが必要**: Oracle CDC インスタンスのパスワードが設定されていないか、パスワードが無効です。<br /><br /> **予期しないエラー**: その他すべての回復できないエラーです。|  
    |![OK](../../integration-services/change-data-capture/media/okay.gif "OK")|**[実行中]** : CDC インスタンスが実行されていて、変更レコードが処理されています。 次の副状態が利用できます。<br /><br /> **アイドル状態**: すべての変更レコードが処理され、ターゲット変更テーブルに格納されました。 アクティブなトランザクションはこれ以上ありません。<br /><br /> **処理**: 変更テーブルにまだ書き込まれていない、処理中の変更レコードがあります。|  
    |![[停止]](../../integration-services/change-data-capture/media/stop.gif "[停止]")|**[停止]** : CDC インスタンスが実行されていません。 停止状態は、CDC インスタンスが正常に停止したことを示します。|  
    |![一時停止](../../integration-services/change-data-capture/media/paused.gif "一時停止")|**一時停止**: CDC インスタンスが実行されていますが、再試行できないエラーにより処理が中断されています。 次の副状態が利用できます。<br /><br /> **接続解除**: ソース Oracle データベースへの接続を確立できません。 接続が回復すると処理が再開されます。<br /><br /> **ストレージ**: 記憶領域がいっぱいです。 追加の記憶領域に空きができると処理が再開されます。<br /><br /> **ロガー**: ロガーは Oracle に接続されていますが、必要なトランザクション ログが利用できないなどの一時的な問題が発生しており、Oracle トランザクション ログを読み取ることができません。|  
  
-   **[詳細な状態]** : 現在の副状態です。  
  
-   **[状態メッセージ]** : 現在の状態についての詳細情報です。  
  
-   **[タイムスタンプ]** : CDC の状態が状態テーブルから最後に読み取られたときの UTC 時刻です。  
  
-   **[カウンター]** : このセクションでは、次の情報を監視します。  
  
    -   **[最後のトランザクションのタイムスタンプ]** : 変更テーブルに最後のトランザクションが書き込まれたローカル時刻です。  
  
    -   **[最後の変更のタイムスタンプ]** : ソース Oracle データベース トランザクション ログの Oracle CDC インスタンスによって確認された最新の変更のローカル時刻です。 CDC インスタンスの Oracle トランザクション ログの読み取りについての現在の待機時間に関する情報を提供します。  
  
    -   **[トランザクション ログの先頭 CN]** : Oracle トランザクション ログから読み取られた最新の変更番号 (CN) です。  
  
    -   **[トランザクション ログの末尾 CN]** : CDC インスタンスの復旧または再起動のための変更番号です。 再起動またはその他の種類の障害 (クラスターのフェールオーバーを含む) が発生した場合、Oracle CDC インスタンスはこの場所に移動します。  
  
    -   **[現在の CN]** : トランザクション ログではなく、ソース Oracle データベースで確認された最後の変更番号 (SCN) です。  
  
    -   **[アクティブなトランザクション数]** : Oracle CDC インスタンスによって処理され、まだ判断 (コミットまたはロールバック) が行われていないソース Oracle トランザクションの現在の数です。  
  
    -   **[ステージングされたトランザクション数]** : [cdc.xdbcdc_staged_transactions](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_staged_transactions) テーブルにステージングされたソース Oracle トランザクションの現在の数です。  
  
-   **[カウンター]** : このセクションでは、次の情報を監視します。  
  
    -   **[完了したトランザクション数]** : CDC インスタンスが最後にリセットされた後に完了したトランザクションの数です。 これには、対象のテーブルが含まれていないトランザクションは含まれません。  
  
    -   **[書き込まれた変更]** : SQL Server 変更テーブルに書き込まれた変更の数です。  
  
 **Oracle**  
 CDC インスタンスと、Oracle データベースに対する CDC インスタンスの接続に関する情報が表示されます。 このタブは読み取り専用です。 これらのプロパティを編集するには、左側のペインでインスタンスを右クリックし、 **[プロパティ]** を選択するか、右側のペインで **[プロパティ]** をクリックして [\<インスタンス> のプロパティ] ダイアログ ボックスを開きます。  
  
 これらのプロパティとその編集方法については、「 [Edit the Oracle Database Properties](../../integration-services/change-data-capture/edit-the-oracle-database-properties.md)」を参照してください。  
  
 **テーブル**  
 CDC インスタンスに含まれるテーブルについての情報を表示します。 列情報も表示されます。 このタブは読み取り専用です。 これらのプロパティを編集するには、左側のペインでインスタンスを右クリックし、 **[プロパティ]** を選択するか、右側のペインで **[プロパティ]** をクリックして [\<インスタンス> のプロパティ] ダイアログ ボックスを開きます。  
  
 これらのプロパティとその編集方法については、「 [Edit Tables](../../integration-services/change-data-capture/edit-tables.md)」を参照してください。  
  
 **詳細設定**  
 CDC インスタンスの詳細プロパティとプロパティ値を表示します。 このタブは読み取り専用です。 これらのプロパティを編集するには、左側のペインでインスタンスを右クリックし、 **[プロパティ]** を選択するか、右側のペインで **[プロパティ]** をクリックして [\<インスタンス> のプロパティ] ダイアログ ボックスを開きます。  
  
 これらのプロパティとその編集方法については、「 [Edit the Advanced Properties](../../integration-services/change-data-capture/edit-the-advanced-properties.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server 変更データベース インスタンスを作成する方法](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [CDC インスタンスのプロパティを表示する方法](../../integration-services/change-data-capture/how-to-view-the-cdc-instance-properties.md)   
 [CDC インスタンスのプロパティを編集する方法](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [新しいインスタンス ウィザードの使用](../../integration-services/change-data-capture/use-the-new-instance-wizard.md)  
  
  
