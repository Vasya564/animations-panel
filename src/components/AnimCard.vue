<template>
  <figure class="animations__list__item" 
    :draggable="draggable"
    @dragstart="dragStart"
    @dragover.stop>
    <div class="animations__list__item-backdrop">
        <slot></slot>
    </div>
    <figcaption class="animations__list__item-category">{{ animCategory }}</figcaption>
    <figcaption class="animations__list__item-name">{{ animName }}</figcaption>
  </figure>
</template>

<script>
export default {
    name: 'AnimCard',
    props: {
        iconId: String,
        animId: String,
        animCategory: {
            type: String,
            default: 'Анімація'
        },
        animName: {
            type: String,
            default: 'Відсутня'
        },
        draggable: String
    },
    methods: {
        dragStart(e){
            const target = e.target
            e.dataTransfer.setData('card_id', target.id)
        }
    }
}
</script>

<style>
</style>