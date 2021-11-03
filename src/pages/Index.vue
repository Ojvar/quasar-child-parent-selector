<template>
    <q-page class="column">
        <parent-children v-model="locations" service="location" />
        <div class="row"><pre>{{ locations }}</pre></div>
    </q-page>
</template>

<script>
import { defineComponent } from "vue";
import ParentChildren from "src/components/ParentChildren.vue";

export default defineComponent({
    name: "PageIndex",
    components: { ParentChildren },
    data() { return { locations: [{}] }; },
});
</script>
