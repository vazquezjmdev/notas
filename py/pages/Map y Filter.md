- ```
  ambda_reverse = lambda s: s[::-1]
  print(lambda_reverse("tengo la camisa sucio"))
  ```
-
- map(<f>,<iterable>)
	- #+BEGIN_EXAMPLE
	  def reverse(s):
	       return s[::-1]
	  reverse("patata")
	  #atatap" 
	  animals = ["cat","dog", "bird", "gecko"]
	  
	  iterator = map(reverse, animals)
	  for i in iterator:
	    print(i)
	  
	  list(iterator)
	  
	  
	  #+END_EXAMPLE
-
-