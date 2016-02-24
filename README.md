## Regarding Issues

vue-paginator

## Installation

[Use npm.](https://docs.npmjs.com/cli/install)

```
npm install --save vue-paginator
```

##example

```
// example

  <!-- html -->
  <div id="app">
    <paginator :total="total" :current.sync="current">
    </paginator>
  </div>


<!--js-->
var paginator = require('paginator.vue')

Vue.component('paginator',paginator);


// bootstrap the paginator

var demo = new Vue({
  el: '#app',
  data: {
    current: 2,
    total: 20
  }
})

```

