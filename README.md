# Template Engine Demo
use when you have HTML code you want to use over and over again, render value in template tag

## Step by step
  > add template.
  > add render method.
  > data for display in template,which must be array of object.
  > variable keep the content of the element template.
  > call render method with need parameter.

## Template tag
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
## Data Structure 
**data must be array of object
```
 let data = [
    {firstname: 'Siriphon',lastname: 'Panayathipo', email: 'siriphon@gmail.com'},
    {firstname: 'Manop',lastname: 'Bunmi', email: 'manop@gmail.com'},
    {firstname: 'Somsi',lastname: 'Gaidee', email: 'somsi@gmail.com'},
  ];
```
## Get the content (innerHTML) of the selected element template.
```
let contentTemplate = $(`#masterTemplate`).html();  //use jQuery Method
//or document.getElementById('masterTemplate').innerHTML //use HTML DOM Method
```
## Render Method 
```
  const RenderTemplate = (contentTemplate = null, elementId = null, data = null) => {
    
    //Check parameters
    if(!contentTemplate || !elementId || !data || data.constructor !== Array) return 
    else if(data.constructor === Object) data = [{...data}]
    
    let content = [];
    let keys = data.length > 0 && Object.keys(data[0])
    data.forEach((element) => {
      let item = contentTemplate;
      keys.forEach(o => {
        let replace = `{{` + o + `}}`;
        let re = new RegExp(replace, `gi`);
        item = item.replace(re, element[o])
      })
      content.push(item)
    });
    document.getElementById(`${elementId}`).innerHTML = content.join('');
  }
```
## Calling render method 
```
 RenderTemplate(contentTemplate, `tbody-data`, data);
```