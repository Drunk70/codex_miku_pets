# Codex Pets

Codex 桌面宠物系统的宠物资源合集（[Codex 桌面宠物系统](https://github.com/codexorg/codex-pets)）。每个宠物都包含了导入 Codex 所需的全部文件：`pet.json` 描述符、`manifest.json` 动画状态映射文件，以及 WebP 格式的精灵图。

---

## 特性

- **两个可直接使用的宠物**：Q Miku Leek Pet 和兔子（三花猫 Tuzi）
- **像素风格精灵图**：1536 x 1872 像素，8 列 x 9 行，每格 192 x 208 像素
- **完整的状态覆盖**：待机、行走、奔跑、睡眠、思考、工作、成功、错误、等待
- **零代码**：纯资源包，只需将文件夹放入 Codex 的宠物目录即可

---

## 项目结构

```
pets/
├── README.md
├── q_miku_leek_pet/
│   ├── manifest.json      # 状态映射和元数据
│   ├── pet.json           # 宠物描述符
│   └── spritesheet.webp   # 动画精灵图
└── tuzi/
    ├── manifest.json
    ├── pet.json
    └── spritesheet.webp
```

---

## 安装说明

1. 克隆或下载此仓库。
2. 将一个或两个宠物文件夹（`q_miku_leek_pet` 和/或 `tuzi`）复制到 Codex 的宠物资源目录。典型路径为：

   ```
   ~/.codex/pets/
   ```

   或对于本地 Codex 安装：

   ```
   /path/to/codex/data/pets/
   ```

3. 重启 Codex。新宠物应该会出现在宠物选择器中。

如果宠物没有显示，请检查 `manifest.json` 和 `pet.json` 文件是否直接位于每个宠物文件夹内，而不是嵌套在更深一层。

---

## 宠物

### Q Miku Leek Pet

| 属性          | 值                                            |
|---------------|-----------------------------------------------|
| ID            | `q-miku-leek-pet`                             |
| 显示名称      | Q Miku Leek Pet                               |
| 描述          | 一只可爱的 Q 风格青色双马尾像素宠物，戴着未来风格的耳机，手持一根绿色的韭菜。 |

**支持的状态：** idle、running-right、running-left、waving、jumping、failed、waiting、running、review

---

### 兔子 (Tuzi)

| 属性          | 值                                            |
|---------------|-----------------------------------------------|
| ID            | `tuzi`                                        |
| 显示名称      | 兔子                                          |
| 描述          | 一只 Q 版三花狸猫，有着绿色的眼睛、白色胸口和爪子，还戴着一条柔软的蓝色围巾。 |

**支持的状态：** idle、running-right、running-left、waving、jumping、failed、waiting、running、review

---

## 配置格式

### `pet.json`

运行时 Codex 加载的最小化宠物描述符。

```json
{
  "id": "q-miku-leek-pet",
  "displayName": "Q Miku Leek Pet",
  "description": "A cute Q-style teal twin-tail pixel pet...",
  "spritesheetPath": "spritesheet.webp"
}
```

| 字段             | 用途                                           |
|------------------|----------------------------------------------|
| `id`             | 宠物的唯一标识符                              |
| `displayName`   | 在 Codex UI 中显示的人类可读名称              |
| `description`    | 宠物外观的简短描述                            |
| `spritesheetPath`| 精灵图的文件名（相对路径）                    |

---

### `manifest.json`

记录元数据并将 Codex 操作名称映射到精灵图中的实际动画行。Codex 本身不读取此文件，这是为资源发布者提供的。

```json
{
  "id": "q-miku-leek-pet",
  "folder": "q_miku_leek_pet",
  "displayName": "Q Miku Leek Pet",
  "description": "...",
  "codexPetFile": "pet.json",
  "spritesheet": {
    "path": "spritesheet.webp",
    "format": "WEBP",
    "mode": "RGBA",
    "width": 1536,
    "height": 1872,
    "cellWidth": 192,
    "cellHeight": 208,
    "columns": 8,
    "rows": 9
  },
  "requestedStateMapping": {
    "idle": "idle",
    "walk": "running-right / running-left",
    "run": "running-right / running-left",
    "sleep": "waiting",
    "thinking": "review",
    "working": "running",
    "success": "jumping / waving",
    "error": "failed",
    "waiting": "waiting"
  },
  "codexStates": [
    "idle", "running-right", "running-left", "waving",
    "jumping", "failed", "waiting", "running", "review"
  ],
  "notes": "..."
}
```

| 字段                             | 用途                                              |
|----------------------------------|-------------------------------------------------|
| `id`                             | 与 `pet.json` 的 `id` 相同                       |
| `folder`                         | 所属文件夹名称                                    |
| `codexPetFile`                   | Codex 将加载的文件名（`pet.json`）              |
| `spritesheet.path`               | 精灵图文件名                                      |
| `spritesheet.format`             | 图片格式（`WEBP`）                                |
| `spritesheet.mode`               | 颜色模式（`RGBA`）                                |
| `spritesheet.width/height`       | 完整精灵图尺寸（像素）                            |
| `spritesheet.cellWidth/cellHeight` | 每个动画帧的尺寸（像素）                        |
| `spritesheet.columns/rows`       | 精灵图的网格布局                                  |
| `requestedStateMapping`          | 将 Codex 操作名称映射到精灵图中的动画名称        |
| `codexStates`                    | 此宠物支持的所有动画状态列表                      |

---

## 精灵图规格

所有宠物共享相同的网格布局，便于工具处理：

| 属性          | 值            |
|---------------|---------------|
| 尺寸          | 1536 x 1872 像素 |
| 单格尺寸      | 192 x 208 像素 |
| 布局          | 8 列 x 9 行   |
| 格式          | WEBP (RGBA)   |

每一行对应一个动画序列。Codex 的宠物引擎从上到下依次读取各行。

---

## 贡献指南

欢迎贡献。您可以通过以下方式添加新宠物：

1. 在仓库根目录下创建一个新的子目录。
2. 添加 `pet.json`、`manifest.json` 和 `spritesheet.webp` 文件。
3. 遵循上述精灵图规格（1536 x 1872 像素、8 x 9 网格、192 x 208 像素单格）。
4. 更新此 README 在宠物部分记录新宠物。

请保持 `manifest.json` 与 `pet.json` 同步（相同的 `id`、`displayName`、`description`）。

---

## 许可证

MIT 许可证

特此授予获得本软件及相关文档文件（"软件"）副本的任何人不受限制地处理本软件的权利，包括但不限于使用、复制、修改、合并、发布、分发、再许可和/或销售本软件副本的权利，并允许获得本软件的人员在满足以下条件的情况下这样做：

上述版权声明和本许可声明应包含在本软件的所有副本或重要部分中。

本软件按"原样"提供，不提供任何形式的明示或暗示保证，包括但不限于对适销性、特定用途适用性和非侵权性的保证。在任何情况下，作者或版权持有人均不对因本软件或使用或其他与本软件相关的交易而产生的任何索赔、损害或其他责任负责。