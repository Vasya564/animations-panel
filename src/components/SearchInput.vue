<template>
    <div class="animations__search">
        <input 
            placeholder="Пошук по назві" 
            class="animations__search__input" 
            :value="modelValue"
            @input="$emit('update:modelValue', $event.target.value)"
        />
        <span class="material-symbols-outlined search">search</span>
    </div>
</template>

<script>
export default {
    name: 'SearchInput',
    props: ['modelValue'],
    emits: ['update:modelValue']
}
</script>

<style lang="scss">
@use './src/variables.scss' as v;
.animations__search{
    position: relative;
}
.animations__search__input{
    padding: 0 10px;
    height: 40px;
    width: 100%;
    background-color: v.$frost-white-color-3-op;
    border: 1px v.$frost-white-color-3-op solid;
    color: v.$white-color;
    outline: none;
}
.animations__search__input::placeholder, .material-symbols-outlined{
    color: v.$white-color-29-op;
}
.animations__search__input:focus::placeholder {
    color: transparent;
}
.material-symbols-outlined.search{
    position: absolute;
    top: 8px;
    right: 5px;
    transition: all .3s;
}
.material-symbols-outlined.search:hover{
    color: v.$white-color;
    cursor: pointer;
}
</style>