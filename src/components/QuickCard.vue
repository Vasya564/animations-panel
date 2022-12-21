<template>
    <div class="animations__list__item">
        <figure class="animations__list__item" :class="[animId == '' ? '' : 'none']">
            <div class="animations__list__item-backdrop bgradient">
            </div>
            <figcaption class="animations__list__item-category">Анімація</figcaption>
            <figcaption class="animations__list__item-name">Відсутня</figcaption>
        </figure>
        <figure class="animations__list__item" :class="[animId == '' ? 'none' : '']" draggable="false">
            <div class="animations__list__item-backdrop">
                <img class="animations__list__item-image" :src="iconId" draggable="false">
            </div>
            <figcaption class="animations__list__item-category">{{ animCategory }}</figcaption>
            <figcaption class="animations__list__item-name">{{ animName }}</figcaption>
        </figure>
        <div class="animations__list__item-controls">
            <span class="material-symbols-rounded close" :class="[animId == '' ? 'hidden' : '']" @click="removeAnim">close</span>
            <span class="animations__list__item-number">{{ number }}</span>
        </div>
    </div>
</template>

<script>
export default {
    name: 'QuickCard',
    props: ['number', 'animId', 'iconId', 'animName', 'animCategory'],
    methods: {
        removeAnim(e){
            const quickAnimId = e.target.parentNode.parentNode.id
            const quickAnimList = JSON.parse(localStorage.getItem('quickAnims'))
            const objectIndex = quickAnimList.findIndex((obj => obj.id == quickAnimId))
            quickAnimList[objectIndex].iconId = ''
            quickAnimList[objectIndex].animId = ''
            quickAnimList[objectIndex].animCategory = ''
            quickAnimList[objectIndex].animName = ''
            localStorage.setItem('quickAnims', JSON.stringify(quickAnimList))
            this.$emit('sync')
        }
    }
}
</script>

<style lang="scss">
@use './src/variables.scss' as v;
.material-symbols-rounded.close {
    font-variation-settings:
    'wght' 700;
    font-size: 14px;
    &:hover{
        cursor: pointer;
    }
}
.animations__list__item-controls{
    position: absolute;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    top: 0;
    height: 76px;
    color: v.$white-color-15-op;
    padding: 5px 0;
    right: 5px;
    z-index: 5;
}
.animations__list__item-number{
    font-size: 18px;
    font-style: italic;
    padding-right: 5px;
}
</style>