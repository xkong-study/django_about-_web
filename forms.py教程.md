## 1.定义表单类：

在Django中，您可以创建一个继承自 forms.Form 的表单类，然后在类中定义表单的字段和验证规则。例如：

```bash
from django import forms

class MyForm(forms.Form):
    name = forms.CharField(max_length=100)
    email = forms.EmailField()
    age = forms.IntegerField()

```

## 2.在视图中使用表单:

```bash
from django.shortcuts import render, redirect

def create_user(request):
    if request.method == 'POST':
        form = MyForm(request.POST)
        if form.is_valid():
            # 处理表单数据，保存到数据库等
            name = form.cleaned_data['name']
            email = form.cleaned_data['email']
            age = form.cleaned_data['age']
            # 执行操作，例如保存到数据库
            # 重定向到成功页面或其他操作
            return redirect('success_page')
    else:
        form = MyForm()
    return render(request, 'create_user.html', {'form': form})
```

## 3.在模板中渲染表单

```bash
<form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">提交</button>
</form>

```
