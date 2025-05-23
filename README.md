# 🎓 CourseMasterX  
快速、高效地解决高校排课问题，让排课变得更轻松！  
---
适用于按班级排课

[📄 English](README_EN.md)  [📄  عربي  ](README_AR.md)
## ⚙️ **运行要求**  
确保以下环境满足运行需求：  
- **操作系统**：🖥️ Windows  
- **显卡**：🎮 NVIDIA 显卡，可运行cuda程序（已在 RTX 4070、RTX 2060上测试 ✅，其他型号显卡还未测试）  

---

## 📥 **软件下载**  

1. **下载并解压程序**  

   📦 下载压缩包后解压。如果操作系统提示存在安全威胁，请选择 **允许运行**。⚠️如果未允许运行，系统会自动删除程序文件。  

2. **文件说明**：

   - **`CourseMasterX.exe`**：🚀 主程序文件，双击后即可执行排课任务。  
   - **`really_data_csv` 文件夹**：📂 包含待排课的样例文件，供测试和参考。  

---

## **程序运行**

1. **启动程序**  
   双击 `CourseMasterX.exe`，运行默认配置，检查程序是否能够正常启动。

2. **设置搜索范围**  
   程序启动后，会提示你输入搜索范围。  
   - **建议输入值：** `9` （数值越大，程序尝试搜索的范围越广）。

<img src="console1.PNG" alt="程序运行截图" width="650">


3. **运行结果**  
   运行结束后，检查是否生成结果文件，包括：
   - `result_class_0.csv`
   - `result_room_0.csv`
   - `result_teacher_0.csv`
   - `result_unit_0.csv`

   如果生成了更多文件，不必担心，这表示程序生成了多个排课方案。

<img src="result1.PNG" alt="结果文件截图" width="400">

---

## **高校配置文件说明**

成功完成基本操作后，学习如何修改配置文件以满足用户需求。

### **配置文件位置**
所有配置文件都位于 `really_data_csv` 文件夹中。本程序所有涉及的文件均为 **CSV 格式**，可使用 **Office Excel** 或 **WPS Excel** 打开和编辑，也可以用记事本打开直接编辑。

---

### **配置文件一览表**
| 文件名       | 描述         | 功能                       |    
|--------------|--------------|----------------------------|
| `class.csv`  | 班级信息     | 包含班级人数等信息         |    
| `room.csv`   | 教室信息     | 包含教室类型和容量等信息   |   
| `cut.csv`    | 分课信息     | 定义课程分课的具体方式     |    
| `unit.csv`   | 课程计划     | 需要排课的教学计划         |      

---

### **class.csv**
| 字段名 | 描述              | 类型   |
|--------|-------------------|--------|
| id     | 班级id    | 自然数 |
| size   | 班级人数  | 自然数 |

---

### **room.csv**
| 字段名 | 描述                     | 类型   |
|--------|--------------------------|--------|
| id     | 教室id        | 自然数 |
| type   | 教室类型        | 自然数 |
| size   | 容纳人数                | 自然数 |
| 其余字段 | 未使用        | 默认填0，下同      |

---

### **cut.csv**
| 字段名 | 描述                             | 类型   |
|--------|----------------------------------|--------|
| id     | 分课id                        | 自然数 |
| data   | 分课方式，例如 `2 2` 或 `4 4 4`  | 多个空格分隔的自然数 |

---

### **unit.csv**
| 字段名    | 描述                                                              | 类型       |
|-----------|-------------------------------------------------------------------|------------|
| class_id  | 班级id，可多个，用空格分割                               | 自然数     |
| teacher_id| 教师id，可多个，用空格分割                              | 自然数     |
| course    | 课程id                                                 | 自然数     |
| room_type | 所需教室类型，与 `room.csv` 中的 type 字段对应                    | 自然数     |
| week_num  | 未使用                                                           | -          |
| cut       | 每周分课方式，对应 `cut.csv` 中的分课id                           | 自然数     |
| merge     | 未使用                                                           | -          |
| time_type | 使用的时间配置文件名                                              | 字符串     |
| vacation  | 未使用                                                           | -          |
| week_start| 未使用                                                           | -          |
| week_end  | 未使用                                                           | -          |

---

### **time 文件夹**

`time` 文件夹中包含两个时间配置文件：`1.csv` 和 `2.csv`，用于自定义上课的时间段。以 `1.csv` 为例：

| | | | | | | |
|-|-|-|-|-|-|-|
|0|0|0|0|0|1|1|
|0|0|0|0|0|1|1|
|0|0|0|0|0|1|1|
|0|0|0|0|0|1|1|
|0|0|0|0|0|1|1|
|1|1|1|1|1|1|1|
|0|0|0|0|0|1|1|
|0|0|0|0|0|1|1|
|0|0|0|0|0|1|1|
|0|0|0|0|0|1|1|
|0|0|0|0|0|1|1|
|1|1|1|1|1|1|1|
|1|1|1|1|1|1|1|
|1|1|1|1|1|1|1|
|1|1|1|1|1|1|1|

- 表格包含 7 列，分别对应一周的 7 天，每天有 15 个时间段。
  - **被 `1` 标记的时间段**：不可用。
  - **被 `0` 标记的时间段**：可用。
- 例如：
  - 周一到周五的“上午”有 5 个时间段为 `0`，“下午”也有 5 个时间段为 `0`，这些时间段可以安排课程。

---

### **特殊情况说明**

#### 示例问题：
**如果有一门课要求连上 6 节，按照 `1.csv` 的设置，能安排吗？**

**答：不能**，因为没有任何一个时间区间可以容纳连续 6 节课。  
建议将课程拆分为两次授课，例如“3 3”或“2 4”，确保每次占用课时小于等于 5。

---

## **结果文件说明**

每组尾部数字相同的 CSV 文件为同一套排课方案。例如：  
`result_room_0.csv`、`result_teacher_0.csv`、`result_unit_0.csv` 和 `result_class_0.csv` 属于同一结果方案。

---

### **result_room_0.csv**
| 字段名 | 描述                                                                 |
|--------|----------------------------------------------------------------------|
| room   | 一个课程计划被安排的教室id                                           |
| course | 课程id                                                              |
| day    | 3 个数字为 1 组，表示周几、课程起始节次、课程结束节次（字段名可能修改） |
| start  | 未使用                                                              |
| end    | 未使用                                                              |
| 补充说明  | 文件中的每行对应输入的unit.csv中每行的位置。        |
---

### **result_teacher_0.csv**
| 字段名  | 描述                                                                 |
|---------|----------------------------------------------------------------------|
| teachers| 教师id                                                              |
| course  | 课程id                                                              |
| day     | 3 个数字为 1 组，表示周几、课程起始节次、课程结束节次（字段名可能修改） |

---

### **result_unit_0.csv**
| 字段名 | 描述                                                                 |
|--------|----------------------------------------------------------------------|
| day    | 同上                                                                |
| 补充说明  | 文件中的每行对应输入的unit.csv中每行的位置。        |
---

### **result_class_0.csv**
| 字段名 | 描述                                                                 |
|--------|----------------------------------------------------------------------|
| classes| 班级id                                                              |
| course | 课程id                                                              |
| day    | 同上                                                                |

## **中小学排课配置文件说明**
区别于高校，中小学在固定教室排课，需要我们对配置文件做一点修改。

程序默认读取的是really_data_csv文件夹下的内容，所以首先将really_school_data_csv里的文件全部拷贝到really_data_csv中，替换到原来的文件。


### **配置文件一览表**
| 文件名       | 描述         | 功能                       |    
|--------------|--------------|----------------------------|
| `class.csv`  | 班级信息     | 实际的班级人数已经不重要了，只要和room中教室的size大于等于班级人数即可         |    
| `room.csv`   | 教室信息     | 每个教室都改为一个不重复的type类型，保证在unit中分到对应的课程计划  |   
| `cut.csv`    | 分课信息     | 根据实际情况安排     |    
| `unit.csv`   | 课程计划     | 每个班级的id和教室的id需要保持一致         |    
---

我们逐个来解释下really_school_data_csv中的文件。

### **class.csv**
| id | size              |    
|--------|-------------------|
| 0   | 50    | 
| 1  | 50  |
---
表示有两个班级，id为0和1，每个班级的人数为50。

因为不需要对教室进行安排，所以这里的人数可以随便设置。

### **room.csv**
| id | building|floor|name|type|size |
|--------|------|---|------|-----------|--------|
| 0    | 0|     0| 0| 0   | 50 |
| 1    | 0|     0| 0| 0   | 50 |
---
这里提供了两个教室，id为0和1，教室尺寸为50，要大于对应的班级人数。

building、floor、name三个字段未使用，默认0即可。

### **cut.csv**
| id | data                             | 
|--------|----------------------------------|
| 0     | 1 1 1 1 1                        |
| 1   | 1 1 1 1 | 
| 2  | 1 1 1 | 
---
id=0的分课方式，表示一周上5次课，每次上1节。

id=1的分课方式，表示一周上4次课，每次上1节。

每个1之间用空格分割，1改成2也可以，表示每次上2节课。

以此类推。

### **unit.csv**
| class_id | teacher_id | course | room_type | week_num | cut | merge | time_type | vacation | week_start | week_end |
|----------|------------|--------|-----------|----------|-----|-------|-----------|----------|------------|----------|
| 0        | 0          | 0      | 0         | 0        | 0   | 0     | 1.csv     | 0        | 0          | 0        |
| 0        | 1          | 1      | 0         | 0        | 0   | 0     | 1.csv     | 0        | 0          | 0        |
| 0        | 2          | 2      | 0         | 0        | 0   | 0     | 2.csv     | 0        | 0          | 0        |
| 0        | 3          | 3      | 0         | 0        | 0   | 0     | 1.csv     | 0        | 0          | 0        |
| 0        | 4          | 4      | 0         | 0        | 0   | 0     | 2.csv     | 0        | 0          | 0        |
| 1        | 0          | 0      | 1         | 0        | 0   | 0     | 1.csv     | 0        | 0          | 0        |
| 1        | 1          | 1      | 1         | 0        | 0   | 0     | 1.csv     | 0        | 0          | 0        |
| 1        | 2          | 2      | 1         | 0        | 0   | 0     | 2.csv     | 0        | 0          | 0        |
| 1        | 3          | 3      | 1         | 0        | 0   | 0     | 1.csv     | 0        | 0          | 0        |
| 1        | 4          | 4      | 1         | 0        | 0   | 0     | 2.csv     | 0        | 0          | 0        |
---
这里我们假设教室0安排给班级0，教室1安排给班级1。

方法是将class_id为0的行中room_type都设置为0，由于在room.csv中type为0的教室有且只有1个id=0的，所以达到了固定教室的目的。

同理我们将class_id为1中的room_type都设置为1，从而将room.csv中id=1的教室固定分配给1班。（反过来也可以教室0安排给班级1，教室1安排给班级0）

time_type字段我设置了两个文件1.csv和2.csv。

`1.csv`
|   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 | 1 | 1 |
| 0 | 0 | 0 | 0 | 0 | 1 | 1 |
| 0 | 0 | 0 | 0 | 0 | 1 | 1 |
| 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| 1 | 1 | 1 | 1 | 1 | 1 | 1 |
---
`1.csv`的含义是每周7天，有5天上课，对于在unit.csv的time_type字段中选择1.csv的课程计划的课程，只安排在每天的前3节课，也就是`0`的位置。

`2.csv`
|   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|
| 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| 0 | 0 | 0 | 0 | 0 | 1 | 1 |
| 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| 0 | 0 | 0 | 0 | 0 | 1 | 1 |
| 0 | 0 | 0 | 0 | 0 | 1 | 1 |
| 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| 1 | 1 | 1 | 1 | 1 | 1 | 1 |
---
`2.csv`表示只安排在每天的第4、6、7节课，也就是`0`的位置。

其余部分和高校排课的设置一样，可以查看前面的说明。