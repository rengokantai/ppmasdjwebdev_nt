### ppmasdjwebdev_nt
####7. Management and Maintenance of Your Application
#####Creating manage.py commands
```
from django.core.management.base import BaseCommand
class Command(BaseCommand):
  help=''
  def add_arguments(self,parser):
    parser.add_arguments('add',nargs='+',type=int)
  def handle(self, *args, **options):
    self.stdout.write('')
```
