<template>
    <div class="select-city">
        <label for="select-city">Choose the city:</label>
        <select id="select-city" v-model="selectedCity" @change="selectCity">
            <option
                v-for="(city, index) in selectedCitiesFromParent"
                :value="city.id"
                :key="index">
                {{ city.name }}
            </option>
        </select>
    </div>
</template>

<script>
export default {
    props: ["selectedCitiesFromParent"],
    data() {
        return {
            selectedCity: ""
        }
    },
    methods: {
        selectCity() {
            this.$emit("cityWasSelected", this.selectedCity);
        }
    }
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
            width: 45%;
        }

        label {
            margin-right: 15px;
        }

        option {
            font-size: 16px;
        }
    }
</style>


