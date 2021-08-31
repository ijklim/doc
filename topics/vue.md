# Vue Guide

* Sample composable

```js
// useCounter.js
import {ref, readonly} from 'vue';

// Note: Outside of export count is global, state will be preserved across components
const count = ref(0);

export default () => {
    const increment = () => count.value++;

    return {
        count: readonly(count), // Safeguard count using readyonly()
        increment,
    };
}
```