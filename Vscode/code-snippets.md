# Vscode code snippets

## scope

- javascript
- typescript
- typescriptreact
- ...

## how can I get the file name

use `${TM_FILENAME}`. Notice that the filename will appear with extensions. You can use `${TM_FILENAME/(\\.\\w+)//}` to remove that.

## cursor position

`$1` will be the first cursor point. When you press `Tab` key, it jumps to `$2`. The final position you can jump to is `$0`  

You can also add label to these positions, using the syntax `${1: labelName}`, replace labelName to whatever label you want.

## example

Here's a simple example, when I type "rfc" in a tsx file, it will generate a component using the current file's name as its name.

```json
{
  "React arrow function component": {
  "scope": "typescriptreact",
  "prefix": "rfc",
  "body": [
   "import { FC } from \"react\";",
   "",
   "type ${TM_FILENAME/(\\.\\w+)//}Props = {",
   "\t$1",
   "};",
   "",
   "export const ${TM_FILENAME/(\\.\\w+)//}: FC<${TM_FILENAME/(\\.\\w+)//}Props> = (${2:props}) => {",
   " return (",
   "  <div>${0:${TM_FILENAME/(\\.\\w+)//}}</div>",
   " );",
   "};",
  ],
  "description": "Create a react arrow function component and export it"
 }
}

```

## Infer the previous placeholder and do transformation

the setter of the prop will be capitalized after you press the tab key.

```json
{
  "React useState hook": {
  "scope": "typescriptreact",
  "prefix": "ust",
  "body": [
   "const [$1,set${1/(\\w)/${1:/upcase}/}] = useState<$3>($4);$0"
  ],
  "description": "Create a react useState hook"
 }
}
```
