<template>
    <router-link :to="{ name: 'Details', params: {id: user._id} }" target="_blank">
        <h3>{{ user.Code }}</h3>
    </router-link>
</template>

<script>
export default {
    props:['user']
}
</script>
<style>

</style>