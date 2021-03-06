---
title: '方法: ユーザー インターフェイスを持たないコントロールを Windows フォームに追加する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
f1_keywords:
- NonVisualSelection
helpviewer_keywords:
- invisible controls [Windows Forms]
- Windows Forms controls, adding to form
- controls [Windows Forms], nonvisual
- Windows Forms controls, nonvisual
- nonvisual controls [Windows Forms]
ms.assetid: 52134d9c-cff6-4eed-8e2b-3d5eb3bd494e
ms.openlocfilehash: bc1f844e5a2cf4d4f3b64ebf20e935f36ff85e12
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2019
ms.locfileid: "69987084"
---
# <a name="how-to-add-controls-without-a-user-interface-to-windows-forms"></a>方法: ユーザー インターフェイスを持たないコントロールを Windows フォームに追加する

非可視のコントロール (またはコンポーネント) は、アプリケーションに機能を提供します。 他のコントロールとは異なり、コンポーネントはユーザーにユーザーインターフェイスを提供しないため、Windows フォームデザイナー画面に表示する必要はありません。 コンポーネントがフォームに追加されると、すべてのコンポーネントが表示されるフォームの下部に、サイズ変更可能なトレイ Windows フォームデザイナーが表示されます。 コンポーネントトレイにコントロールが追加されたら、コンポーネントを選択し、フォーム上の他のコントロールと同様にそのプロパティを設定できます。

## <a name="add-a-component-to-a-windows-form"></a>Windows フォームへのコンポーネントの追加

1. Visual Studio でフォームを開きます。 詳細については、「[方法: デザイナー](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/w5yd62ts(v=vs.100))で Windows フォームを表示します。

2. **ツールボックス**でコンポーネントをクリックし、フォームにドラッグします。

     コンポーネントがコンポーネントトレイに表示されます。

また、実行時にコンポーネントをフォームに追加することもできます。 これは、特に、ユーザーインターフェイスを持つコントロールとは異なり、コンポーネントにはビジュアル式がないため、一般的なシナリオです。 次の例では、 <xref:System.Windows.Forms.Timer>コンポーネントが実行時に追加されます。 (Visual Studio にはさまざまなタイマーが含まれていることに注意してください<xref:System.Windows.Forms.Timer> 。この場合は、Windows フォームコンポーネントを使用します。 Visual Studio でのさまざまなタイマーの詳細については、「[サーバーベースのタイマーの概要](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/tb9yt5e6(v=vs.90))」を参照してください)。

> [!CAUTION]
> コンポーネントには、多くの場合、コンポーネントを効果的に機能させるために設定する必要があるコントロール固有のプロパティがあります。 以下の<xref:System.Windows.Forms.Timer>コンポーネントの場合は、 `Interval`プロパティを設定します。 コンポーネントをプロジェクトに追加するときは、そのコンポーネントに必要なプロパティを設定します。

## <a name="add-a-component-to-a-windows-form-programmatically"></a>プログラムによって Windows フォームにコンポーネントを追加する

1. コードで<xref:System.Windows.Forms.Timer>クラスのインスタンスを作成します。

2. タイマーの`Interval`タイマー刻みの間隔を決定するには、プロパティを設定します。

3. コンポーネントに必要なその他のプロパティを構成します。

     次のコードは、 <xref:System.Windows.Forms.Timer> `Interval`プロパティセットを使用したの作成を示しています。

    ```vb
    Public Sub CreateTimer()
       Dim timerKeepTrack As New System.Windows.Forms.Timer
       timerKeepTrack.Interval = 1000
    End Sub
    ```

    ```csharp
    public void createTimer()
    {
       System.Windows.Forms.Timer timerKeepTrack = new
           System.Windows.Forms.Timer();
       timerKeepTrack.Interval = 1000;
    }
    ```

    ```cpp
    public:
       void createTimer()
       {
          System::Windows::Forms::Timer^ timerKeepTrack = gcnew
             System::Windows::Forms::Timer();
          timerKeepTrack->Interval = 1000;
       }
    ```

    > [!IMPORTANT]
    > 悪意のある UserControl を参照することにより、ネットワーク経由でローカルコンピューターをセキュリティ上のリスクにさらすことがあります。 これは、悪意のあるユーザーが有害なカスタムコントロールを作成した後、誤ってプロジェクトに追加した場合にのみ問題になります。

## <a name="see-also"></a>関連項目

- [Windows フォーム コントロール](index.md)
- [方法: コントロールを Windows フォームに追加する](how-to-add-controls-to-windows-forms.md)
- [方法: Windows フォームに ActiveX コントロールを追加する](how-to-add-activex-controls-to-windows-forms.md)
- [Windows フォームへのコントロールの追加](putting-controls-on-windows-forms.md)
- [各 Windows フォーム コントロールのラベル設定とショートカットの作成](labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)
- [Windows フォームで使用するコントロール](controls-to-use-on-windows-forms.md)
- [Windows フォーム コントロールの機能別一覧](windows-forms-controls-by-function.md)
