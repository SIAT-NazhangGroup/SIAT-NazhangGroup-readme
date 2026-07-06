# SIAT-NazhangGroup

中科院深圳先进技术研究院（SIAT）**医学影像组学与影像分析课题组**（Na Zhang 课题组）—— GitHub 组织主页仓库。

本仓库是 SIAT-NazhangGroup 的**组织级元仓库**，用于：
1. 介绍课题组研究方向与本账号发布内容的**用途声明**
2. 维护本组织下所有**仓库目录**
3. 制定本组织各仓库 README 的**编写规范**（输入/输出格式、模型托管、路径约定等）

> 本仓库为组织内部参考文档，**不含可运行代码或患者数据**。

---

## 目录

- [账号介绍与用途声明](#账号介绍与用途声明)
- [仓库目录](#仓库目录)
- [README 编写规范](#readme-编写规范)
  - [必含章节](#必含章节)
  - [输入格式约定](#输入格式约定)
  - [输出格式约定](#输出格式约定)
  - [模型权重托管约定](#模型权重托管约定)
  - [路径与隐私约定](#路径与隐私约定)
  - [标签值约定](#标签值约定)
- [许可证与引用](#许可证与引用)

---

## 账号介绍与用途声明

**研究方向**：面向重大疾病的医学影像定量分析，覆盖多模态 MRI（DCE、VWI / 高分辨血管壁成像等）的自动分割、肿瘤/斑块生境（habitat）与影像组学特征提取、以及面向临床预后/分型的机器学习建模。当前在研方向包括：

- **颅内动脉粥样硬化斑块影像分析**：颅内大血管（基底动脉、大脑中动脉等）高分辨率 MRI / VWI 血管壁成像的自动分割、斑块形态学与影像组学特征提取，服务于卒中复发风险与斑块负荷的临床研究。
- **乳腺癌肿瘤生境（habitat）分析**：基于多期相 DCE-MRI 的肿瘤内部异质性刻画（wash-in/wash-out 体素聚类 → habitat 子区域 → 影像组学特征 → 良恶性分类）。

**本账号发布内容类型**：

| 类型 | 说明 | 托管位置 |
|------|------|----------|
| **代码** | 分割网络、预处理/推理脚本、特征提取流水线 | GitHub |
| **工具** | Jupyter Notebook 工作流、命令行脚本 | GitHub |
| **模型** | 训练好的深度学习权重（`.pth` / `.ckpt` 等） | **Hugging Face** `SIAT-NazhangGroup/*` |
| **数据** | 患者相关数据表、影像组学特征表等（脱敏后） | **Hugging Face 私有数据集** `SIAT-NazhangGroup/*`（仅授权访问） |
| **资料** | 数据格式约定、使用说明、README 规范 | GitHub（本仓库及各仓库 README） |

**本账号明确不发布的内容**：
- 患者原始影像（DICOM / nii.gz 等可识别患者的信息）
- 患者标注数据
- 任何含 PHI（受保护健康信息）的内容

> 所有涉及患者数据的处理与上传须遵循伦理审查与数据使用协议。本组织 GitHub 仓库仅发布**方法代码**与**模型权重**，患者数据统一托管在 **Hugging Face 私有数据集仓库**，不发布在 GitHub。

---

## 仓库目录

### 公开仓库

| 仓库 | 简介 | 主要语言 | 模型权重 |
|------|------|----------|----------|
| [BA-T1-wall-lumen-seg](https://github.com/SIAT-NazhangGroup/BA-T1-wall-lumen-seg) | 基底动脉 T1 加权像血管壁/管腔自动分割（CBAM-PlaqueSegNet，2D 切片分割 + 3D 重建） | Python | [🤗 HF](https://huggingface.co/SIAT-NazhangGroup/BA-T1-wall-lumen-seg) |
| [plaque-morph-radio](https://github.com/SIAT-NazhangGroup/plaque-morph-radio) | 颅内动脉粥样硬化斑块 2D/3D 形态学与影像组学特征提取工具集（含 RR 重构比计算） | Jupyter Notebook | — |

### 内部仓库

| 仓库 | 简介 | 可见性 |
|------|------|--------|
| [Tumor-Habitat-Analysis-BreastCancer](https://github.com/SIAT-NazhangGroup/Tumor-Habitat-Analysis-BreastCancer) | 乳腺癌 DCE-MRI 肿瘤生境分析 + 良恶性分类流水线（TIC 提取 → habitat 聚类 → 影像组学 → Monte Carlo LASSO + 多模型分类） | Private |
| SIAT-NazhangGroup-readme | 本仓库：组织介绍与 README 规范 | Private |

### Hugging Face 仓库

**模型权重**：

| 仓库 | 内容 | 大小 |
|------|------|------|
| [SIAT-NazhangGroup/BA-T1-wall-lumen-seg](https://huggingface.co/SIAT-NazhangGroup/BA-T1-wall-lumen-seg) | `valid_bestPlaqueSegnet_cbam20250207.pth`（CBAM-PlaqueSegNet 权重） | ~36 MB |

**患者/数据集（私有，需授权）**：

| 仓库 | 内容 | 可见性 |
|------|------|--------|
| [SIAT-NazhangGroup/Tumor-Habitat-Analysis-BreastCancer](https://huggingface.co/datasets/SIAT-NazhangGroup/Tumor-Habitat-Analysis-BreastCancer) | 乳腺癌 habitat 分析的病例清单、影像组学特征表、特征选择矩阵等 | Private |

> 新增仓库时请同步更新本表。

---

## README 编写规范

本组织下所有仓库的 README 应遵循以下规范，保证可读性、可复现性与隐私安全。

### 必含章节

每个仓库 README **至少**包含以下章节（顺序可调整，但需齐全）：

1. **项目标题 + 一句话简介** —— 做什么、用于什么
2. **目录** —— 章节导航
3. **模型/工具介绍** —— 目标、适用模态、方法概要
4. **仓库结构** —— 文件树 + 每个文件的作用
5. **环境依赖** —— Python 版本、关键库、安装命令
6. **数据格式** —— 见下方[输入格式约定](#输入格式约定)与[输出格式约定](#输出格式约定)
7. **使用流程** —— 命令行示例（每个脚本的主参数都要列出）
8. **输出说明** —— 输出目录结构 + 标签值含义表
9. **模型权重 / 患者数据**（如有）—— 见[模型权重托管约定](#模型权重托管约定)
10. **注意事项** —— 隐私、硬编码路径、GPU/CPU、模态匹配等
11. **引用 / Citation** —— 相关论文 BibTeX（待发表可写 "待补充"）
12. **许可证** —— 数据使用与代码分发许可

### 输入格式约定

README 中**输入格式**章节应明确以下信息（用表格更清晰）：

| 项目 | 示例 | 说明 |
|------|------|------|
| 图像来源 | DICOM 序列 / mhd+nii.gz | 输入影像的原始格式 |
| 模态 | T1 / PD / T2 / DCE / VWI | 明确支持哪些模态 |
| 图像类型 | 沿血管中心线正交重建的逐层切面 / 多期相 DCE 体数据 | 是否有特殊重建或时序 |
| 体素间距 | 平面 0.1 × 0.1 mm，层间距 0.5 mm | 重采样目标（如不重采样注明"保留原始 spacing"） |
| 病例 ID 约定 | `patient_name` + `label_name`（病灶名） | 命名规范 |

并给出**目录结构示例**：

```
data_root/
└── <patient_id>/
    ├── <modality>/   # DICOM 序列或派生 nii
    └── *.nii.gz      # 可选人工标注 / mask
```

### 输出格式约定

README 中**输出格式**章节应明确：

- 输出目录结构（树形图）
- 每个输出文件的格式与含义
- **标签值表**（见[标签值约定](#标签值约定)）
- 几何信息（spacing / origin / direction 是否保留、是否重采样回原始 DICOM 几何）

### 模型权重托管约定

**所有训练好的模型权重一律托管在 [Hugging Face](https://huggingface.co/SIAT-NazhangGroup)，不放入 GitHub 仓库**，理由：

1. GitHub 单文件硬限制 100 MB，超限需 Git LFS（免费额度有限）
2. HF 提供 CDN 加速下载、版本管理、下载统计
3. 便于他人用 `hf download` / `hf_hub_download` 程序化获取

**患者相关数据**（含 ID 的清单、影像组学特征表等）托管在 **Hugging Face 私有数据集仓库**（`repo_type=dataset`，Private），同样不放入 GitHub。README 的"患者数据与模型权重"章节应包含：

- 权重 / 数据文件名、大小、保存方式
- HF 仓库链接（区分 `model` 与 `dataset` 两种 repo_type）
- **三种下载方式**（hf CLI / huggingface_hub Python / 浏览器直接下载）
- 加载方式（如需 `weights_only=False` 或特定 import）

模板：

```markdown
## 患者数据与模型权重

### 模型权重（如有）
- 文件名：`xxx.pth`
- 大小：约 XX MB
- 保存方式：`torch.save(model, PATH)`（整模型）
- 加载方式：`torch.load(PATH, map_location=..., weights_only=False)`
- **下载地址**：https://huggingface.co/SIAT-NazhangGroup/<repo-name>

### 患者数据
- **下载地址**：https://huggingface.co/datasets/SIAT-NazhangGroup/<repo-name>（Private，需授权）

### 下载方式

​```bash
# 模型权重：hf CLI（推荐）
hf download SIAT-NazhangGroup/<repo-name> <filename>.pth --local-dir ./weights

# 患者数据：huggingface_hub Python
from huggingface_hub import snapshot_download
path = snapshot_download(repo_id="SIAT-NazhangGroup/<repo-name>",
                         repo_type="dataset", local_dir="./data")

# 浏览器直接下载
# 模型：https://huggingface.co/SIAT-NazhangGroup/<repo-name>/blob/main/<filename>.pth
# 数据：https://huggingface.co/datasets/SIAT-NazhangGroup/<repo-name>
​```
```

### 路径与隐私约定

**所有代码与 README 中禁止硬编码本地绝对路径**（如 `/home/tzl/...`、`E:/xxx/...`、`D:\experiments\...`、含本地用户名 / 队列名的目录），理由：

1. 泄露本地用户名、目录结构与队列信息
2. 他人无法直接运行

**推荐做法**（参考 `plaque-morph-radio`、`Tumor-Habitat-Analysis-BreastCancer`）：

- Notebook / 脚本中用占位符（如 `PROJECT_ROOT`、`<PROJECT_ROOT>`），README 给出占位符 → 实际路径的映射表，说明运行前全局替换
- 命令行脚本用 `argparse` 参数 + 合理的 `default`（default 可以是相对路径或占位符）
- README 命令示例一律用 `/path/to/...` 或占位符形式

**患者数据隐私**：

- 仓库 `.gitignore` 应排除 `*.nii.gz`、`*.nii`、`*.dcm`、`*.mhd`、`*.raw`、`*.pth`、`*.zip`、以及含患者信息的 `*.csv` / `*.xlsx` / `*.docx` 等数据表
- 提交前自查，确保不含任何患者可识别信息
- 若历史中误提交过患者数据，须用 `git filter-repo` 彻底清除并 `force push`，仅 `git rm` 不够

### 标签值约定

各仓库按自身结构定义标签值表，README 中务必用表格说明。下面给出本组织现有仓库的标签约定，新增结构时在各仓库 README 中扩展并同步更新本表。

**分割类（颅内斑块，`BA-T1-wall-lumen-seg` 等）**：

| 体素值 | 含义 | 英文 |
|:---:|:---|:---|
| 0 | 背景 | background |
| 1 | 管腔 | lumen |
| 2 | 管壁 | wall |

**生境分析类（乳腺癌，`Tumor-Habitat-Analysis-BreastCancer`）**：

habitat 子区域标签：

| 体素值 | 含义 |
|:---:|:---|
| 0 | 背景（mask 外） |
| 1 | habitat 1（特征前缀 `H1`） |
| 2 | habitat 2（特征前缀 `H2`） |
| 3 | habitat 3（特征前缀 `H3`） |

良恶性标签（`grade` 列）：

| grade | 含义 |
|:---:|:---|
| 0 | Benign |
| 1 | Malignant |

> 若某仓库引入新结构（如斑块内核、出血、新 habitat 等），需在本表基础上扩展并在该仓库 README 中明确说明，同时更新本规范。

---

## 许可证与引用

### 许可证

本组织各仓库的代码默认采用 **MIT License**（除非仓库内另有声明）。模型权重的使用须遵循对应 HF 仓库的 license 说明。

**患者数据**不对外发布，如需用于研究合作请联系课题组获取数据使用与代码分发许可。

### 引用

如本组织仓库对你的研究有帮助，请引用相关论文（各仓库 README 末尾的 "引用 / Citation" 章节会给出具体 BibTeX）。

### 联系

- 课题组：中科院深圳先进技术研究院（SIAT）医学影像组学与影像分析课题组（Na Zhang 课题组）
- GitHub 组织：[SIAT-NazhangGroup](https://github.com/SIAT-NazhangGroup)
- Hugging Face 组织：[SIAT-NazhangGroup](https://huggingface.co/SIAT-NazhangGroup)
