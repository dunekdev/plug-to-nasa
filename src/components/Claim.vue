<template>
    <div id="claim">
        <h1 class="title">TO THE MOON</h1>
        <p class="desc">Begin your jurney through our amazing galaxy</p>
        <p class="desc">and discover places you never even heard of</p>
    </div>
</template>
<script>
export default {
  name: 'Claim',
};
</script>

<style lang="scss" scoped>
    #claim {
        text-align: center;
        @media (min-width: 1200px){
            p {
                font-size: 20px;
            }
        }
    }
</style>
