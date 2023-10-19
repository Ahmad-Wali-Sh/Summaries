# Django Crontab

dead simple crontab powered job scheduling for django (1.8+).

##
install
```
pip install django-crontab

INSTALLED_APPS = (
    'django_crontab',
    ...
)
```

## Function to Run
---
```python
def my_scheduled_job():
  management.call_command('dbbackup')
```

## CRONJOBS
---
```python
CRONJOBS = [
    ('*/5 * * * *', 'myapp.cron.my_scheduled_job'),
    ('0   4 * * *', 'django.core.management.call_command', ['clearsessions']), #this is a command
]
```

finally run:
```
python manage.py crontab add
python manage.py crontab show
or
python manage.py crontab remove
```

## Date Format 
    Crontab Format:

        MIN HOUR DOM MON DOW CMD

    Format Meanings and Allowed Value:
    MIN     Minute field    0 to 59
    HOUR    Hour field      0 to 23
    DOM     Day of Month    1-31
    MON     Month field     1-12
    DOW     Day Of Week     0-6
    CMD     Command     Any command to be executed.

    example: 0 18,6 * * * is for everyday at 6:00 and 18:00

additional tool for Crontab:

https://crontab.guru/


