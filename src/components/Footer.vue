<template>
    <footer>
        <p>Copyright &copy; 2022</p>
        <RouterLink to="/about">About </RouterLink>
    </footer>
</template>
<script>
import { RouterLink } from 'vue-router';

export default{
    components: { RouterLink }
}
</script>
<style scoped>
a {
    color: #333;

}
footer {
margin-top: 30px;
text-align: center;
}
</style>