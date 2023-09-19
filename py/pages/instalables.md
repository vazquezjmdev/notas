- #+BEGIN_EXAMPLE
  fichero  setup.py
  
  from setuptools import setup
  setup(
      name='',
      version='',
      description='',
      author='',
      author_email='',
      url='',
      packages=[],
      scripts=[]
    
  )
  
  phython3 setup.py sdist
  #+END_EXAMPLE
- instalar
	- pip install fichero comprimido
- Actualizar
	- se vuelve ejecutar
		- pip install fichero_comprimido --upgrade
- Borrar
	- pip unistall nombre paquete