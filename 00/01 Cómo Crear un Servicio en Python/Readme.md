1 - Instalamos las librerias
```
apt-get install python-daemon python-lockfile
```

2- Creamos el servicio
```
#!/usr/bin/env python
# -*- coding: utf-8 -*-

import logging
import time
from daemon import runner

class App():
   def __init__(self):
      self.stdin_path      = '/dev/null'
      self.stdout_path     = '/dev/tty'
      self.stderr_path     = '/dev/tty'
      self.pidfile_path    =  '/var/run/test.pid'
      self.pidfile_timeout = 5

   def run(self):
      i = 0
      while True:
         logger.info("message %s" %i++)
         i += 1
         time.sleep(1)

if __name__ == '__main__':
   app = App()
   logger = logging.getLogger("testlog")
   logger.setLevel(logging.INFO)
   formatter = logging.Formatter("%(asctime)s - %(name)s - %(message)s")
   handler = logging.FileHandler("/var/log/test.log")
   handler.setFormatter(formatter)
   logger.addHandler(handler)

   serv = runner.DaemonRunner(app)
   serv.daemon_context.files_preserve=[handler.stream]
   serv.do_action()
```

3- Usando el servicio
```
python deamon.py start
python deamon.py stop
```

4- Info
http://www.elmundoenbits.com/2014/04/crear-daemon-servicio-python.html#.WccQ6X6GOV4
