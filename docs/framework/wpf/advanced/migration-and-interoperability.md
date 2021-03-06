---
title: 移行と相互運用性
ms.date: 03/30/2017
f1_keywords:
- AutoGeneratedOrientationPage
helpviewer_keywords:
- Windows Presentation Foundation [WPF], interoperability
- WPF [WPF], migration
- Windows Forms controls [WPF interoperability]
- controls [WPF interoperability]
- Windows Presentation Foundation [WPF], migration
- interoperability [WPF]
- WPF [WPF], interoperability
- migration [WPF]
ms.assetid: d655de05-bf63-4814-bc64-6b3be01c70a2
ms.openlocfilehash: fcb7ece1081ae0858148cef883429b205478689b
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73040890"
---
# <a name="migration-and-interoperability"></a>移行と相互運用性
このページには、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] アプリケーションとその他の種類の Microsoft Windows アプリケーションとの間の相互運用を実装する方法について説明しているドキュメントへのリンクが含まれています。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [WPF と Windows フォームの相互運用性](wpf-and-windows-forms-interoperation.md)  
 [WPF と Win32 の相互運用性](wpf-and-win32-interoperation.md)  
 [WPF と Direct3D9 の相互運用性](wpf-and-direct3d9-interoperation.md)  
  
## <a name="reference"></a>参照  
  
|用語|定義|  
|----------|----------------|  
|<xref:System.Windows.Forms.Integration.WindowsFormsHost>|[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ページの要素として [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] コントロールをホストするために使用できる要素。|  
|<xref:System.Windows.Forms.Integration.ElementHost>|[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] コントロールをホストするために使用できる [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] コントロール。|  
|<xref:System.Windows.Interop.HwndSource>|[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] アプリケーション内の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 領域をホストします。|  
|<xref:System.Windows.Interop.HwndHost>|<xref:System.Windows.Forms.Integration.WindowsFormsHost>の基本クラスは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションによってホストされるときに、すべての HWND ベースのテクノロジが使用するいくつかの基本的な機能を定義します。 これをサブクラス化して、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーション内の [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] ウィンドウをホストします。|  
|<xref:System.Windows.Interop.BrowserInteropHelper>|ブラウザーでホストされている [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションのブラウザー環境の条件を報告するためのヘルパークラス。|  
  
## <a name="related-sections"></a>関連項目
