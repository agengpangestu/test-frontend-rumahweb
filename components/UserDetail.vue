<script lang="ts" setup>
import BaseDialog from './Custom/BaseDialog.vue';

const emit = defineEmits(["close"]);

const closeModal = () => {
    emit("close");
};

defineProps({
    user: {
        type: Object,
        required: true
    }
});

</script>
<template>
    <BaseDialog @close="closeModal">
        <template #title>
            <div class="flex justify-center">
                <h2 class="font-semibold">Detail Usr</h2>
            </div>
        </template>
        <template #body>
            <CustomLableValue label="Name" :value="user.name" />
            <CustomLableValue label="Username" :value="user.username" />
            <CustomLableValue label="Email" :value="user.email" />
            <CustomLableValue label="Address"
                :value="`${user.address.street}, ${user.address.suite}, ${user.address.city}`"
                :value-second="`lat: ${user.address.geo.lat}, lng: ${user.address.geo.lng}`" />
            <CustomLableValue label="Phone" :value="user.phone" />
            <CustomLableValue label="Website" :value="user.website" />
            <CustomLableValue label="Company"
                :value="`name: ${user.company.name}, Catch Phrase: ${user.company.catchPhrase}, ${user.company.bs}`" />
        </template>
        <template #button>
            <div class="flex justify-end">
                <button @click="closeModal" class="p-1 px-4 text-white bg-red-500 rounded">Close</button>
            </div>
        </template>
    </BaseDialog>
</template>
