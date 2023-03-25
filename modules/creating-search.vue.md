# Creating search.vue

```html

<template>
    <FormKit v-model="model.slug" label="Slug" id="slug" type="text" validation="required" />
</template>

<script>

export default {
    watch: {
        model: {
            handler: function (newVal) {
                var path = ['blog', 'content'];
                this.$emitter.emit("system-search", { path:['blog', 'content'], search: this.model });
            },
            deep: true
        },
    },
    data() {
        return {
            id: null,
            model: {
                slug: "",
            },

        };
    },
};
</script>
```
