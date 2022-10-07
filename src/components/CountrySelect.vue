<template>
    <div>
        <select v-model="selected" class="form-select mb-10 mt-10 block w-6/12 mx-auto border p-4 ">
            <option value="0">Select country</option>
            <option v-for="country in countries" :value="country.ID">{{country.Country}}</option>
        </select>
    </div>
</template>

<script>
    export default {
        name: 'CountrySelect',
        props: ['countries'],
        data() {
            return {
                selected: 0,
            }
        }
    }
</script>