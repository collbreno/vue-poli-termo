<template>
    <div class="parent">
        <div class="panel">
            <div class="row">
                <guess-component :letters="squareController.guessData.letters" />
                <guess-count 
                    @click="$emit('onGuessCountPressed')"
                    :count="squareController.guesses.length"/>
            </div>
            <word-component v-for="(word, index) in squareController.words"
                :rowIndex="index"
                :wordData="word"
                :lettersScale="squareController.lettersScale[index]"
                :showCorrectAnswer="squareController.isFinished"
                v-bind:key="`word-${index}`" />
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'
import SquareController from '@/types/SquareController';
import GuessComponent from '@/components/GuessComponent.vue';
import WordComponent from '@/components/WordComponent.vue';
import GuessCount from '@/components/GuessCount.vue';


export default defineComponent({
    emits: [ 'onGuessCountPressed' ],
    components: {
        GuessComponent,
        WordComponent,
        GuessCount,
    },
    props: {
        squareController: {
            required: true,
            type: Object as PropType<SquareController>
        }
    }
})
</script>

<style scoped>
    .panel {
        width: 80vw;
        height: 80vw;
        max-height: 360px;
        max-width: 360px;
        margin: auto;
        margin-top: 20px;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .parent {
        width: 100%;
    }

    .row {
        flex: 1;
        width: 100%;
    }
</style>