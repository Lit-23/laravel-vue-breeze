<script setup>
import { onMounted, ref } from 'vue';

const model = defineModel({
    type: String,
    required: true,
});

defineProps({
    name: {
        type: String,
        required: true,
    },
    type: {
        type: String,
        default: 'text',
    },
    message: String,
    autofocus: {
        type: Boolean,
        default: false,
    },
});

const input = ref('');

onMounted(() => {
    if (input.value.hasAttribute('autofocus')) {
        input.value.focus();
    }
});

defineExpose({ focus: () => input.value.focus() });
</script>

<template>
    <div>
        <label class="block text-sm font-medium text-gray-700" :for="type">{{ name }}</label>
        <input
            :type="type"
            :class="[
                'w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500',
                message ? 'border-red-500' : ''
            ]"
            v-model="model"
            ref="input"
        />
        <small class="block text-green-600" v-if="message">{{ message }}</small>
    </div>
</template>
