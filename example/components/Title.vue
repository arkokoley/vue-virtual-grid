<template>
    <div class="title" :style="{ height: `${item.height}px` }">
        <h2 @click="$emit('event-test')">{{ item.injected.title }}</h2>
    </div>
</template>

<script lang="ts">
import { Prop, Component, Vue } from 'vue-property-decorator';
import { Item } from '../../src/types';

export interface Title {
    title: string;
}

@Component
export default class TitleComponent extends Vue {
    @Prop() item: Item<Title>;
}
</script>

<style scoped>
.title {
    display: inline-grid;
    align-items: center;
    width: 100%;
    color: #fff;
    background: #666;

    border-radius: 3px;
}
</style>
