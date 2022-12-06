python manage.py shell
Editor.objects.order_by('first_name')
Editor.objects.order_by('-first_name')
Editor.objects.all()[:]

django-admin startproject 
python manage.py startapp 

>>> Editor.objects.filter(id = 2).update(first_name ='Kim')
>>> Editor.objects.filter(id = 2).delete()
pip install pillow

### models
    from django.contrib.auth.models import AbstractBaseUser,BaseUserManager
    import datetime as dt
    from django.contrib import messages
    from django.contrib.auth import login, logout, authenticate
    from django.contrib.auth.hashers import make_passwor
    from cloudinary.models import CloudinaryField
    user=models.ForeignKey("Users",on_delete=models.CASCADE)

    class MyAccountManager(BaseUserManager):
        def create_user(self, email, username, password=None):
            if not email:
                raise ValueError(" User must have an email address")
            if not username:
                raise ValueError(" User must have an username!")    

            user = self.model(
                email=self.normalize_email(email),
                username=username,
            )
            user.set_password(password)
            user.save(using=self._db)
            return user

        def create_superuser(self, email, username, password):
            user = self.create_user(
                email=self.normalize_email(email),
                password = password,
                username=username,
            )
            user.email = email
            user.is_admin = True 
            user.is_staff = True 
            user.is_superuser = True 
            user.save(using=self._db)
            return user


    class Users(AbstractBaseUser):
        username = models.CharField( max_length=20, unique=True)  
        email = models.CharField( max_length=50, unique=True)    
        date_joined = models.DateTimeField(verbose_name='date joined', auto_now_add=True)
        last_login = models.DateTimeField(default=dt.datetime.now)
        is_admin = models.BooleanField(default=False)
        is_active = models.BooleanField(default=True)
        is_staff = models.BooleanField(default=False)
        is_superuser = models.BooleanField(default=False)
        password = models.CharField( max_length=100)

        USERNAME_FIELD = 'username'
        REQUIRED_FIELDS = [ 'email']

        objects=MyAccountManager()

        def _str_(self):
            return self.email

        def has_perm(self, perm, obj=None):
            return self.is_admin

        def has_module_perms(self, app_label):
            return True
### Authenticating
 user= authenticate(email=email, password=password)
### Email configurations
    EMAIL_USE_SSL = True
    EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
    EMAIL_HOST = 'smtp.gmail.com'
    EMAIL_PORT = 465
    EMAIL_USE_TLS = False
    EMAIL_HOST_USER = os.environ.get('EMAIL_HOST_USER')
    EMAIL_HOST_PASSWORD = os.environ.get('EMAIL_HOST_PASSWORD')


#### DATABASE
if os.environ.get('MODE')=="dev":
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql',
            'NAME': 'notebook',
            'USER':'postgres',
            'PASSWORD': os.environ['PASSWORD'],
            'HOST':'localhost', 
        }
    }

- production
else:
   DATABASES = {
       'default': dj_database_url.config(
           default=os.environ.get('DATABASE_URL')
       )
   }
   
### Rest api cutom vlidations
https://stackoverflow.com/questions/31278418/django-rest-framework-custom-fields-validation
