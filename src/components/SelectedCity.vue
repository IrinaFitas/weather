<template>
    <div>
        <figure>
            <i class="icon">===>>></i>
            <p><strong>{{ selectedCity.name }}</strong></p>
            <p>Temperature is: {{ selectedCity.main.temp }}&#176;</p>
            <p>Humidity is: {{ selectedCity.main.humidity }}</p>
        </figure>
    </div>
</template>

<script>
export default {
    props: ["selectedCity"]    
}
</script>

<style lang="scss" scoped>
    figure {
        width: 480px;
        height: 250px;
        background-color: #6139f6;

        p {
            font-size: 20px;
            line-height: 0.5;
        }
    }
</style>

