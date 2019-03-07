<template>
    <div class="country-list">
        <label for="select-country">Choose the country:</label>
        <select id="select-country" v-model="selectedCountry" @change="chooseCountry">
            <option 
                v-for="(country, index) in countries" :key="index"
                :value="country.value"> 
                {{ country.label }}
            </option>
        </select>
    </div>
</template>

<script>
export default {
    data() {
        return {
            selectedCountry: "UA"
        }
    },
    props: ["countries"],
    mounted() {
        this.chooseCountry();
    },
    methods: {
        chooseCountry() {
            this.$emit("countryWasChoose", this.selectedCountry);
        }
    }
}
</script>

<style lang="scss">
    .country-list {
        width: 100%;
        font-size: 24px;
        align-self: center;
        margin-bottom: 15px;
        color: black;

        label {
            margin-right: 10px;
        }

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


