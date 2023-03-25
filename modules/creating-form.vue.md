# Creating form.vue

```html
<template>
  <edit-render :path_param="['blog', 'content']" :model="model"></edit-render>
</template>

<script>
  export default {
    data() {
      return {
        id: null,
        model: {
          id: "",
          description: "",
          user_id: "",
          payment_id: "",
          amount: "",
          completed: "",
          successful: ""
        },
  
      };
    }
  };
</script>

```
