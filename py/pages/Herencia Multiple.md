- super(va1)
- El inicializador Clase.\_\_init\_\_(self,val01,val02)
- print(Cuadrado.mro()) orden de resolucion
- ejemplo
	- FiguraGeometrica.py
	- ```apl
	  class FiguraGeometrica:
	      def __init__(self, ancho, alto):
	          self._ancho = ancho
	          self._alto = alto
	  
	      @property
	      def ancho(self):
	          return self._ancho
	  
	      @ancho.setter
	      def ancho(self, ancho):
	          self._ancho = ancho
	  
	      @property
	      def alto(self):
	          return self._alto
	  
	      @alto.setter
	      def alto(self, alto):
	          self._alto = alto
	  
	      def __str__(self):
	          return f'FiguraGeometrica [Ancho: {self._ancho}, Alto: {self.alto} ]'
	  ```
- Color.py
	- ```apl
	  class Color:
	      def __init__(self, color):
	          self._color = color
	  
	      @property
	      def color(self):
	          return self._color
	  
	      @color.setter
	      def color(self, color):
	          self._color = color
	  
	      def __str__(self):
	          return f'Color[color: {self._color}]'
	  ```
- Cuadrado.py
	- ```
	  from FiguraGeometrica import FiguraGeometrica
	  from Color import Color
	  
	  class Cuadrado(FiguraGeometrica, Color):
	      def __init__(self, lado, color):
	          # super().__init__(lado)
	          FiguraGeometrica.__init__(self, lado, lado)
	          Color.__init__(self, color)
	  
	      def calcular_area(self):
	          return self.alto * self.ancho
	  
	      def __str__(self):
	          return f'{FiguraGeometrica.__str__(self)} {Color.__str__(self)}'
	          
	  ```
- test_figura_geaometrica.py
	- ```
	  from Cuadrado import Cuadrado
	  
	  cuadrado1 = Cuadrado(5, 'rojo')
	  print(f'Cálculo área cuadrado: {cuadrado1.calcular_area()}')
	  print(cuadrado1)
	  
	  ```