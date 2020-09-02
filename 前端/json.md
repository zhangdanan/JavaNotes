# JSON

### 什么是JSON

JSON是一种与开发语言无关的、轻量级的数据格式。全称JavaScriptObject Notation

### JSON数据表示

数据结构

对象Object

使用花括号{}包含的键值对结构，Key必须是string类型，也就是必须用双引号括住，value可以是任何基本类型或数据结构

Array

使用中括号[]来起始，并用逗号，来分隔元素

基本类型

string、number、true、false、null

### 生成json

#### put

```
public static void PutJSONObject() throws JSONException {
        JSONObject zhangsan=new JSONObject();
        Object null1=null;
        zhangsan.put("age",22);
        zhangsan.put("car",false);
        zhangsan.put("name","张亚楠");
        zhangsan.put("birthday","2020-04-30");
        zhangsan.put("like",new String[]{"听歌","运动"});
        zhangsan.put("hotel",null1);
        System.out.println(zhangsan.toString());
    }
```



#### Map

```
public static void CreateJsonByMap(){
        Map<String,Object> zhangsan=new HashMap <String, Object>();
        Object null1=null;
        zhangsan.put("age",22);
        zhangsan.put("car",false);
        zhangsan.put("name","张亚楠");
        zhangsan.put("birthday","2020-04-30");
        zhangsan.put("like",new String[]{"听歌","运动"});
        zhangsan.put("hotel",null1);
        System.out.println(new JSONObject(zhangsan));
    }
```



#### Bean

```
public class User {
    public String name;
    public String birthday;
    public Integer age;
    public Boolean car;
    ....getter/setter
    }
    
    
public static void CreateJsonByBean(){
        User user=new User();
        user.setAge(22);
        user.setBirthday("2020-04-30");
        user.setCar(false);
        user.setName("zhangdanan");
        System.out.println(new JSONObject(user));
    }
```

### 读取Json

有很多json解析工具