---
title: 演练：显示语句完成 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - statement completion
ms.assetid: f3152c4e-7673-4047-a079-2326941d1c83
author: madskristensen
ms.author: madsk
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- vssdk
ms.openlocfilehash: 78cbcc9b2efd37aa99906d7ed7708621ec213b2e
ms.sourcegitcommit: e3c3d2b185b689c5e32ab4e595abc1ac60b6b9a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2020
ms.locfileid: "76269069"
---
# <a name="walkthrough-display-statement-completion"></a>演练：显示语句完成
您可以通过定义要为其提供完成的标识符，然后触发完成会话来实现基于语言的语句完成。 您可以在语言服务的上下文中定义语句结束，定义自己的文件扩展名和内容类型，然后仅为该类型显示完成。 或者，可以触发现有内容类型（例如，"纯文本"）的完成。 本演练演示如何为 "纯文本" 内容类型（文本文件的内容类型）触发语句结束。 "Text" 内容类型是所有其他内容类型（包括代码和 XML 文件）的上级。

 语句完成通常通过键入特定字符来触发，例如键入标识符的开头（例如 "using"）。 通常通过按**空格键**、 **Tab**或**Enter**键来提交选择。 可以通过使用击键（<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口）的命令处理程序和实现 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> 接口的处理程序提供程序来实现在键入字符时触发的 IntelliSense 功能。 若要创建完成源（即参与完成的标识符列表），请实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource> 接口和完成源提供程序（<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider> 接口）。 提供程序是 Managed Extensibility Framework （MEF）组件部件。 它们负责导出源和控制器类，以及导入服务和代理（例如 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>），该操作在文本缓冲区中启用导航，而 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>，这会触发完成会话。

 此演练演示如何为硬编码的标识符集实现语句结束。 在完整实现中，语言服务和语言文档负责提供该内容。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-mef-project"></a>创建 MEF 项目

#### <a name="to-create-a-mef-project"></a>创建 MEF 项目

1. 创建C# VSIX 项目。 （在 "**新建项目**" 对话框中，依次选择 "**视觉对象C#** "、"扩展性"、" **VSIX 项目**"。）将解决方案命名为 `CompletionTest`。

2. 将编辑器分类器项模板添加到项目。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

4. 将以下引用添加到项目，并确保**CopyLocal**设置为 `false`：

     Microsoft.VisualStudio.Editor

     Microsoft.VisualStudio.Language.Intellisense

     Microsoft.VisualStudio.OLE.Interop

     VisualStudio. 15。0

     Microsoft.VisualStudio.Shell.Immutable.10.0

     Microsoft.VisualStudio.TextManager.Interop

## <a name="implement-the-completion-source"></a>实现完成源
 完成源负责收集一组标识符，并在用户键入完成触发器时将内容添加到完成窗口，如标识符的第一个字母。 在此示例中，标识符及其说明在 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A> 方法中硬编码。 大多数情况下，使用语言的分析器来获取标记，以填充完成列表。

### <a name="to-implement-the-completion-source"></a>实现完成源

1. 添加一个类文件并将其命名为 `TestCompletionSource`。

2. 添加以下导入：

     [!code-csharp[VSSDKCompletionTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_1.cs)]
     [!code-vb[VSSDKCompletionTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_1.vb)]

3. 修改 `TestCompletionSource` 的类声明，使其实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>：

     [!code-csharp[VSSDKCompletionTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_2.cs)]
     [!code-vb[VSSDKCompletionTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_2.vb)]

4. 为源提供程序、文本缓冲区和 <xref:Microsoft.VisualStudio.Language.Intellisense.Completion> 对象（对应于将参与完成会话的标识符）的列表添加私有字段：

     [!code-csharp[VSSDKCompletionTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_3.cs)]
     [!code-vb[VSSDKCompletionTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_3.vb)]

5. 添加一个构造函数，用于设置源提供程序和缓冲区。 后面的步骤定义了 `TestCompletionSourceProvider` 类：

     [!code-csharp[VSSDKCompletionTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_4.cs)]
     [!code-vb[VSSDKCompletionTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_4.vb)]

6. 通过添加包含要在上下文中提供的完成的完成集来实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A> 方法。 每个完成集包含一组 <xref:Microsoft.VisualStudio.Language.Intellisense.Completion> 完成，并对应于完成窗口的一个选项卡。 （在 Visual Basic 项目中，完成窗口选项卡命名为**Common**和**All**。）`FindTokenSpanAtPosition` 方法是在下一步中定义的。

     [!code-csharp[VSSDKCompletionTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_5.cs)]
     [!code-vb[VSSDKCompletionTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_5.vb)]

7. 以下方法用于从光标位置查找当前单词：

     [!code-csharp[VSSDKCompletionTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_6.cs)]
     [!code-vb[VSSDKCompletionTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_6.vb)]

8. 实现 `Dispose()` 方法：

     [!code-csharp[VSSDKCompletionTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_7.cs)]
     [!code-vb[VSSDKCompletionTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_7.vb)]

## <a name="implement-the-completion-source-provider"></a>实现完成源提供程序
 完成源提供程序是实例化完成源的 MEF 组件部分。

### <a name="to-implement-the-completion-source-provider"></a>实现完成源提供程序

1. 添加一个名为 `TestCompletionSourceProvider` 的类，该类实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider>。 使用 "纯文本" <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> 和 "test 完成" <xref:Microsoft.VisualStudio.Utilities.NameAttribute> 导出此类。

     [!code-csharp[VSSDKCompletionTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_8.cs)]
     [!code-vb[VSSDKCompletionTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_8.vb)]

2. 导入 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>，它在完成源中查找当前单词。

     [!code-csharp[VSSDKCompletionTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_9.cs)]
     [!code-vb[VSSDKCompletionTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_9.vb)]

3. 实现 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider.TryCreateCompletionSource%2A> 方法来实例化完成源。

     [!code-csharp[VSSDKCompletionTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_10.cs)]
     [!code-vb[VSSDKCompletionTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_10.vb)]

## <a name="implement-the-completion-command-handler-provider"></a>实现完成命令处理程序提供程序
 完成命令处理程序提供程序是从一个 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>派生的，该提供程序侦听一个文本视图创建事件，并将该视图从 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>转换，这使得可以将命令添加到 Visual Studio shell 的命令链中-添加到 <xref:Microsoft.VisualStudio.Text.Editor.ITextView>。 由于此类是一个 MEF 导出，因此还可以使用它导入命令处理程序本身所需的服务。

#### <a name="to-implement-the-completion-command-handler-provider"></a>实现完成命令处理程序提供程序

1. 添加一个名为 `TestCompletionCommandHandler`的文件。

2. 添加以下 using 指令：

     [!code-csharp[VSSDKCompletionTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_11.cs)]
     [!code-vb[VSSDKCompletionTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_11.vb)]

3. 添加一个名为 `TestCompletionHandlerProvider` 的类，该类实现 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>。 使用 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> 的 "令牌完成处理程序"、"纯文本" <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> 和 <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Editable>来导出此类。

     [!code-csharp[VSSDKCompletionTest#12](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_12.cs)]
     [!code-vb[VSSDKCompletionTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_12.vb)]

4. 导入 <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>，这允许从 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 转换为 <xref:Microsoft.VisualStudio.Text.Editor.ITextView>、<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>和允许访问标准 Visual Studio 服务的 <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>。

     [!code-csharp[VSSDKCompletionTest#13](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_13.cs)]
     [!code-vb[VSSDKCompletionTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_13.vb)]

5. 实现 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A> 方法来实例化命令处理程序。

     [!code-csharp[VSSDKCompletionTest#14](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_14.cs)]
     [!code-vb[VSSDKCompletionTest#14](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_14.vb)]

## <a name="implement-the-completion-command-handler"></a>实现完成命令处理程序
 由于语句完成由击键触发，因此必须实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口以接收和处理触发、提交和消除完成会话的击键。

#### <a name="to-implement-the-completion-command-handler"></a>实现完成命令处理程序

1. 添加一个名为 `TestCompletionCommandHandler` 的类，该类实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>：

    [!code-csharp[VSSDKCompletionTest#15](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_15.cs)]
    [!code-vb[VSSDKCompletionTest#15](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_15.vb)]

2. 为下一个命令处理程序添加私有字段（传递命令）、文本视图、命令处理程序提供程序（启用对各种服务的访问权限）和完成会话：

    [!code-csharp[VSSDKCompletionTest#16](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_16.cs)]
    [!code-vb[VSSDKCompletionTest#16](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_16.vb)]

3. 添加一个构造函数，用于设置文本视图和提供程序字段，并将命令添加到命令链：

    [!code-csharp[VSSDKCompletionTest#17](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_17.cs)]
    [!code-vb[VSSDKCompletionTest#17](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_17.vb)]

4. 通过传递命令来实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 方法：

    [!code-csharp[VSSDKCompletionTest#18](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_18.cs)]
    [!code-vb[VSSDKCompletionTest#18](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_18.vb)]

5. 实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 方法。 此方法收到击键时，必须执行以下操作之一：

   - 允许将字符写入缓冲区，然后触发或筛选器完成。 （打印字符将执行此操作。）

   - 提交完成，但不允许将字符写入缓冲区。 （在显示完成会话时，空格、**选项卡**和**Enter**执行此操作。）

   - 允许将命令传递到下一个处理程序。 （所有其他命令。）

     由于此方法可能显示 UI，因此请调用 <xref:Microsoft.VisualStudio.Shell.VsShellUtilities.IsInAutomationFunction%2A> 以确保它不在自动化上下文中调用：

     [!code-csharp[VSSDKCompletionTest#19](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_19.cs)]
     [!code-vb[VSSDKCompletionTest#19](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_19.vb)]

6. 此代码是一个触发完成会话的私有方法：

    [!code-csharp[VSSDKCompletionTest#20](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_20.cs)]
    [!code-vb[VSSDKCompletionTest#20](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_20.vb)]

7. 下一个示例是取消订阅 <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSession.Dismissed> 事件的私有方法：

    [!code-csharp[VSSDKCompletionTest#21](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_21.cs)]
    [!code-vb[VSSDKCompletionTest#21](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_21.vb)]

## <a name="build-and-test-the-code"></a>生成和测试代码
 若要测试此代码，请生成 CompletionTest 解决方案并在实验实例中运行它。

#### <a name="to-build-and-test-the-completiontest-solution"></a>生成和测试 CompletionTest 解决方案

1. 生成解决方案。

2. 在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

3. 创建一个文本文件并键入一些文本，其中包括 "添加" 一词。

4. 键入第一个 "a" 和 "d" 时，应显示包含 "加法" 和 "适配" 的列表。 请注意，选择 "添加"。 如果键入其他 "d"，则该列表应仅包含 "加法"，此时将选择此选项。 可以按**空格键**、 **Tab**或**Enter**键提交 "加法"，也可以通过键入 Esc 或其他任何键来关闭列表。

## <a name="see-also"></a>另请参阅
- [演练：将内容类型链接到文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
