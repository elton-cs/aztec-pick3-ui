<script>
    import Counter from "./Counter.svelte";
    import Submit from "./Submit.svelte";

    let digit1 = "";
    let digit2 = "";
    let digit3 = "";

    let name = "";

</script>

<div class="flex flex-col items-center">
    <h1 class="font-bold">Aztec ZkPick 3</h1>

    <div class="flex flex-row items-center">
        <Counter/>
        <Counter/>
        <Counter/>
    </div>

    <Submit/>

</div>