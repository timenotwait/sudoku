<script>
    import { textStore } from '@sudoku/stores/text'
</script>

<div class="text-box">
    {#each $textStore as str}
        <p>{str.slice(0, str.length - 8)}</p>
    {/each}
</div>

<style>
    .text-box {
        @apply border p-3 rounded-md bg-gray-100;
        font-size: 1rem; /* 字体稍小 */
    }
</style>