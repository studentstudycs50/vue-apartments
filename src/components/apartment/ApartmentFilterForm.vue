<template>
    <form class="form" @submit.prevent="handleSubmit">
        <CustomSelect 
        :items="cities" 
        class="form__select" 
        v-model="city"
        />
        <CustomInput 
        v-model="price"
        placeholder="Price, from"
        error-message="Please add information"
        :rules="rules"
        type="number"
        />
        <Button 
        class="form__submit"
        type="submit"
        >Chose</Button>
    </form>
</template>

<script>
import CustomInput from '../shared/CustomInput.vue';
import CustomSelect from '../shared/CustomSelect.vue';
import Button from '../Button.vue';
import { isRequired, charLimit } from '@/utils/validationRules';

    export default {
        name: 'ApartmentFilterForm',
        components: {
            CustomInput,
            CustomSelect,
            Button
        },
        data() {
            return {
                price: '',
                city: ''
            }
        },
        computed: {
            rules() {
                return [ isRequired, charLimit(10) ]
            },
            cities() {
                return [{ value: '', label: 'City', selected: true }, 'Kiev', 'Odesa', 'Poltava', 'Kharkiv', 'Dnipro', 'Lviv', 'Kherson', 'Mariupol']
            }
        },
        methods: {
            handleSubmit() {
                this.$emit('submit', {
                   city: this.city,
                   price: this.price
                });
            }
        }
    }
</script>

<style lang="scss" scoped>
.form {
    display: flex;

    &__select {
        margin-right: 30px;
    }

    &__submit {
        margin-left: auto;
    }
}
</style>