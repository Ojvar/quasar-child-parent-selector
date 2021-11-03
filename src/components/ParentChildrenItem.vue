<template>
    <div class="column">
        <!-- Parent -->
        <q-select
            :options="parents"
            v-model="parent"
            @filter="filterFn"
            @filter-abort="abortFilterFn"
        >
            <template v-slot:no-option>
                <q-item>
                    <q-item-section class="text-grey">
                        No results
                    </q-item-section>
                </q-item>
            </template>
        </q-select>
        <!-- Parent -->
        <!-- Child -->
        <q-select
            :options="parents"
            v-model="parent"
            @filter="filterFn"
            @filter-abort="abortFilterFn"
        >
            <template v-slot:no-option>
                <q-item>
                    <q-item-section class="text-grey">
                        No results
                    </q-item-section>
                </q-item>
            </template>
        </q-select>
        <!-- Child -->

        <q-btn icon="fa fa-times" class="text-red" @click="onRemove"></q-btn>
    </div>
</template>

<script>
const ReferenceService = {
    loadParents(service) {
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                switch (service.toLowerCase()) {
                    case "location":
                        resolve(["Iran", "Everywhere else Iran"]);

                    default:
                        resolve([]);
                }
            }, 2000);
        });
    },
    loadChildren(service) {
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                switch (service.toLowerCase()) {
                    case "location":
                        resolve(["Qazvin", "Everywhere else Qazvin"]);

                    default:
                        resolve([]);
                }
            }, 2000);
        });
    },
};

export default {
    name: "ParentChildrenItem",
    props: {
        reference: { type: String, default: "location" },
        modelValue: {
            default: () => ({ parent: null, child: null }),
            type: Object,
        },
    },
    data() {
        return {
            parents: null,
            filterParent: "",
        };
    },
    computed: {
        parent: {
            set(value) {
                this.updateModelValue("parent", value);
            },
            get() {
                return this.modelValue.parent;
            },
        },
        child: {
            set(value) {
                this.updateModelValue("child", value);
            },
            get() {
                return this.modelValue.child;
            },
        },
    },
    methods: {
        filterFn(val, update, abort) {
            this.filterParent = val;
            if (this.parents !== null) {
                update();
            }
            ReferenceService.loadParents(this.reference)
                .then((res) =>
                    update(() => {
                        this.parents = res;
                    })
                )
                .catch((err) =>
                    update(() => {
                        this.parents = [];
                    })
                );
        },
        abortFilterFn() {},

        updateModelValue(key, value) {
            this.$emit("update:model-value", {
                ...this.modelValue,
                [key]: value,
            });
        },
        onRemove() {
            this.$emit("on-remove", this.modelValue);
        },
    },
};
</script>
