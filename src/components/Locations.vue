<template>
    <div class="column">
        <div class="row">
            <q-btn icon="fa fa-plus" @click="onAddLocation"> </q-btn>
        </div>

        <location
            :key="index"
            v-for="(item, index) in locations"
            v-model="locations[index]"
        >
        </location>
    </div>
</template>

<script>
import Location from "./Location.vue";

export default {
    name: "Locations",

    components: {
        Location,
    },

    computed: {
        locations: {
            get() {
                return this.modelValue;
            },
            set(value) {
                this.$emit("update:model-value", value);
            },
        },
    },

    props: {
        modelValue: {
            type: Array,
            default: () => [],
        },
    },

    methods: {
        onAddLocation() {
            this.locations.push({
                country: null,
                city: null,
            });
        },
    },
};
</script>
