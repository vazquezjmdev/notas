- ``` 
  awk -F ',' '{print $2, $4}' archivo.csv
  ```
- ``` 
  awk  '{sum += $3}' END '{print "Promedio:, sum/NR(cantidad de campos)}' archivo.csv
  ```
- ``` 
  awk ' '$4 > 70' archivo.txt
  ```
- ``` 
  awk '{gsub(/Ariel/, "Burrito")}; print}' archivo.txt
  ```
-