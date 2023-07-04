- For accessing model attributes that have been added using `model.setAttribute()` we do:
  ```html
  ${variable_name}
  ```

- For looping over a collection of objects do:
   ``` html
   <tr th: each={"x : ${variable_name}">
     <td th: text="{x.id}"/>
   </tr>
   ```

