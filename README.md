# Excel4J 是基于Excel模板导入导出
---
## 1.对象模型(/src/test/java/moudles/Student.java)  基于ExcelField注解
```
    // 学号
    @ExcelField(title = "学号", order = 1)
    private String id;

    // 姓名
    @ExcelField(title = "姓名", order = 2)
    private String name;

    // 班级
    @ExcelField(title = "班级", order = 3)
    private String classes;

```

## 2.Excel转对象模型(/src/test/java/base/Excel2Moudle.java)
  ### 2-1. Excel对象
  ![excel文件](https://raw.githubusercontent.com/Crab2died/Excel4J/master/src/test/java/resource/image/excel_import.png)
  ### 2-2. 转换函数
  ```
    @Test
    public void excel2Object(){
        String path = "D:\\IdeaSpace\\Excel4J\\src\\test\\java\\resource\\student.xlsx";
        List<Object> students = ExcelUtil.getInstance().readExcel2ObjsByClasspath(path, Student.class);
        for (Object obj : students){
            Student stu = (Student) obj;
            System.out.println(stu.getName() + " -- " + stu.getClasses());
        }

        students  = ExcelUtil.getInstance().readExcel2ObjsByClasspath(path, Student.class, 0, 2);
        for (Object obj : students){
            Student stu = (Student) obj;
            System.out.println(stu.getName() + " -- " + stu.getClasses());
        }
    }
  ```
  
## 3. 对象转Excel表格，基于模板(/src/test/java/base/Moudle2Excel.java)
   ### 3-1. Excel模板
![demo模板](https://raw.githubusercontent.com/Crab2died/Excel4J/master/src/test/java/resource/image/template.png)
   ### 3-2. 导出函数
   ```
    @Test
    public void object2Excel(){
        String tempPath = "D:\\IdeaSpace\\Excel4J\\src\\test\\java\\resource\\template.xlsx";
        List<Student> list = new ArrayList<>();
        list.add(new Student("1010001", "盖伦", "六年级三班"));
        list.add(new Student("1010002", "古尔丹", "一年级三班"));
        list.add(new Student("1010003", "蒙多", "六年级一班"));
        list.add(new Student("1010004", "萝卜特", "三年级二班"));
        Map<String, String> datas = new HashMap<>();
        datas.put("title", "战争学院花名册");
        datas.put("info", "学校统一花名册");
        ExcelUtil.getInstance().exportObj2ExcelByTemplate(datas, tempPath, "D:\\2.xlsx", list, Student.class, false, true);
    }
   ```
   ### 3-3. 导出效果图
![导出效果图](https://raw.githubusercontent.com/Crab2died/Excel4J/master/src/test/java/resource/image/excel_export.png)
   
