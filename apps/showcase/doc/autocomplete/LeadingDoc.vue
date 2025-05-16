<template>
    <DocSectionText v-bind="$attrs">
        <p>Adding the <i>leading</i> slot displays a content before the input field.</p>
    </DocSectionText>
    <div class="card flex justify-center">
        <AutoComplete v-model="value" :suggestions="items" @complete="search">
            <template #leading="{ value, placeholder }">
                <div v-if="value" class="flex gap-2">
                    <div class="w-2 rounded-full bg-green-600">&nbsp;</div>
                </div>
                <div v-else>{{ placeholder }}</div>
            </template>
            <template #option="{ option }">
                <div class="flex gap-2">
                    <div class="w-2 rounded-full bg-green-600">&nbsp;</div>
                    <div>{{ option }}</div>
                </div>
            </template>
        </AutoComplete>
    </div>
    <DocSectionCode :code="code" />
</template>

<script>
export default {
    data() {
        return {
            value: '',
            items: [],
            code: {
                basic: `
<AutoComplete v-model="value" dropdown :suggestions="items" @complete="search" />
`,
                options: `
<template>
    <div class="card flex justify-center">
        <AutoComplete v-model="value" dropdown :suggestions="items" @complete="search" />
    </div>
</template>

<script>
export default {
    data() {
        return {
            value: '',
            items: []
        };
    },
    methods: {
        search(event) {
            let _items = [...Array(10).keys()];

            this.items = event.query ? [...Array(10).keys()].map((item) => event.query + '-' + item) : _items;
        }
    }
};
<\/script>
`,
                composition: `
<template>
    <div class="card flex justify-center">
        <AutoComplete v-model="value" dropdown :suggestions="items" @complete="search" />
    </div>
</template>

<script setup>
import { ref } from "vue";

const value = ref(null);
const items = ref([]);

const search = (event) => {
    let _items = [...Array(10).keys()];

    items.value = event.query ? [...Array(10).keys()].map((item) => event.query + '-' + item) : _items;
}
<\/script>
`
            }
        };
    },
    methods: {
        search(event) {
            let _items = [...Array(10).keys()];

            this.items = event.query ? [...Array(10).keys()].map((item) => event.query + '-' + item) : _items;
        }
    }
};
</script>
