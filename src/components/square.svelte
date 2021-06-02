<script lang="ts">
    export let value: string = null;
    $: symbol = value === null ? "" : value;
</script>

<button class="square" on:click>
    {symbol}
</button>

<style>
    .square {
        background: #fff;
        border: 1px solid #999;
        float: left;
        font-size: 24px;
        font-weight: bold;
        line-height: 34px;
        height: 34px;
        margin-right: -1px;
        margin-top: -1px;
        padding: 0;
        text-align: center;
        width: 34px;
    }
</style>