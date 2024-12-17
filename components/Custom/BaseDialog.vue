<script setup lang="ts">

const emit = defineEmits(["close"])

function closeModal() {
    console.log('base modal closed');

    emit("close")
}
</script>
<template>
    <Teleport to="body">
        <div class="fixed top-0 left-0 flex justify-center items-center w-full z-[999] h-full bg-gray-900 bg-opacity-80"
            role="dialog" aria-labelledby="modalTitle">
            <div class="w-[450px] h-auto bg-white p-2 rounded-lg" ref="target">
                <header class="p-2" v-if="$slots.title" id="modalTitle">
                    <slot name="title" />
                </header>
                <main class="h-full p-2 space-y-2.5">
                    <div>
                        <slot name="body" />
                    </div>
                    <div class="space-x-5">
                        <slot name="button" />
                    </div>
                </main>
            </div>
        </div>
    </Teleport>
</template>


<style scoped></style>