# LexLoom

LexLoom 是一个精简的 Python 密码字典生成器，用于在授权的安全测试、密码强度评估或个人账户自查场景中，根据目标相关信息生成候选密码字典。

> 请仅在你拥有明确授权的系统、账户或测试环境中使用本工具。不要将生成的字典用于未授权访问、撞库、爆破或其他违法行为。

## 功能特点

- 基于姓名、昵称、公司、宠物名、关键词等信息生成组合
- 支持生日、伴侣生日、孩子生日等日期片段
- 支持季节、月份、星期与年份组合，例如 `Winter2023!`
- 支持指定单个年份或年份范围，例如 `2023`、`2020-2025`
- 内置常见弱密码与键盘行走模式，例如 `qwerty`、`1qaz2wsx`
- 可选 Leet speak 变体，例如 `a -> @`、`e -> 3`
- 支持最小/最大长度过滤
- 无第三方依赖，直接使用 Python 标准库运行

## 环境要求

- Python 3.8 或更高版本
## 快速开始

查看帮助：

```powershell
python .\lexloom.py --help
```

进入交互式模式：

```powershell
python .\lexloom.py -i
```

根据用户名、公司和季节生成字典：

```powershell
python .\lexloom.py -n john+doe -c apple --season -o output.txt
```

生成月份与指定年份范围组合：

```powershell
python .\lexloom.py --month --year 2023-2024 -o months.txt
```

限制输出密码长度：

```powershell
python .\lexloom.py -n admin --min 8 --max 16 -o admin_words.txt
```

## 常用参数

| 参数 | 说明 |
| --- | --- |
| `-i, --interactive` | 进入交互式模式 |
| `-n, --name` | 姓名或用户名，支持 `john+doe` 形式 |
| `--surname` | 姓氏 |
| `--nickname` | 昵称 |
| `-b, --birthday` | 生日，格式为 `YYYYMMDD` |
| `--partner-name` | 伴侣姓名 |
| `--partner-birthday` | 伴侣生日 |
| `--child-name` | 孩子姓名 |
| `--child-birthday` | 孩子生日 |
| `-p, --pet` | 宠物名 |
| `-c, --company` | 公司或单位名 |
| `-k, --keywords` | 关键词，多个值用英文逗号分隔 |
| `--season` | 启用季节组合 |
| `--month` | 启用月份组合 |
| `--weekday` | 启用星期组合 |
| `--year` | 指定年份，支持 `2023` 或 `2020-2025` |
| `--leet` | 启用 Leet speak 变体 |
| `--no-special` | 禁用特殊字符尾部 |
| `--no-keyboard` | 禁用键盘密码模式 |
| `--no-common` | 禁用常见弱密码 |
| `--word-combo` | 启用词语两两组合 |
| `--min` | 最小长度，默认 `6` |
| `--max` | 最大长度，默认 `24` |
| `-o, --output` | 输出文件名，默认 `lexloom_passwords.txt` |
| `-q, --quiet` | 静默模式 |

## 年份规则

如果没有通过 `--year` 指定年份，LexLoom 会默认使用当前年份附近的年份片段：当前年份前 3 年到后 1 年，并同时加入完整年份和两位年份。

示例：

```powershell
python .\lexloom.py --season
```

如果当前年份是 `2026`，则会使用类似 `2023`、`23`、`2024`、`24`、`2025`、`25`、`2026`、`26`、`2027`、`27` 的年份片段。

## 输出说明

生成结果会写入输出文件，每行一个候选密码。默认输出文件为：

```text
lexloom_passwords.txt
```

输出内容会先去重，再按长度和字典序排序。

## 示例

生成目标信息、生日、关键词、季节和 Leet 变体：

```powershell
python .\lexloom.py -n john+doe -b 19900315 -k github,dev --season --leet -o john_dict.txt
```

禁用常见弱密码和键盘模式，只保留目标相关组合：

```powershell
python .\lexloom.py -n alice -c example --year 2024 --no-common --no-keyboard -o focused.txt
```

生成星期组合并关闭特殊字符尾部：

```powershell
python .\lexloom.py --weekday --year 2023 --no-special -o weekday.txt
```

## 项目结构

```text
LexLoom/
├── lexloom.py   # 主程序
└── README.md    # 项目说明
```

## 许可证

当前仓库未声明许可证。使用、分发或修改前，请先根据你的项目需求补充合适的开源许可证。
