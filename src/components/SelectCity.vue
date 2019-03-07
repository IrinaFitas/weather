<template>
    <div class="select-city">
        <select>
            <option
                v-for="(city, index) in selectedCitiesFromParent"
                :value="index"
                :key="index">
                {{ city.name }}
            </option>
        </select>
    </div>
</template>

<script>
export default {
    props: ["selectedCitiesFromParent"]
}
</script>
<style lang="scss" scoped>
    .select-city {
        width: 100%;
        font-size: 24px;
        align-self: center;
        margin-bottom: 15px;
        color: black;

        select {
            padding: 15px;
            border: 2px solid #004d00;
            outline: none;
        }

        option {
            font-size: 16px;
        }
    }
</style>


