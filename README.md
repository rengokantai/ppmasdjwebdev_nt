### ppmasdjwebdev_nt
####6. Caching for Optimum Performance
#####Low-level caching
```
CACHES ={
  'default':{
    'BACKEND':'django.core.cache.backends.db.DatabaseCache',
    'LOCATION':'tbname',
  }
}
```
command
```
python manage.py createcachetable
```
sample file
```
from django.views.generic.detail import DetailView
from django.core.cache import cache
....

class CacheDetailView(DetailView):
  def get_queryset(self):
    return super(CacheDetailView,self).get_queryset().select_related()
  def get_object(self,queryset=None):
    obj = cache.get('%s-%s' % self.model.__name__.lower(),self.kwargs['pk']),None)
    if not obj:
      obj = super(CachedDetailView,self).get_object(queryset)
      cache.set('%s-%s'%(self.model.__name__.lower(),self.kwargs['pk']),obj)
    return obj
```

update cache(delete old cache)  
override save() in model.py.
```
def save(self,*args,**kwargs):
  super(M,self).save(*args,**kwargs)
  cache.delete('m-%s'%self.pk)
```
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
