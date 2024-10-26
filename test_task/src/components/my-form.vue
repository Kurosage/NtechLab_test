

<template>

    <div class="form" >
        <label class="form__label label_name" for="input_name">Имя</label>
        <p v-if="isInvalidName" class="form__error error error_name">Поле не может быть пустым</p>
        <input class="form__input input_name" type="text" v-model="name" placeholder="Введите имя" min-length="1" :disabled="disabled" required>
        
        <label class="form__label label_age" for="input_age">Возраст</label>
        <p v-if="isInvalidAge" class="form__error error error_age">Введите возраст от 18 до 100 лет</p>
        <input class="form__input input_age" type="number" v-model="age" placeholder="Введите возраст" :disabled="disabled" required>
        
        <button class="form__button button_save" @click="saveInfo" :disabled="disabled">Сохранить</button>
        <button class="form__button button_reset" @click="resetInfo" :disabled="disabled">Отменить</button>
    </div>
    
</template>
<script setup>
    import { defineProps } from 'vue';
    import { ref } from 'vue';
    import { defineEmits } from 'vue';
    const isInvalidName = ref(false)
    const isInvalidAge = ref(false)
    const props = defineProps({
        item:{
            type:Object,
            required:true
        },
        disabled:{
            type:Boolean,
            required:true
        }
    })
    const emit = defineEmits(["save"])
    const name = ref(props.item.name?props.item.name:"")
    const age = ref(props.item.age?props.item.age:"")
    function resetInfo(){
        name.value = props.item.name
        age.value = props.item.age
        isInvalidName.value = false
        isInvalidAge.value = false
    }
    function saveInfo(){
        itemValidation()
        if (!isInvalidName.value && !isInvalidAge.value ){
            isInvalidName.value = false
            isInvalidAge.value = false
            emit('save',{name: name.value,age: age.value})
        }
    }
    function itemValidation(){
        if (name.value.trim().length != 0){
            isInvalidName.value  = false
           
        }else{
            isInvalidName.value  = true
           
        }
        if (age.value >= 18 && age.value <=100){
            isInvalidAge.value = false
           
        }else{
            isInvalidAge.value = true
        }
    }
   
    
</script>
<style scoped>
.form{
    background-color: rgb(233, 159, 171);
    border-radius: 5px;
    padding: 50px 5% ;
    display: flex;
    align-items: center;
    flex-direction: column;
    gap:10px;
}
input{
    height: 20px;
    border-radius:inherit;
    border: 0;
}
button{
    border-radius:inherit;
    height: 20px;
    width: 50%;
    font-weight: bold;
    border: 0;
}
.button_save{
    background-color: rgb(54, 172, 64);
}
.button_reset{
    background-color: rgb(233, 85, 85);
}
label{
    font-size: 20px;
    font-weight: bold;
}
.form__error{
    color:red;
    padding: 0;
    margin: 0;
}
</style>
  