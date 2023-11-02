### 1、git怎么忽略.idea文件夹中的内容出现在change list中

要在Git中忽略`.idea`文件夹及其内容，以防止其出现在变更列表中，你可以使用`.gitignore`文件来定义要忽略的文件和文件夹。`.gitignore`文件包含一些通配符规则，告诉Git哪些文件和文件夹应该被忽略。

下面是一些步骤来实现这一目标：

1. 创建或编辑`.gitignore`文件：在你的Git仓库根目录下，创建一个名为`.gitignore`的文件，如果它不存在的话。

2. 在`.gitignore`文件中添加如下内容，以忽略`.idea`文件夹：

   ```plaintext
   .idea/
   ```

   这会告诉Git忽略`.idea`文件夹及其下的所有内容。

3. 保存并提交`.gitignore`文件到Git仓库：

   ```bash
   git add .gitignore
   git commit -m "添加.gitignore文件以忽略.idea文件夹"
   ```

4. 确保你的`.gitignore`文件已经提交到Git仓库。之后，任何在`.idea`文件夹中的更改将不会出现在变更列表中，也不会被Git跟踪。

如果你已经在Git仓库中添加了`.idea`文件夹的内容，需要在添加`.gitignore`文件后，使用以下命令将`.idea`文件夹的内容从Git仓库中移除：

```bash
git rm -r --cached .idea/
```

这将从Git中移除`.idea`文件夹的内容，但保留本地文件。然后，提交这一变更。这样，`.idea`文件夹及其内容将不再受Git版本控制，并且不会出现在变更列表中。

### 2、git default changelist中出现了target文件中的文件，怎么移除

Git的默认更改列表（default changelist）通常是IDEA中的功能，用于暂时存放你的更改，但不会将它们提交到版本控制系统中。如果`target`文件夹中的文件出现在默认更改列表中，你可以执行以下步骤来将它们从默认更改列表中移除：

1. 打开IDEA：确保你的项目已在IntelliJ IDEA中打开。

2. 打开"Version Control"工具窗口：
   - 在IDEA中，点击右下角的"Version Control"图标（通常是一个圆圈中的齿轮图标）来打开"Version Control"工具窗口。

3. 默认更改列表（Default Changelist）：
   - 在"Version Control"工具窗口中，你会看到一个名为"Default Changelist"的更改列表，其中包含了你尚未提交的更改。

4. 移除更改：
   - 在 "Default Changelist" 下，找到 `target` 文件夹中的文件。
   - 右键单击这些文件，并选择 "Move to Another Changelist"（移到另一个更改列表）。
   - 选择一个自定义的更改列表或创建一个新的更改列表，并将这些文件移动到这个新的更改列表中。

5. 提交更改：
   - 一旦你将这些文件从默认更改列表中移除，你可以选择是否将它们包含在提交中。如果不想提交它们，只需提交默认更改列表中的其他更改即可。

这将允许你从默认更改列表中将`target`文件夹中的文件分离出来，并在需要时将它们包含在提交中。请注意，Git仍然会跟踪`target`文件夹中的文件，但它们不再出现在默认更改列表中。如果你不想让Git跟踪`target`文件夹中的文件，你可以将它们添加到`.gitignore`文件中，如前面的回答中所述。

### 3、idea的default changelist中文件的颜色表示什么意思

在IntelliJ IDEA的Default Changelist中，文件的颜色通常用来表示文件的状态。不同颜色表示不同的状态，以下是一些常见的颜色和它们的含义：

1. **绿色**：绿色通常表示文件已被添加到Git暂存区（Staged）。这意味着文件已经准备好提交。

2. **蓝色**：蓝色表示文件在工作目录中有修改，但尚未添加到Git暂存区。这些修改尚未被Git跟踪。

3. **灰色**：灰色通常表示文件未被Git跟踪，即它是新添加的文件或是在`.gitignore`中被忽略的文件。

4. **红色**：红色表示文件已被删除或移动，但这些更改尚未被Git跟踪。

这些颜色表示可以帮助你更容易地识别在Default Changelist中的文件的状态。你可以根据这些颜色来判断是否需要将文件添加到Git暂存区，或者提交你的更改。这有助于版本控制和跟踪项目中的文件状态。