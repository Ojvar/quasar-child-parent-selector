<template>
    <div class="column">
        <div class="row">
            <q-btn icon="fa fa-plus" @click="onAddLocation"> </q-btn>
        </div>
        <parent-children-item :reference="reference"
            :key="index" @on-remove="onRemoveItem(item)"
            v-for="(item, index) in items" v-model="items[index]"></parent-children-item>
    </div>
</template>

<script>
import ParentChildrenItem from "./ParentChildrenItem.vue";

export default {
    name: "ParentChildren",
    components: { ParentChildrenItem, },
    computed: {
        items: {
            get() { return this.modelValue; },
            set(value) { this.$emit("update:model-value", value); },
        },
    },
    props: {
        modelValue: { type: Array, default: () => [], },
        reference: { type: String, default: "location" },
    },
    methods: {
        onAddLocation() { this.items.push({ parent: null, child: null, }); },
        onRemoveItem(item){ this.items = this.items.filter(x => x !== item); }
    },
};
</script>
