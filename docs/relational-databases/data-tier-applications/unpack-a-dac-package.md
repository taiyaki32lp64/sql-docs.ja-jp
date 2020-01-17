---
title: DAC パッケージのアンパック | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- wizard [DAC], unpack
- data-tier application [SQL Server], unpack
- How to [DAC], unpack
- unpack DAC
ms.assetid: 697b69b3-f157-4e22-ac4e-f65c5fc2d0ad
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5e2be902c241403ec044b3d348f90dc85327b8ad
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909531"
---
# <a name="unpack-a-dac-package"></a>DAC パッケージのアンパック
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [データ層アプリケーションのアンパック] ダイアログ ボックスでは、データ層アプリケーション (DAC) パッケージからスクリプトおよびファイルを解凍できます。 解凍されたスクリプトおよびファイルが配置されるフォルダーは、パッケージを使用して DAC を実稼働システムに配置する前に確認できます。 また、DAC の内容は、別のフォルダーにアンパックされた別のパッケージの内容と比較することもできます。  
  
1.  **作業を開始する準備:** [セキュリティ](#Security)  
  
2.  **DAC のアンパック:** [[データ層アプリケーションのアンパック] ダイアログの使用](#UnpackDACDial)、[DAC パッケージの内容の確認](#ExamDACPack)  

##  <a name="Security"></a> セキュリティ  
 ソースが不明または信頼されていない DAC パッケージは配置しないことをお勧めします。 こうした DAC には、意図しない [!INCLUDE[tsql](../../includes/tsql-md.md)] コードを実行したり、スキーマを変更してエラーを発生させるような、悪意のあるコードが含まれている可能性があります。 DAC のソースが不明または信頼されていない場合は、使用する前に、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]の隔離されたテスト インスタンスに DAC を配置し、DAC をアンパックして、ストアド プロシージャやその他のユーザー定義コードなどのコードを確認してください。  
  
##  <a name="UnpackDACDial"></a> [データ層アプリケーションのアンパック] ダイアログの使用  
 **DAC パッケージ ファイルをアンパックするには**  
  
-   **Windows エクスプローラー**で、DAC パッケージ (.dacpac) ファイルの場所に移動します。  
  
-   [データ層アプリケーションのアンパック] ダイアログ ボックスを開くには、次の 2 つの方法のいずれかを使用します。  
  
    1.  DAC パッケージ (.dacpac) ファイルを右クリックして、 **[アンパック]** をクリックします。  
  
    2.  DAC パッケージ ファイルをダブルクリックします。  
  
-   次のダイアログで必要な設定を行います。  
  
    -   [[Microsoft SQL Server DAC パッケージ ファイルのアンパック]](#Unpack)  
  
    -   [[フォルダーの参照]](#Browse)  
  
###  <a name="Unpack"></a> [Microsoft SQL Server DAC パッケージ ファイルのアンパック]  
 このページでは、アンパックされたファイルの配置先となるフォルダーを指定し、アンパック操作を実行します。  
  
 **[ファイルがアンパックされるフォルダー]:** アンパックされたファイルのフォルダーへの完全パスを指定します。 フォルダーが存在し、完全パスがわかっている場合は、このボックスにパスを入力します。 それ以外の場合は、 **[参照]** をクリックしてフォルダーに移動するか、新しいフォルダーを作成します。  
  
 **[参照]** : **[フォルダーの参照]** ページを開きます。このページでは、ファイル階層を移動してフォルダーを選択したり、新しいフォルダーを作成することができます。  
  
 **[アンパック]** : アンパック操作を開始します。  
  
 **[キャンセル]** : DAC パッケージをアンパックすることなく、ダイアログ ボックスを終了します。  
  
###  <a name="Browse"></a> [フォルダーの参照]  
 このページでは、アンパック操作の対象となるフォルダーを選択します。 また、必要に応じて、新しいフォルダーを作成することもできます。  
  
 **[フォルダー一覧]** : コンピューターのファイル階層を表示します。 ノードを展開し、DAC パッケージをアンパックするフォルダーに移動します。 フォルダーをクリックし、 **[OK]** をクリックします。  
  
 **[新しいフォルダーの作成]** : フォルダー階層で現在選択しているフォルダー内に作成する新しいフォルダーの名前を指定するダイアログ ボックスを開きます。  
  
 **[OK]** : **[DAC パッケージ ファイルのアンパック]** ページの **[ファイルがアンパックされるフォルダー]** ボックスで選択したフォルダーへのパスを配置して、そのページに戻ります。  
  
 **[キャンセル]** : フォルダーを選択することなく、ダイアログ ボックスを終了します。  
  
##  <a name="ExamDACPack"></a> DAC パッケージの内容の確認  
 パッケージをアンパックすると、 **[データ層アプリケーションのアンパック]** ダイアログ ボックスで作成されたファイルを確認することができます。 このダイアログ ボックスによって、選択した対象フォルダーに次のファイルが作成されます。  
  
1.  DAC で定義されたオブジェクトを作成するためのステートメントを含む Transact-SQL スクリプト。 ファイル名は *DACName*.sql です。この場合、 *DACName* は DAC の名前になります。  
  
2.  パッケージのすべての XML ファイル。  
  
3.  DAC の配置前ファイルまたは配置後ファイルなど、DAC の Extra Files セクションにあるすべてのファイル。  
  
 詳細については、「 [Validate a DAC Package](../../relational-databases/data-tier-applications/validate-a-dac-package.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [[データ層アプリケーション]](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [データ層アプリケーションの配置](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)   
 [データ層アプリケーションのアップグレード](../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md)  
  
  
