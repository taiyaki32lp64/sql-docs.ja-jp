---
title: スクリプト コンポーネント エディターでのスクリプト コンポーネントの構成 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script component
- Script Component Editor
- SSIS Script component, configuring
- Script component [Integration Services], configuring
ms.assetid: 586dd799-f383-4d6d-b1a1-f09233d14f0a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1b2b588c61742d5ab9c57d934b0f4f11230f1ca5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62894816"
---
# <a name="configuring-the-script-component-in-the-script-component-editor"></a>スクリプト コンポーネント エディターでのスクリプト コンポーネントの構成
  スクリプト コンポーネント内でカスタム コードを記述する前に、作成するデータ フロー コンポーネントの種類 (変換元、変換、または変換先) を選択し、 **[スクリプト変換エディター]** でスクリプト コンポーネントのメタデータおよびプロパティを構成する必要があります。  
  
## <a name="selecting-the-type-of-component-to-create"></a>作成するコンポーネントの種類の選択  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーの [データ フロー] ペインにスクリプト コンポーネントを追加すると、 **[スクリプト コンポーネントの種類を選択]** ダイアログ ボックスが表示されます。 コンポーネントをあらかじめ、変換元、変換、または変換先として構成しておきます。 最初にこれを選択したら、引き続き **[スクリプト変換エディター]** でスクリプト コンポーネントを構成できます。  
  
 スクリプト コンポーネントの既定のスクリプト言語を設定するには、 **[オプション]** ダイアログ ボックスの **[全般]** ページにある **[スクリプト言語]** オプションを使用します。 詳細については、「 [General Page](../../general-page-of-integration-services-designers-options.md)」を参照してください。  
  
## <a name="understanding-the-two-design-time-modes"></a>デザイン時の 2 つのモードについて  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーでは、スクリプト コンポーネントにメタデータ デザイン モードとコード デザイン モードの 2 つのモードがあります。  
  
 **[スクリプト変換エディター]** を開くと、スクリプト コンポーネントはメタデータ デザイン モードになります。 このモードでは、入力列の選択、および出力と出力列の追加または構成を行うことができますが、コードは記述できません。 このコンポーネントのメタデータを構成した後で、コード デザイン モードに切り替えてスクリプトを記述できます。  
  
 **[スクリプトの編集]** をクリックしてコード デザイン モードに切り替えると、スクリプト コンポーネントではメタデータがロックされ、追加の変更ができなくなり、入力と出力のメタデータから基本コードが自動的に生成されます。 コードの自動生成が完了すると、カスタム コードを入力できるようになります。 作成したコードは自動生成された基本クラスを使用し、すべて厳密に型指定されたオブジェクトとして、入力行の処理、バッファーおよびバッファー内の列へのアクセス、およびパッケージからの接続マネージャーと変数の取得を行います。  
  
 コード デザイン モードでカスタム コードを入力したら、モードを切り替えてメタデータ デザイン モードに戻すことができます。 これによって入力したコードが削除されることはありませんが、次にメタデータを変更すると、基本クラスが再生成されます。 その後、カスタム コードが参照するオブジェクトが存在しないか、または変更されたために、コンポーネントの検証に失敗する可能性があります。 その場合、再生成された基本クラスに対してコードが正常にコンパイルされるように、コードを手動で修正する必要があります。  
  
## <a name="configuring-the-component-in-metadata-design-mode"></a>メタデータ デザイン モードでのコンポーネントの構成  
 メタデータ デザイン モードでは、入力列の選択、および出力と出力列の追加や構成を行うことができますが、コードは記述できません。 コンポーネントのメタデータを構成した後で、コード デザイン モードに切り替えてスクリプトを記述します。  
  
 カスタム エディターで構成する必要のあるプロパティは、スクリプト コンポーネントの使用法に応じて異なります。 スクリプト コンポーネントは、変換元、変換、または変換先として構成できます。 コンポーネントの使用方法に応じて、入力または出力のどちらか、またはその両方がサポートされます。 記述するカスタム コードでは、入力および出力の行と列が処理されます。  
  
### <a name="inputs-columns-page-of-the-script-transformation-editor"></a>[スクリプト変換エディター] の [入力列] ページ  
 変換および変換先では、 **[スクリプト変換エディター]** の **[入力列]** ページが表示されます。変換元では表示されません。 このページでは、使用できる入力列から、使用するカスタム スクリプトを選択し、その入力列に読み取り専用でアクセスするか、または読み取り/書き込みでアクセスするかを指定します。  
  
 このメタデータに基づいて生成されるコード プロジェクトでは、BufferWrapper プロジェクト アイテムに、各入力のクラスが含まれます。このクラスには、選択した各入力列用の型指定されたアクセサー プロパティが含まれています。 たとえば、整数値を選択する**CustomerID**列と文字列**CustomerName**という名前の入力からの列`CustomerInput`、BufferWrapper プロジェクト アイテムが含まれます、`CustomerInput`クラス派生した<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>、および`CustomerInput`クラスが名前付き整数のプロパティを公開**CustomerID**という名前の文字列プロパティと**CustomerName**します。 この規則により、次のような型チェック付きのコードが記述できます。  
  
```vb  
Dim currentCustomerID as Integer = CustomerInput.CustomerID  
Dim currentCustomerName as String = CustomerInput.CustomerName  
```  
  
 特定の種類のデータ フロー コンポーネントの入力列を構成する方法の詳細については、「[特定の種類のスクリプト コンポーネントの開発](../../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)」で、該当する例を参照してください。  
  
### <a name="inputs-and-outputs-page-of-the-script-transformation-editor"></a>[スクリプト変換エディター] の [入力および出力] ページ  
 変換元、変換、および変換先では、 **[スクリプト変換エディター]** の **[入力および出力]** ページが表示されます。 このページでは、カスタム スクリプトで使用する入力、出力、および出力列を追加、削除、および構成します。ただし、次のような制限があります。  
  
-   スクリプト コンポーネントを変換元として使用する場合、入力はありませんが複数の出力がサポートされます。  
  
-   スクリプト コンポーネントを変換として使用する場合、1 つの入力と複数の出力がサポートされます。  
  
-   スクリプト コンポーネントを変換先として使用する場合、1 つの入力がサポートされますが出力はありません。  
  
 このメタデータに基づいて生成されるコード プロジェクトでは、BufferWrapper プロジェクト アイテムに、各入力および出力のクラスが含まれます。 という名前の出力を作成する場合など`CustomerOutput`、BufferWrapper プロジェクト アイテムが含まれます、`CustomerOutput`から派生したクラス<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>、および`CustomerOutput`クラスが作成された各出力列の型指定されたアクセサー プロパティを格納します。  
  
 出力列は、 **[入力および出力]** ページでのみ構成できます。 変換および変換先の入力列は、 **[入力列]** ページで選択できます。 BufferWrapper プロジェクト アイテムで作成された、型指定されたアクセサー プロパティは、出力列の書き込み専用プロパティです。 入力列のアクセサー プロパティは、 **[入力列]** ページで各列に選択した使用法の種類に応じて、読み取り専用または読み取り/書き込みのプロパティになります。  
  
 特定の種類のデータ フロー コンポーネントの入力および出力を構成する方法の詳細については、「[特定の種類のスクリプト コンポーネントの開発](../../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)」で、該当する例を参照してください。  
  
> [!NOTE]  
>  エラー行の自動処理のスクリプト コンポーネントでエラー出力として出力を直接構成することはできませんが、別の出力を作成するか、可能な場合はスクリプトを使用してこの出力に行を送信することによって、エラー出力の機能を再現することができます。 詳細については、「[スクリプト コンポーネントに対するエラー出力のシミュレート](../../data-flow/transformations/script-component.md)」を参照してください。  
  
#### <a name="exclusiongroup-and-synchronousinputid-properties-of-outputs"></a>出力の ExclusionGroup プロパティおよび SynchronousInputID プロパティ  
 `ExclusionGroup` プロパティは、同期出力型の変換でのみ、0 以外の値になります。この場合、コードはフィルターまたは分岐を実行し、各行を、`ExclusionGroup` の 0 以外の同じ値を共有する出力の 1 つに送ります。 たとえば変換は、行を既定の出力またはエラー出力のどちらかに送信できます。 この場合に追加の出力を作成するには、`SynchronousInputID` プロパティの値が、コンポーネントの入力の `ID` と一致する整数に設定されていることを確認します。  
  
 `SynchronousInputID` プロパティは、同期出力型の変換でのみ、0 以外の値になります。 このプロパティの値が 0 の場合、出力が非同期型であることを示します。 同期出力では、新しい行を追加せず、選択した出力に行が渡されます。このプロパティには、コンポーネントの入力の `ID` が含まれている必要があります。  
  
> [!NOTE]  
>  ときに、**スクリプト変換エディター**最初の出力では、エディターのセットを作成、`SynchronousInputID`への出力のプロパティ、`ID`コンポーネントの入力。 しかし、その後の出力時には、出力の `SynchronousInputID` プロパティが 0 に設定されます。  
>   
>  同期出力型コンポーネントを作成する場合、各出力があります、`SynchronousInputID`プロパティに設定、`ID`コンポーネントの入力。 このため、最初の出力後は、エディターで出力を作成するたびに、`SynchronousInputID` 値を 0 からコンポーネントの入力の `ID` に変更する必要があります。  
>   
>  非同期出力型コンポーネントを作成する場合、各出力の `SynchronousInputID` プロパティを 0 に設定する必要があります。 そのため、最初の出力があります、`SynchronousInputID`値から変更、`ID`を 0 に、コンポーネントの入力。  
  
 スクリプト コンポーネントで 2 つの同期出力のうちのいずれかに行を送信する例については、「[スクリプト コンポーネントによる同期変換の作成](../../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)」を参照してください。  
  
### <a name="object-names-in-generated-script"></a>生成されたスクリプトのオブジェクト名  
 スクリプト コンポーネントは、入力と出力の名前を解析し、入力と出力内の列の名前を解析します。次に、これらの名前に基づいて、BufferWrapper プロジェクト アイテムにクラスとプロパティを生成します。 見つかった名前に、Unicode カテゴリの `UppercaseLetter`、`LowercaseLetter`、`TitlecaseLetter`、`ModifierLetter`、`OtherLetter`、または `DecimalDigitLetter` に属していない文字が含まれている場合、無効な文字は生成された名前から削除されます。 たとえば、スペースは削除されるため、**FirstName** と **[First Name]** という名前の 2 つの入力列は、どちらも列名 **FirstName** を持つと解釈され、予期しない結果が生じます。 このような状況を防ぐには、スクリプト コンポーネントで使用される入力と出力の名前、および入力と出力の列の名前には、このセクションで一覧表示されている Unicode カテゴリに属する文字のみが含まれるようにする必要があります。  
  
### <a name="script-page-of-the-script-transformation-editor"></a>[スクリプト変換エディター] の [スクリプト] ページ  
 **[スクリプト変換エディター]** の **[スクリプト]** ページでは、スクリプト タスクに一意の名前および説明を割り当てます。 また、次のプロパティの値を割り当てることができます。  
  
> [!NOTE]  
>  [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] およびそれ以降のバージョンでは、すべてのスクリプトがプリコンパイル済みです。 以前のバージョンでは、タスクの `Precompile` プロパティを設定することによって、スクリプトをプリコンパイルするかどうかを指定していました。  
  
#### <a name="validateexternalmetadata-property"></a>ValidateExternalMetadata プロパティ  
 `ValidateExternalMetadata` プロパティのブール値は、コンポーネントがデザイン時に外部データ ソースに対する検証を実行するかどうか、または実行時まで検証を延期するかどうかを指定します。 既定では、このプロパティの値は `True` です。つまり、外部メタデータはデザイン時と実行時の両方で検証されます。 外部データ ソースをデザイン時に使用しない場合、たとえば、パッケージの実行時にのみ外部データ ソースをダウンロードしたり、変換先を作成する場合には、このプロパティの値を `False` に設定できます。  
  
#### <a name="readonlyvariables-and-readwritevariables-properties"></a>ReadOnlyVariables プロパティおよび ReadWriteVariables プロパティ  
 既存の変数をコンマ区切りリストとして、これらのプロパティの値に入力すると、スクリプト コンポーネントのコード内で、その変数に読み取り専用アクセスまたは読み取り/書き込みアクセスできるようになります。 変数には、自動生成された基本クラスの <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadOnlyVariables%2A> および <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadWriteVariables%2A> プロパティを介して、コード内でアクセスします。 詳しくは、「[スクリプト コンポーネントでの変数の使用](using-variables-in-the-script-component.md)」をご覧ください。  
  
> [!NOTE]  
>  変数名の大文字と小文字は区別されます。  
  
#### <a name="scriptlanguage"></a>[ScriptLanguage]  
 スクリプト コンポーネントのプログラミング言語として、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic または [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# を選択できます。  
  
#### <a name="edit-script-button"></a>[スクリプトの編集] ボタン  
 **[スクリプトの編集]** ボタンをクリックすると [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE が開き、カスタム スクリプトを記述できます。 詳しくは、「[スクリプト コンポーネントのコーディングおよびデバッグ](coding-and-debugging-the-script-component.md)」をご覧ください。  
  
### <a name="connection-managers-page-of-the-script-transformation-editor"></a>[スクリプト変換エディター] の [接続マネージャー] ページ  
 **[スクリプト変換エディター]** の **[接続マネージャー]** ページでは、カスタム スクリプトで使用する接続マネージャーを追加および削除します。 通常、変換元または変換先コンポーネントを作成する場合は、接続マネージャーを参照する必要があります。  
  
 このメタデータに基づいて生成されるコード プロジェクトの `ComponentWrapper` プロジェクト アイテムには、選択した各接続マネージャー用の型指定されたアクセサー プロパティを格納する `Connections` コレクション クラスが含まれます。 型指定された各アクセサー プロパティの名前は、接続マネージャー自体の名前と同じであり、<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100> のインスタンスとして、接続マネージャーへの参照を返します。 たとえば、エディターの **[接続マネージャー]** ページに `MyADONETConnection` という名前の接続マネージャーを追加した場合、次のコードを使用して、スクリプト内のその接続マネージャーへの参照を取得できます。  
  
```vb  
Dim myADONETConnectionManager As IDTSConnectionManager100 = _  
    Me.Connections.MyADONETConnection  
```  
  
 詳しくは、「[スクリプト コンポーネントでのデータ ソースへの接続](connecting-to-data-sources-in-the-script-component.md)」をご覧ください。  
  
![Integration Services のアイコン (小)](../../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>関連項目  
 [スクリプト コンポーネントのコーディングおよびデバッグ](coding-and-debugging-the-script-component.md)  
  
  
