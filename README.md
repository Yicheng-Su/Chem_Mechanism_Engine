# Chem Mechanism Engine

[中文说明](#中文说明) | [English](#english)

## 中文说明

Chem Mechanism Engine 是一个在浏览器中运行的有机反应机理可视化与创作工具。用户可以从 SMILES 导入反应物和试剂，逐步录制成键、断键和键级变化，添加每一步的标题、提示与示意能量，并将完整反应保存为可分享的 `.cme.json` 文件。

其他用户可以打开这些 JSON 文件，以交互方式学习反应过程，也可以进入创作模式继续修改或扩展已有机理。

> 本项目用于机理教学、交流和可视化创作。自动电子记账、结构警告和能量曲线均为辅助功能，不能替代实验数据、量子化学计算或专业化学判断。

### 主要功能

- 在浏览器中播放和探索分步有机反应机理
- 从 SMILES 导入一个或多个分子
- 通过点击原子和化学键录制成键、断键及键级变化
- 自动跟踪孤对电子、形式电荷和部分常见结构问题
- 为每一步添加标题、操作提示、能量值和能量标签
- 自动生成示意性的反应能量曲线
- 回看、重录和扩展已有步骤
- 将反应保存为 `.cme.json` 文件并与他人分享
- 从反应文件夹批量读取反应，形成个人或共享的机理库

### 项目文件结构

建议保持以下目录结构：

```text
Chem_Mechanism_Engine/
├─ index.html
├─ lib/
│  └─ openchemlib-full.js
└─ reactions/
   ├─ example-1.cme.json
   └─ example-2.cme.json
```

`lib/openchemlib-full.js` 用于解析 SMILES。若移动 `index.html`，请同时保留同级的 `lib` 文件夹，否则“Import from SMILES”功能将不可用。

### 快速开始

1. 下载或克隆整个项目文件夹。
2. 使用最新版 Chrome 或 Edge 打开 `index.html`；也可以直接访问已发布的 GitHub Pages 网站。
3. 如果只是学习已有反应，点击顶部的 **Open Folder**，选择 `reactions` 文件夹。
4. 点击 **Choose Reaction**，从列表中选择一个反应。
5. 按页面提示完成交互，或使用前进、后退和自动播放按钮查看各步机理。

浏览器可能会询问是否允许读取所选文件夹。授权只用于读取本地反应文件；项目本身不需要服务器即可运行。

## 学习已有反应

### 打开反应库

1. 点击 **Open Folder**。
2. 选择包含 `.cme.json` 文件的文件夹，推荐使用项目自带的 `reactions/`。
3. 点击 **Choose Reaction**。
4. 从下拉列表中选择反应。

应用会扫描所选文件夹中的有效 `.cme.json` 文件。支持的浏览器通常会记住最近使用的反应文件夹；再次打开页面时，如果权限仍然有效，应用会尝试自动恢复该反应库。

### 操作反应步骤

- 按页面提示拖动分子或原子，使指定反应位点相互接近。
- 当步骤要求断键或降低键级时，点击相应化学键。
- 使用 **▶** 前进到下一步。
- 使用 **◀** 返回上一步。
- 使用 **↺** 重置到反应初始状态。
- 使用 **⏯** 开始或暂停自动播放。
- 使用孤对电子按钮显示或隐藏孤对电子。
- 使用声音按钮开启或关闭操作音效。
- 如果反应文件包含能量信息，页面会显示可拖动的能量曲线面板。

点击 **Close Reaction** 可关闭当前反应并返回空白状态。

## 创建新反应

### 1. 进入空白创作模式

如果当前已经加载了一个反应，先点击 **Close Reaction**。然后点击：

```text
Create Reaction
```

页面会进入创作模式，并显示浮动创作工具栏和步骤信息编辑区。

如果进入创作模式时已有反应处于加载状态，应用会把它作为可继续编辑的反应打开，而不是新建空白反应。

### 2. 创建或导入分子

当前版本通过 SMILES 创建新分子：

1. 点击创作工具栏中的 **Import from SMILES**。
2. 粘贴一个 SMILES，例如：

   ```text
   CC(=O)O
   ```

3. 点击 **Confirm**，或按 Enter 导入。
4. 拖动分子，将反应物和试剂排列到合适位置。

一次导入多个分子时，每行输入一个 SMILES：

```text
CC(=O)C
NCC
O
```

- Enter：确认并导入
- Shift+Enter：换行，继续输入下一个分子
- **显示所有氢原子**：决定导入时是否显式显示全部氢原子

从 ChemDraw 使用 `Edit → Copy As → SMILES` 获得的字符串也可以直接粘贴。

### 3. 设置初始状态

导入所有起始分子后：

1. 使用选择工具拖动并整理分子位置。
2. 在右侧编辑区填写反应名称。
3. 可为 Step 0 填写初始状态标题和提示。
4. 点击一次 **Create Step** 开始录制第一步。

第一次开始录制步骤时，当前画布会被捕获为该反应的初始状态。

## 录制反应步骤

### 录制与保存步骤

每一步使用“开始录制 → 执行结构变化 → 保存步骤”的方式创建：

1. 点击 **Create Step** 开始录制。
2. 在画布上完成该步涉及的成键、断键或键级变化。
3. 填写步骤标题，例如 `Step 1: Nucleophilic Attack`。
4. 填写给学习者的提示文字。
5. 可选：填写相对能量值和能量标签。
6. 再次点击同一个按钮，此时按钮功能为 **Save Step**。

重要区别：

- **Save Step**：把当前步骤加入内存中的反应文档。
- **Save As / Save**：把整个反应真正写入本地 `.cme.json` 文件。

只点击 Save Step 而不保存文件，关闭或刷新页面后仍可能丢失创作内容。

### 成键

1. 使用选择工具依次点击两个尚未成键的原子。
2. 两原子之间会出现成键候选提示。
3. 点击两原子之间的虚线中点，建立新键。

应用会尝试自动选择电子供体并更新孤对电子及形式电荷。

### 断键或降低键级

1. 依次点击一条现有化学键两端的原子。
2. 点击键的中点，降低一个键级；单键会被断开。
3. 断键后可在弹出的电子分配控件中调整电子归属。
4. 按 Enter 可确认当前电子分配。

### 提高键级

选择一条低于三键的现有化学键后，使用出现的键级控件提高键级。应用会尝试从合适的原子调用孤对电子。

### 使用 π 键进攻

1. 点击双键或三键的键线中部，将该 π 键选作电子源。
2. 点击被进攻的目标原子。
3. 在弹出菜单中选择对称成环，或选择向多重键某一端加成。

### 多动作步骤

一个步骤可以包含多个连续结构变化。保存此类步骤时，应用可能会询问哪些动作需要学习者亲自完成。被选中的动作会成为交互触发点，其他动作会在相邻触发点完成时自动应用。

### 步骤文字与能量

每一步可填写：

- 反应名称
- 步骤标题
- 学习提示或下一步操作说明
- 相对能量值
- 能量标签，例如 `Int1`、`TS2` 或 `Product`

点击 **自动生成曲线** 可根据当前记录的结构变化生成示意能量曲线。自动结果只用于教学展示，不是真实的热力学或动力学计算值。

## 选择、移动、复制与删除

- **Select & drag**：点击或拖动原子和分子。
- **Marquee select**：框选分子；框中只要包含该分子的一个原子，就会选择整个连通片段。
- **Eraser**：删除原子或已选择的结构。
- **Undo**：撤销最近一次结构操作，最多保留有限数量的撤销记录。
- Ctrl/Cmd+C：复制当前选中的原子或结构。
- Ctrl/Cmd+V：在鼠标附近粘贴复制的结构。
- Ctrl/Cmd+Z：撤销。
- Delete / Backspace：删除当前选择。

复制和粘贴使用应用内部剪贴板，不会修改系统剪贴板内容。

## 回看和修改已有步骤

在创作模式下：

- 点击 **Step back** 回看前一步。
- 点击 **Step forward** 返回后一步或最新状态。
- 在历史步骤位置进行结构编辑时，应用会询问是否重录该步骤。
- 重录完成后，应用会尝试保留仍然兼容的后续步骤。
- 如果后续步骤引用了已不存在的原子或化学键，应用会提示从冲突位置截断后续步骤。

修改已有步骤前建议先另存一份副本。

## 保存反应

### 首次保存

1. 确认当前没有正在录制但尚未保存的步骤。
2. 在反应名称输入框中填写名称。
3. 点击 **Save As**。
4. 将文件保存为：

   ```text
   reaction-name.cme.json
   ```

推荐保存到项目的 `reactions/` 文件夹。若之前通过 Open Folder 打开过该文件夹，支持 File System Access API 的浏览器会优先把保存窗口定位到这里，但首次保存仍需要用户确认文件名和位置。

### 后续保存

通过 Save As 创建或通过创作模式打开一个文件后，点击 **Save** 会覆盖当前 `.cme.json` 文件。

### 浏览器兼容说明

- Chrome/Edge：通常支持直接选择文件夹、另存为及覆盖保存。
- 不支持相关文件接口的浏览器：Save As 可能退化为下载 JSON 文件；用户需要手动把下载文件移动到 `reactions/`。
- 本项目目前没有后台自动保存。请在重要修改后主动点击 Save。

## 打开并继续编辑已有反应

打开反应有两种不同用途：

### 用于学习或播放

使用顶部的：

```text
Open Folder → Choose Reaction
```

它会读取一个文件夹内的多个 `.cme.json` 文件。

### 用于继续创作

1. 进入 **Create Reaction**。
2. 点击创作工具栏中的 **Open reaction file**。
3. 选择一个 `.cme.json` 文件。
4. 应用会加载到该反应的最终状态，可继续追加新步骤，或回看并重录旧步骤。

## 分享反应

分享时只需要发送对应的 `.cme.json` 文件。接收者可以：

- 将文件放入自己的 `reactions/` 文件夹，然后通过 Open Folder 加载；或
- 进入创作模式，使用 Open reaction file 打开并继续编辑。

建议同时提供反应名称、来源或参考文献、作者、版本日期，以及哪些能量值属于示意值。

## JSON 文件包含什么

`.cme.json` 文件通常保存：

- 反应名称和说明
- 初始原子、化学键、坐标、孤对电子和形式电荷相关信息
- 每一步的成键、断键、键级和电子变化
- 学习者需要完成的交互触发动作
- 步骤标题和提示
- 示意能量曲线

JSON 文件是可读文本，但建议优先通过应用进行编辑，以避免破坏原子 ID、步骤引用和文件格式。

## 常见问题

### Import from SMILES 不可用

确认 `lib/openchemlib-full.js` 存在，并且 `lib` 文件夹与 HTML 文件保持正确的相对位置。

### Choose Reaction 中没有内容

确认所选文件夹中存在以 `.cme.json` 结尾的有效反应文件。

### Save 按钮提示先使用 Save As

当前反应还没有关联到本地文件。先使用 Save As 创建文件，之后才能使用 Save 覆盖保存。

### 已保存步骤，但重新打开后找不到修改

Save Step 只保存步骤到当前内存文档。还需要点击 Save As 或 Save，把整个反应写入 JSON 文件。

### 自动能量曲线是否是真实 ΔG？

不是。自动曲线根据成键、断键及电荷变化生成，仅用于示意。需要可靠能量数据时，应使用实验结果或适当的计算化学方法，并手动填写数值。

---

## English

Chem Mechanism Engine is a browser-based tool for visualizing, authoring, and sharing organic reaction mechanisms. Users can import molecules from SMILES, record bond formation, bond cleavage, and bond-order changes step by step, annotate each step, and save the complete mechanism as a shareable `.cme.json` file.

Other users can open these files to study the mechanism interactively or continue editing and extending the reaction in Creator mode.

> This project is intended for mechanism education, communication, and visual authoring. Automated electron bookkeeping, structural warnings, and energy profiles are assistive features and do not replace experimental evidence, quantum-chemical calculations, or expert chemical judgment.

### Key features

- Interactive, stepwise playback of organic reaction mechanisms
- Import of one or multiple molecules from SMILES
- Visual recording of bond formation, bond cleavage, and bond-order changes
- Automated tracking of lone pairs, formal charges, and selected structural warnings
- Step titles, learner guidance, relative energies, and energy labels
- Automatically generated illustrative energy profiles
- Review, re-recording, and extension of existing steps
- Save and share reactions as `.cme.json` files
- Load a folder of reaction files as a personal or shared mechanism library

### Recommended project structure

```text
Chem_Mechanism_Engine/
├─ index.html
├─ lib/
│  └─ openchemlib-full.js
└─ reactions/
   ├─ example-1.cme.json
   └─ example-2.cme.json
```

`lib/openchemlib-full.js` is required for SMILES parsing. If you move `index.html`, keep the `lib` directory at the expected relative path.

### Quick start

1. Download or clone the complete project directory.
2. Open `index.html` in a recent version of Chrome or Edge, or visit the published GitHub Pages site.
3. To study an existing reaction, click **Open Folder** and select the `reactions` directory.
4. Click **Choose Reaction** and select a mechanism.
5. Follow the on-screen prompts, or use the forward, backward, reset, and autoplay controls.

## Studying an existing reaction

### Load a reaction library

1. Click **Open Folder**.
2. Select a directory containing `.cme.json` files, preferably the included `reactions/` directory.
3. Click **Choose Reaction**.
4. Select a reaction from the list.

The application scans the selected directory for valid `.cme.json` files. Supported browsers may remember the most recently used reaction directory and restore it on a later visit if permission remains available.

### Navigate a mechanism

- Follow the on-screen prompt and drag molecules or atoms to bring the requested reaction sites together.
- Click the indicated bond when a step requires bond cleavage or a decrease in bond order.
- Use **▶** and **◀** to move forward and backward.
- Use **↺** to reset the reaction.
- Use **⏯** to start or pause autoplay.
- Toggle lone-pair display and sound with the corresponding buttons.
- Reactions containing energy information display a draggable energy-profile panel.

Click **Close Reaction** to unload the current reaction.

## Creating a new reaction

### 1. Start with a blank canvas

If a reaction is currently loaded, click **Close Reaction** first. Then click **Create Reaction**.

If you enter Creator mode while a reaction is still loaded, the application adopts that reaction for continued editing instead of starting a new blank mechanism.

### 2. Create molecules from SMILES

1. Click **Import from SMILES** in the Creator toolbar.
2. Paste a SMILES string, such as `CC(=O)O`.
3. Click **Confirm** or press Enter.
4. Drag the imported molecules into a useful starting arrangement.

To import multiple molecules, enter one SMILES string per line. Use Shift+Enter to insert a new line and Enter to confirm the import. The explicit-hydrogen option controls whether all hydrogens are shown after import.

SMILES copied from ChemDraw with `Edit → Copy As → SMILES` can be pasted directly.

### 3. Define the initial state

1. Import all starting molecules.
2. Arrange the reactants and reagents on the canvas.
3. Enter a reaction name and optional Step 0 guidance.
4. Click **Create Step** once to begin recording Step 1.

The canvas is captured as the reaction's initial state when the first step recording begins.

## Recording mechanism steps

Each step follows the same workflow:

1. Click **Create Step** to begin recording.
2. Perform the bond and structural changes for that step.
3. Enter a step title and learner guidance.
4. Optionally provide a relative energy and energy label.
5. Click the same button again, now acting as **Save Step**.

Do not confuse the two levels of saving:

- **Save Step** adds the step to the in-memory reaction document.
- **Save As / Save** writes the complete reaction to a local `.cme.json` file.

Refreshing or closing the page before saving the file may discard the work.

### Form a bond

Select two atoms that are not currently bonded, then click the dashed midpoint between them. The engine attempts to assign an electron donor and update lone pairs and formal charges automatically.

### Break a bond or lower its order

Select the two atoms of an existing bond and click the bond midpoint. A multiple bond decreases by one order; a single bond is cleaved. Use the electron-assignment control to adjust the destination of the electron pair, and press Enter to confirm it.

### Raise a bond order

After selecting an existing bond below triple-bond order, use the bond-order control to raise its order. The engine attempts to use an available lone pair from a suitable atom.

### Use a π bond as a nucleophile

Click the middle of a double or triple bond, then click the target atom. Choose symmetric ring formation or addition to either end of the multiple bond from the displayed menu.

### Record multiple actions in one step

A step may contain several structural actions. When such a step is saved, the application may ask which actions the learner should perform manually. Selected actions become interactive gates; the remaining actions are applied automatically at the adjacent gate.

### Step text and energies

Each step can include a title, learner guidance, a relative energy, and a label such as `Int1`, `TS2`, or `Product`.

The automatic energy-profile feature generates an illustrative curve from the recorded structural changes. It is not a thermodynamic or kinetic calculation.

## Selection and keyboard shortcuts

- **Select & drag**: select and move atoms or fragments.
- **Marquee select**: drag a box to select connected molecular fragments.
- **Eraser**: remove atoms or the current selection.
- Ctrl/Cmd+Z: undo.
- Ctrl/Cmd+C: copy the current selection inside the application.
- Ctrl/Cmd+V: paste near the current pointer position.
- Delete / Backspace: delete the current selection.
- Enter: confirm the current electron assignment after bond cleavage.

## Reviewing and editing steps

Use **Step back** and **Step forward** in Creator mode to inspect recorded states. Editing a historical state starts an in-place re-recording workflow. The application attempts to preserve later steps that remain compatible and warns before truncating steps that reference missing atoms or bonds.

Save a backup copy before substantially changing an existing mechanism.

## Saving reactions

### First save

1. Finish and save any step currently being recorded.
2. Enter a reaction name.
3. Click **Save As**.
4. Save the file as `reaction-name.cme.json`.

The recommended destination is `reactions/`. If that folder was previously opened with **Open Folder**, a browser supporting the File System Access API normally starts the save dialog there. The first save still requires the user to confirm the location and filename.

### Later saves

After creating a file with Save As, or opening an existing file in Creator mode, **Save** overwrites the current `.cme.json` file.

The project currently has no background autosave. Save explicitly after important changes. In browsers without the required file APIs, Save As may download the JSON instead; move the downloaded file into `reactions/` manually.

## Opening a reaction for editing

To play a library of reactions, use **Open Folder → Choose Reaction**.

To edit one reaction:

1. Enter **Create Reaction** mode.
2. Click **Open reaction file** in the Creator toolbar.
3. Select a `.cme.json` file.
4. Continue from its final state, append steps, or review and re-record earlier steps.

## Sharing reactions

Share the relevant `.cme.json` file. A recipient can place it in their own `reactions/` directory and load that folder, or open the file directly in Creator mode for continued editing.

When sharing a mechanism, consider including its source or reference, author, version date, and a note identifying any illustrative energy values.

## JSON contents

A `.cme.json` file typically contains the reaction metadata, initial atoms and bonds, stepwise structural and electron changes, interactive learner triggers, step guidance, and an illustrative energy profile.

The format is human-readable, but editing it through the application is recommended because manual changes can break atom IDs, step references, or schema consistency.

## Troubleshooting

- **SMILES import is unavailable:** verify that `lib/openchemlib-full.js` exists at the expected relative path.
- **Choose Reaction is empty:** verify that the selected directory contains valid files ending in `.cme.json`.
- **Save asks for Save As first:** the current document is not yet associated with a writable local file.
- **A saved step disappeared after reopening:** Save Step only updates the in-memory document; use Save As or Save to write the complete JSON file.
- **Is the automatic energy curve a real ΔG profile?** No. It is an illustrative heuristic and should be replaced with defensible data when quantitative interpretation is needed.
