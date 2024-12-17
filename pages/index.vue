<script setup lang="ts">
import axios from 'axios';
import type { UserType } from '~/types/user';


const loading = ref<boolean>(true);
const openDialog = ref<boolean>(false);
const selected = ref<object>({});
const searchingName = ref<string>("");

const users = reactive({
    list: [] as UserType[]
});

const getUsers = async () => {
    loading.value = true;
    try {
        loading.value = false;
        const { data } = await axios.get(`https://jsonplaceholder.typicode.com/users/?search=${searchingName.value ?? ''}`, { // searcjh not work
            method: "GET",
        });
        users.list = data
        console.log(users.list);

        return data;
    } catch (error) {
        loading.value = false;
        if (axios.isAxiosError(error)) {
            console.log(error);

        }
    } finally { loading.value = true; }
}
const getUser = async (id: number) => {
    try {
        const { data } = await axios.get(`https://jsonplaceholder.typicode.com/users/${id}`, {
            method: "GET",
        });
        console.log(data);

    } catch (error) {
        if (axios.isAxiosError(error)) {
            console.log(error);

        }
    }
}
const searchName = async () => {
    getUsers();
}
const detailUser = (data: any) => {

    selected.value = data;
    console.log(selected.value);
    openDialog.value = true;
}

onMounted(() => {
    getUsers();
});
</script>
<template>
    <div class="flex flex-col items-center w-full min-h-screen p-5 space-y-5 bg-neutral-300">
        <div>
            <div class="grid">
                <label for="search_name">Pencarian Nama</label>
                <input id="search_name" v-model="searchingName" @input="searchName" type="text"
                    placeholder="Cari nama..." class="pl-1 p-0.5 border-2 w-[300px] rounded">
            </div>
        </div>
        <div class="flex flex-wrap items-center justify-center gap-5">
            <div v-if="loading" v-for="(item, index) in users.list" :key="index">
                <div class="bg-black text-white rounded w-[400px] space-y-5 h-auto p-5 shadow" :key="index"
                    @click="detailUser(item)">
                    <div>
                        <label for="name">Name :</label>
                        <h6 id="email">{{ item.name }}</h6>
                    </div>
                    <div>
                        <label for="email">Email :</label>
                        <h2 id="email">{{ item.email }}</h2>
                    </div>
                    <div>
                        <label for="address">Address :</label>
                        <h3 id="address">{{ item.address?.street }}, {{ item.address?.suite }}, {{ item.address?.city }}
                        </h3>
                    </div>
                </div>
            </div>
            <div v-else>
                <span class="p-1 px-3 text-white bg-black rounded">Loading...</span>
            </div>
        </div>
    </div>
    <UserDetail v-if="openDialog" @close="openDialog = false" :user="selected" />
</template>


<style scoped></style>