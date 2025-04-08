# 🎓 CourseMasterX  
Fast and efficient solution for university course scheduling to make scheduling easier!  

---
Suitable for scheduling classes by class

[📄 中文](README.md)  
## ⚙️ **System Requirements**  
Ensure the following requirements are met:  
- **Operating System**: 🖥️ Windows  
- **Graphics Card**: 🎮 NVIDIA GPU (tested on RTX 4070 ✅)  

---

## 📥 **Software Download**  

1. **Download and Extract the Program**  

   📦 Download the compressed package and extract it. If the operating system warns about a security threat, please select **Allow to Run**. ⚠️ **Note**: If not allowed, the system may automatically delete the program files.  

2. **File Description**:

   - **`CourseMasterX.exe`**: 🚀 The main program file. Double-click to execute the scheduling task.  
   - **`really_data_csv` folder**: 📂 Contains sample files for scheduling, provided for testing and reference.  

---

## **Program Operation**

1. **Start the Program**  
   Double-click `CourseMasterX.exe` to run with default settings and check if the program starts successfully.

2. **Set Search Range**  
   After starting, the program will prompt you to input a search range.  
   - **Recommended value**: `9` (The larger the number, the wider the search range the program will attempt).

<img src="console1.PNG" alt="Program Running Screenshot" width="650">


3. **Execution Results**  
   After execution, check whether the following result files are generated:
   - `result_class_0.csv`
   - `result_room_0.csv`
   - `result_teacher_0.csv`
   - `result_unit_0.csv`

   If additional files are generated, don't worry; this indicates that the program has created multiple scheduling solutions.

<img src="result1.PNG" alt="Result File Screenshot" width="400">

---

## **Configuration File Description**

After successfully performing basic operations, learn how to modify configuration files to meet specific requirements.

### **Configuration File Location**
All configuration files are located in the `really_data_csv` folder. All files used by the program are in **CSV format** and can be opened and edited using **Office Excel**, **WPS Excel**, or directly with a text editor.

---

### **Configuration File Overview**
| File Name      | Description      | Function                   |    
|----------------|------------------|----------------------------|
| `class.csv`    | Class Information| Contains details such as class size. |    
| `room.csv`     | Room Information | Includes room types and capacities.  |   
| `cut.csv`      | Course Splitting | Defines how courses are split.       |    
| `unit.csv`     | Course Plan      | Contains the teaching plan to be scheduled. |      

---

### **class.csv**
| Field Name | Description         | Type   |
|------------|---------------------|--------|
| id         | Class ID            | Integer|
| size       | Class size          | Integer|

---

### **room.csv**
| Field Name | Description         | Type   |
|------------|---------------------|--------|
| id         | Room ID             | Integer|
| type       | Room type           | Integer|
| size       | Capacity            | Integer|
| Other fields | Not used           | Default value is 0 (same below).|

---

### **cut.csv**
| Field Name | Description         | Type   |
|------------|---------------------|--------|
| id         | Split ID            | Integer|
| data       | Splitting method, e.g., `2 2` or `4 4 4`. | Multiple integers separated by spaces.|

---

### **unit.csv**
| Field Name   | Description                                                   | Type       |
|--------------|---------------------------------------------------------------|------------|
| class_id     | Class ID(s), can be multiple, separated by spaces.            | Integer    |
| teacher_id   | Teacher ID(s), can be multiple, separated by spaces.          | Integer    |
| course       | Course ID                                                     | Integer    |
| room_type    | Required room type, corresponds to the `type` field in `room.csv`. | Integer    |
| week_num     | Not used                                                      | -          |
| cut          | Weekly splitting method, corresponds to the split ID in `cut.csv`. | Integer    |
| merge        | Not used                                                      | -          |
| time_type    | Name of the time configuration file being used.               | String     |
| vacation     | Not used                                                      | -          |
| week_start   | Not used                                                      | -          |
| week_end     | Not used                                                      | -          |

---

### **time Folder**

The `time` folder contains two time configuration files: `1.csv` and `2.csv`, which are used to define available time slots for classes. For example, in `1.csv`:

<img src="1csv.PNG" alt="Time Configuration File Screenshot" width="500">

- The table contains 7 columns, corresponding to the 7 days of the week, with 15 time slots per day.
  - **Slots marked with `1`**: Unavailable.  
  - **Slots marked with `0`**: Available.  
- Example:
  - On weekdays (Monday to Friday), the "morning" has 5 time slots marked as `0`, and the "afternoon" also has 5 time slots marked as `0`. These time slots are available for scheduling classes.

---

### **Special Case Explanation**

#### Example Question:
**If a course requires 6 consecutive lessons, can it be scheduled according to the current settings in `1.csv`?**

**Answer: No**, because no single time slot can accommodate 6 consecutive lessons.  
It is recommended to split the course into two sessions, such as "3 3" or "2 4", ensuring that each session occupies no more than 5 time slots.

---

## **Result File Description**

Result files with the same trailing number belong to the same scheduling solution. For example:  
`result_room_0.csv`, `result_teacher_0.csv`, `result_unit_0.csv`, and `result_class_0.csv` belong to the same solution set.

---

### **result_room_0.csv**
| Field Name | Description                                                      |
|------------|------------------------------------------------------------------|
| room       | The ID of the room assigned to the course plan.                  |
| course     | Course ID                                                       |
| day        | A group of 3 numbers, representing the day of the week, start period, and end period (field name may change). |
| start      | Not used                                                        |
| end        | Not used                                                        |
| Note       | Each row corresponds to the row position in `unit.csv`.          |

---

### **result_teacher_0.csv**
| Field Name | Description                                                      |
|------------|------------------------------------------------------------------|
| teachers   | Teacher ID                                                      |
| course     | Course ID                                                       |
| day        | A group of 3 numbers, representing the day of the week, start period, and end period (field name may change). |

---

### **result_unit_0.csv**
| Field Name | Description                                                      |
|------------|------------------------------------------------------------------|
| day        | Same as above                                                   |
| Note       | Each row corresponds to the row position in `unit.csv`.          |

---

### **result_class_0.csv**
| Field Name | Description                                                      |
|------------|------------------------------------------------------------------|
| classes    | Class ID                                                        |
| course     | Course ID                                                       |
| day        | Same as above                                                   |