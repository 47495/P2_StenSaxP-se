<script setup>
    const props = defineProps(['alternatives'])
</script>

<template>
    <div id="object-stats">
        <div v-for="alt of Object.keys(props.alternatives)" :key="alt">
            <div class="object">
                <img :src="`./img/${alt}.png`"
                 style="height: 2rem;" class="ignore" />
                <div>{{ props.alternatives[alt] }}</div>
            </div>
        </div>
    </div>
</template>

<style scoped>
#object-stats {
    display: flex;
    justify-content: space-evenly;
}

.object {
    display: flex;
    align-items: center;
}

.object > * {
    margin: 0.25rem;
}
</style>