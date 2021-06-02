<script lang="ts">
    import Square from "./square.svelte";

    const WINNING_POSITIONS = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],

        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],

        [0, 4, 8],
        [2, 4, 6],
    ];

    let nextPlayer = 'X';
    let winner = null;
    let squares = Array(9).fill(null);
    $: status = nextPlayer !== null ? `Next player: ${nextPlayer}` : winner !== null ? `Player ${winner} won` : 'Draw';
    
    function select(i) {
        if (nextPlayer !== null && squares[i] === null) {
            squares[i] = nextPlayer;
            nextPlayer = nextPlayer === 'X' ? 'O' : 'X';

            WINNING_POSITIONS.forEach(l => {
                if (squares[l[0]] !== null && squares[l[0]] == squares[l[1]] && squares[l[1]] == squares[l[2]]) {
                    winner = squares[l[0]];
                    nextPlayer = null;
                }
            });
            if (winner === null) {
                if (squares.filter(e => e === null).length === 0) {
                    nextPlayer = null;
                }
            }
        }
    }
</script>

<div>
    <div class="status">{status}</div>
    <div class="board">
        {#each squares as square, i}
            <Square value={square} on:click={e => select(i)}/>
        {/each}
    </div>
</div>

<style>

    .board {
        display: grid;
		grid-template-columns: repeat(3, 34px);
		grid-template-rows: repeat(3, 34px);
		grid-gap: 0em;
        margin: 1em 0;
    }
</style>