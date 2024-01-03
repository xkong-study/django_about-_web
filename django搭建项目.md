# Django Blog 应用

这是一个使用Django创建的简单博客应用，用于展示帖子和评论。

## 步骤 1: 创建 Django 项目

- 使用Django命令行工具创建一个新的Django项目：

  ```bash
  django-admin startproject myproject
  ```
进入项目目录：

  ```bash
  cd myproject
  ```
步骤 2: 创建 Django 应用
使用Django命令行工具创建一个新的Django应用：

  ```bash
  python manage.py startapp myapp
```
步骤 3: 定义模型
在 myapp/models.py 中定义模型。例如，下面是一个帖子（Post）和评论（Comment）的模型示例：

  ```bash
  from django.db import models
  from django.utils import timezone

class Post(models.Model):
    title = models.CharField(max_length=200)
    author = models.ForeignKey('auth.User', on_delete=models.CASCADE)
    body = models.TextField()
    created_date = models.DateTimeField(default=timezone.now)
    published_date = models.DateTimeField(blank=True, null=True)

    def publish(self):
        self.published_date = timezone.now()
        self.save()

    def __str__(self):
        return self.title

class Comment(models.Model):
    post = models.ForeignKey('Post', related_name='comments', on_delete=models.CASCADE)
    author = models.CharField(max_length=100)
    text = models.TextField()
    created_date = models.DateTimeField(default=timezone.now)
    approved_comment = models.BooleanField(default=False)

    def approve(self):
        self.approved_comment = True
        self.save()

    def __str__(self):
        return self.text
```

步骤 4: 迁移数据库
创建模型迁移文件：
 
  ```bash
  python manage.py makemigrations
  ```
应用迁移并创建数据库表：

  ```bash
  python manage.py migrate
  ```
步骤 5: 创建视图
在 myapp/views.py 中创建视图函数。例如，以下是用于显示帖子列表和单个帖子详细信息的视图函数示例：

  ```bash
  from django.shortcuts import render, get_object_or_404
  from .models import Post

def post_list(request):
    posts = Post.objects.all()
    return render(request, 'myapp/post_list.html', {'posts': posts})

def post_detail(request, pk):
    post = get_object_or_404(Post, pk=pk)
    return render(request, 'myapp/post_detail.html', {'post': post})
```

步骤 6: 创建 URL 映射
在 myapp/urls.py 中创建 URL 映射以连接视图和网址。例如：

  ```bash
  from django.urls import path
  from . import views

urlpatterns = [
    path('', views.post_list, name='post_list'),  # 帖子列表
    path('post/<int:pk>/', views.post_detail, name='post_detail'),  # 帖子详细信息
]
```

这些步骤总结了如何创建一个简单的博客应用，并在其中显示数据库中的数据。根据您的项目需求，您可以进一步定制视图、模板和样式。

安装和运行
为了安装所需的依赖项，请运行以下命令：

  ```bash
  pip install -r requirements.txt
  ```
然后，运行开发服务器：

  ```bash
  python manage.py runserver
  ```

应用将在 http://127.0.0.1:8000/ 上运行。

