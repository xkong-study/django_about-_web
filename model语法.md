# 常用字段类型：
1. CharField：用于存储短文本字符串，需要指定max_length参数来定义最大长度。
```bash
name = models.CharField(max_length=100)
```
2. IntegerField：用于存储整数。
```bash
age = models.IntegerField()
```
3. FloatField：用于存储浮点数。
```bash
price = models.FloatField()
```
4. DecimalField：用于存储十进制数，需要指定max_digits和decimal_places参数来定义位数。
```bash
price = models.DecimalField(max_digits=10, decimal_places=2)
```
5. DateField：用于存储日期。
```bash
birthdate = models.DateField()
```
6. TimeField：用于存储时间。
```bash
meeting_time = models.TimeField()
```
7. DateTimeField：用于存储日期和时间。
```bash
created_at = models.DateTimeField()
```
8. BooleanField：用于存储布尔值。
```bash
is_published = models.BooleanField()
```
9. EmailField：用于存储电子邮件地址。
```bash
email = models.EmailField()
```

# 模型之间的关系字段类型：
1. ForeignKey：用于创建一对多的关系，一个模型可以与另一个模型关联。
```bash
class Author(models.Model):
    name = models.CharField(max_length=100)

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.ForeignKey(Author, on_delete=models.CASCADE)
```
2. ManyToManyField：用于创建多对多的关系，多个模型可以相互关联。
```bash
class Student(models.Model):
    name = models.CharField(max_length=100)

class Course(models.Model):
    title = models.CharField(max_length=100)
    students = models.ManyToManyField(Student)
```
3. OneToOneField：用于创建一对一的关系，一个模型与另一个模型的一个实例相关联。
```bash
class Person(models.Model):
    name = models.CharField(max_length=100)

class Passport(models.Model):
    passport_number = models.CharField(max_length=20)
    person = models.OneToOneField(Person, on_delete=models.CASCADE)
```
