4、在score表中查询成绩大于80的记录；	

```select grade from score where grade>=80;```

5、查询“10中文”和“10英语”班级所有的学生信息(残缺)

```select * from student where student.class_id in (select classes.class_id from classes where class_name='10中文' or class_name='10英语')```

6、查询课号“maths”成绩大于60并且小于90的	学生记录(残缺)

```  select * from score where grade>=70 and grade<=90 and course_id in(select course_id from course where course_name='math')  ```

7、在student表中查询“张”姓的学生记录

```select * from student where student_name like '张%'```

8、在student表中查询带有“三”字的学生记录

```select * from student where student_name like '%三%'```

9、在student表中查询第二个字为“三”的学生记录

```select * from student where student_name like '%_三_%'```

10、将score表中按照成绩从高到低的顺序提取数据

```select grade from score order by grade DESC```

11、统计score表中course_id等于1的总成绩（使用sum函数计算字段的累加和）

```select sum(garde) from score where course_id=1;```

12、统计student表中的学生人数（使用count函数统计记录行数）

```select count(student_id) from student```

13、在score表中查询每个学生的平均成绩

```select student_id,AVG(grade) from score group by student_id ``` 

14、在score表中查询学生平均成绩高于70分的学生记录

```select student_id,AVG(grade) as avg from score GROUP BY student_id Having avg(grade)>=70;```








；





