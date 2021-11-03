<template>
    <div class="column">
        <q-input v-model="country"></q-input>
        <q-input v-model="city"></q-input>
        <q-btn icon="fa fa-times" class="text-red" @click="onRemove"></q-btn>{

        }
    </div>
</template>

<script>
export default {
    props: {
        modelValue: {
            default: () => ({ country: null, city: null }),
            type: Object,
        },
    },
    computed: {
        country: {
            set(value) { this.updateModelValue("country", value); },
            get() { return this.modelValue.country; },
        },
        city: {
            set(value) { this.updateModelValue("city", value); },
            get() { return this.modelValue.city;},
        },
    },
    methods: {
        updateModelValue(key, value) {
            this.$emit("update:model-value", { ...this.modelValue, [key]: value,});
        },
        onRemove(){
            this.$emit("on-remove", this.modelValue);
        }
    },
};
</script>
