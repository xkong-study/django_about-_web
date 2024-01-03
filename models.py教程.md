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

除了 CASCADE，还有其他选项可以作为 on_delete 的值，包括：

models.PROTECT：防止删除关联对象，会引发 ProtectedError 异常。

models.SET_NULL：将关联字段设置为 NULL（仅适用于可以为 NULL 的字段）。

models.SET_DEFAULT：将关联字段设置为默认值。

models.SET()：将关联字段设置为指定的值。

models.DO_NOTHING：不执行任何操作，留待开发者手动处理。

如图所示：  
[![2024-01-03-11-39-53](https://i.ibb.co/474vHqt/2024-01-03-11-39-53.png)](https://ibb.co/mGhZ3jT)

# Django的数据库查询语法
1. get()：获取满足指定条件的单个对象。
```bash
post = Post.objects.get(id=1)
```
2. filter()：根据指定条件筛选多个对象。
```bash
posts = Post.objects.filter(published_date__isnull=False)
```
3. exclude()：排除满足指定条件的对象。
```bash
posts = Post.objects.exclude(author__username='admin')
```
4. all()：获取模型的所有对象。
```bash
posts = Post.objects.all()
```
5. count()：计算满足条件的对象数量。
```bash
count = Post.objects.filter(published_date__isnull=False).count()
```
6. order_by()：按指定字段对对象进行排序。
```bash
posts = Post.objects.order_by('-published_date')
```
7. distinct()：获取去重后的对象集合。
```bash
authors = Post.objects.values_list('author', flat=True).distinct()
```
8. annotate()：用于添加聚合计算结果到查询中。
```bash
from django.db.models import Count
authors_with_count = Author.objects.annotate(num_posts=Count('post'))
```
9. values() 和 values_list()：用于选择特定字段的值。
```bash
titles = Post.objects.values_list('title', flat=True)
```
10. 链式查询：可以将多个查询方法链接在一起，以构建更复杂的查询。
```bash
recent_posts = Post.objects.filter(published_date__isnull=False).order_by('-published_date')[:5]
```
11. 复杂查询：Django支持使用Q对象和复杂查询表达式进行复杂的查询操作。
```bash
from django.db.models import Q
posts = Post.objects.filter(Q(title__icontains='Django') | Q(body__icontains='Django'))
```
12. 聚合函数：Django支持各种聚合函数，如Sum、Avg、Min和Max等，用于计算统计信息。
```bash
from django.db.models import Sum
total_likes = Post.objects.aggregate(total_likes=Sum('likes'))
```
