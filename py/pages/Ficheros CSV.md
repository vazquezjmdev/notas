- import csv
- Listas
- ```
  import csv
  contactos = [("jose",187),("tere",160)]
  with open("contactos.csv", "w", newline="\n") as csvfile:
      writer = csv.writer(csvfile,delimiter=",")
      for contacto in contactos:
          writer.writerow(contacto)
  ```
- ```
  with open("contactos.csv", "r", newline="\n") as csvfile:
      reader = csv.reader(csvfile,delimiter=",")
      for contacto in reader:
          print(contacto)
  ```
- ```
  with open("contactos.csv", "r", newline="\n") as csvfile:
      reader = csv.reader(csvfile,delimiter=",")
      for contacto,alto in reader:
          print(contacto,alto)
  ```
- Dicionari