<template>
    <q-page class="column">
        <Locations v-model="locations" />
        <div class="row"><pre>{{ locations }}</pre></div>
    </q-page>
</template>

<script>
import { defineComponent } from "vue";
import Locations from "src/components/Locations.vue";

export default defineComponent({
    name: "PageIndex",
    components: { Locations },
    data() {
        return { locations: [{}] };
    },
});
</script>
