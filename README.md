# 保全档案的托管密钥授权和退役

托管端以密钥版本标识实际使用范围，归档端只掌握包装引用。涉及打开及退役的回执均为合成记录，不存放密钥或正文。

资料中的对象、身份及记录均为虚构。各来源使用 UTF-8 JSON Lines，一行是一个原始对象。`seq` 是全局到达序号，按演练资料的可知顺序排列。事实发生时刻、确认时刻与适用时段以同行中的独立字段为准，用相对演练起点的整数分钟表达。JSON `null` 保留来源的缺省或未确认值。除非来源明确使用相同标识，编号只在所属来源和实体域内有意义。

## 来源

- `sources/archives.jsonl`　卷宗盘点中 copy 是存放处的副本键，wrapper 是包装引用，available 表示该次盘点是否可访问。
- `sources/decisions.jsonl`　独立的保全或到期决定。from/until 是保全区间。dispose 表示可启动核查。
- `sources/operators.jsonl`　由办案机构登记的 actor 当前具有的动作和用途。scope 可为卷宗号或托管的管理权限标识。
- `sources/wrappers.jsonl`　托管端引用与实际 generation 的映射。同代可包装多份归档，retired 指版本已经退役。
- `sources/receipts.jsonl`　托管动作的外部回执。object 为副本或代次；received 与 completed 对执行作不同承诺。

## 查看记录

使用 Python 3.11.2 标准库，无需安装第三方包。以下命令列出可读取的来源、查看单个来源记录并检查资料格式。读取命令按输入顺序输出 JSON，可通过 `--through` 限制已到达的记录。

```bash
python3 source_records.py
python3 source_records.py archives
python3 -m unittest discover -v
```
