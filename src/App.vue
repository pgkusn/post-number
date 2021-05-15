<template>
    <img alt="Vue logo" src="./assets/logo.png">
    <div>
        <span v-if="distSelect">{{ distSelect }}</span>

        <select v-model="citySelectComputed">
            <option value="" disabled>
                請選擇
            </option>
            <option v-for="city in cities" :key="city" :value="city">
                {{ city }}
            </option>
        </select>

        <select v-model="distSelect">
            <option value="" disabled>
                請選擇
            </option>
            <option v-for="dist in districts" :key="dist.zip" :value="dist.zip">
                {{ dist.name }}
            </option>
        </select>
    </div>
</template>

<script>
import { ref, computed } from 'vue';
import postData from '@/assets/post.json';

export default {
    name: 'App',
    setup () {
        const citySelect = ref('');
        const citySelectComputed = computed({
            get () {
                return citySelect.value;
            },
            set (val) {
                citySelect.value = val;
                distSelect.value = '';
            }
        });
        const cities = computed(() => postData.map(item => item.name));

        const distSelect = ref('');
        const districts = computed(() => postData.find(item => item.name === citySelect.value)?.districts);

        return {
            citySelect,
            cities,
            distSelect,
            districts,
            citySelectComputed
        };
    }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
