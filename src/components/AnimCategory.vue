<template>
    <div class="animations__category__container">
        <figure class="animations__category active">
            <img class="animations__category__image active__image" src="../assets/dance.svg">
            <figcaption class="animations__category__name">Танці</figcaption>
        </figure>
        <figure class="animations__category">
            <img class="animations__category__image" src="../assets/walk.svg">
            <figcaption class="animations__category__name">Cтиль ходьби</figcaption>
        </figure>
        <figure class="animations__category">
            <img class="animations__category__image" src="../assets/exer.svg">
            <figcaption class="animations__category__name">Фіз.вправи</figcaption>
        </figure>
        <figure class="animations__category">
            <img class="animations__category__image" src="../assets/social.svg">
            <figcaption class="animations__category__name">Cоціальні</figcaption>
        </figure>
        <figure class="animations__category">
            <img class="animations__category__image" src="../assets/emotion.svg">
            <figcaption class="animations__category__name">Емоції</figcaption>
        </figure>
        <figure class="animations__category">
            <img class="animations__category__image" src="../assets/action.svg">
            <figcaption class="animations__category__name">Дії</figcaption>
        </figure>
        <figure class="animations__category">
            <img class="animations__category__image" src="../assets/stand.svg">
            <figcaption class="animations__category__name">Стійки</figcaption>
        </figure>
        <figure class="animations__category">
            <img class="animations__category__image" src="../assets/unaccept.svg">
            <figcaption class="animations__category__name">Непристойні</figcaption>
        </figure>
    </div>
</template>

<script>
export default {
    name: 'AnimCategory'
}
</script>

<style lang="scss">
@use './src/variables.scss' as v;
.animations__category__container{
    display: flex;
    flex-direction: column;
    color: v.$white-color-40-op;
    padding: 25px 0;
}
.animations__category{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 75px;
    padding: 5px 0;
    flex: 1;
    color: v.$white-color-25-op;
    width: 150px;
    &:not(:first-child){
        margin-top: 30px;
    }
}
.active{
    color: v.$white-color;
    background: linear-gradient(to left, #131a1b85, #e5ffff14, #e5ffff00);
}
.animations__category__name{
    font-size: 12px;
}
.animations__category__image{
    height: 36px;
    opacity: 0.25;
    filter: invert(93%) sepia(15%) saturate(284%) hue-rotate(128deg) brightness(104%) contrast(105%);
}
.active__image{
    opacity: 1;
}
</style>