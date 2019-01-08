#Template Engine Demo
use when render value in template tag

## mockup data
```
 let data = [
    {firstname: 'Siriphon',lastname: 'Panayathipo', email: 'siriphon@gmail.com'},
    {firstname: 'Manop',lastname: 'Bunmi', email: 'manop@gmail.com'},
    {firstname: 'Somsi',lastname: 'Gaidee', email: 'somsi@gmail.com'},
  ];
```
## template tag
```
  <template id="MasterTemplate">
    <tr>
      <td>{{firstname}}</td>
      <td>{{lastname}}</td>
      <td>{{email}}</td>
      <td>
          <a class="btn btn-danger btn-xs" onclick="delItem('{{firstname}}')">
            <i class="fa fa-trash" aria-hidden="true"></i> delete
        </a>
          <a class="btn btn-info btn-xs" onclick="editItem('{{firstname}}')">
            <i class="fa fa-pencil-square-o" aria-hidden="true"></i> Edit
        </a>
        </td>
    </tr>
  </template>
```
## javascript function
```
  const RenderTemplate = (elementId = null , data = []) => {
    let content = [];
    let keys = data.length > 0 && Object.keys(data[0])
    data.forEach( ( element ) => {
      let item = MasterTemplate;
      keys.forEach(o => {
        let replace = `{{`+o+`}}`;
        let re = new RegExp(replace,`gi`);
        item = item.replace(re, element[o])
      })
      content.push(item)
    });
    document.getElementById(`${elementId}`).innerHTML = content.join(''); 
  }
```
