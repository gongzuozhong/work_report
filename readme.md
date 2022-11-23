- 新建项目

  

- 配置admin

- 数据库表结构设计

  ```python
  class Employee(models.Model):
      email = models.EmailField(verbose_name="邮箱", unique=True)
      password = models.CharField(verbose_name="密码", max_length=255)
      true_name = models.CharField(verbose_name="姓名", max_length=255)
      head_img = models.ImageField(verbose_name="头像", default=None)
      department = OneToOneField(verbose_name="部门", to="Department", on_delete=models.CASCADE)
      reg_date = DateField(verbose_name="加入日期", auto_now_add=True)
      last_update = DateField(verbose_name="加入日期", auto_now_add=True, auto_now=True)
      last_login = DateField(verbose_name="加入日期")
  
      class Meta:
          verbose_name = '员工'
  
  
  class Department(models.Model):
      title = models.CharField(verbose_name="部门名称", max_length=255)
      parent = models.ForeignKey(to='self', verbose_name="上级部门",on_delete=models.CASCADE())
      add_date = DateField(verbose_name="添加日期", auto_now_add=True)
  
      class Meta:
          verbose_name = '部门'
  
  
  class Notice(models.Model):
      title = models.CharField(verbose_name="通知标题", max_length=255)
      content = models.TextField(verbose_name="通知内容")
      is_top = models.BooleanField(verbose_name="置顶", default=False)
      add_date = DateField(verbose_name="添加日期", auto_now_add=True)
      last_update = DateField(verbose_name="修改日期", auto_now_add=True, auto_now=True)
  
      class Meta:
          verbose_name = '通知'
  
  
  class ReportPlan(models.Model):
      report = models.CharField(verbose_name="工作总结", max_length=255)
      plan = models.TextField(verbose_name="工作计划")
      is_draft = models.BooleanField(verbose_name="草稿", default=True)
      employee = models.ForeignKey(to="Employee", verbose_name="员工", on_delete=models.CASCADE())
      add_date = DateField(verbose_name="添加日期", auto_now_add=True)
      send_date = DateField(verbose_name="发送日期", auto_now_add=True)
  
      class Meta:
          verbose_name = '报告'
  
  
  class Attachment(models.Model):
      file_url = models.FileField(verbose_name="附件地址")
      report_plan = models.ForeignKey(to="ReportPlan", verbose_name="所属报告")
  
      class Meta:
          verbose_name = '附件'
  ```

- 后台登录地址以及超管账号密码

- 其他注意事项

