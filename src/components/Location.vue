<template>
    <div class="column">
        <q-input v-model="country"></q-input>
        <q-input v-model="city"></q-input>
    </div>
</template>

<script>
export default {
    props: {
        modelValue: {
            type: Object,
            default: () => ({
                country: "w",
                city: "z",
            }),
        },
    },

    computed: {
        country: {
            set(value) {
                this.$emit("update:model-value", {
                    ...this.modelValue,
                    country: value,
                });
            },
            get() {
                return this.modelValue.country;
            },
        },

        city: {
            set(value) {
                this.$emit("update:model-value", {
                    ...this.modelValue,
                    city: value,
                });
            },
            get() {
                return this.modelValue.city;
            },
        },
    },
};
</script>
