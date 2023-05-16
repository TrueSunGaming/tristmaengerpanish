<script lang="ts">
    import Keyboard from "./lib/Keyboard.svelte";
    
    const basesList: string[] = "abcdefghijklmnŋoʊprstuvwyz".split("");

    const alphabet =          "aāäbćdeēëfghiīïjklmnŋoōöʊprsśtþuūüvwyz";
    const bases: string[] =   "aaabcdeeefghiiijklmnŋoooʊprssttuuuvwyz".split("").map((v) => basesList.indexOf(v).toString(2)).map((v) => v.length != 5 ? `${console.log(v.length), new Array(5 - v.length).fill(0).join("")}${v}` : v);
    const accents: string[] = "01201001200001200000001200001010120000".split("").map((v) => Number(v).toString(2)).map((v) => v.length == 1 ? `0${v}` : v);

    const keyboard: string[] = [...alphabet.split(""), " ", ".", "!", "?"];

    let input = "";

    const map: Map<string, string> = new Map([
        ["R", "R"],
        ["L", "L"],
        ["\n", "\n"]
    ]);

    for (let i = 0; i < alphabet.length; i++) map.set(alphabet[i], `${bases[i]}-${accents[i]}`);

    function translate(inp: string): string {
        return inp.replace(/\s*[!\.?]+/g, "RL").replace(/\s+/g, "R").split("").map((v) => map.get(v)).join("<br>").replace(/0/g, "U").replace(/1/g, "D");
    }

    $: output = translate(input);
</script>
<main>
    <h1>tristmaenjëpaniś tū sīnz</h1>
    <Keyboard alphabet={keyboard} on:type={(e) => input += e.detail.text} />
    <br>
    <textarea bind:value={input}></textarea>
    <h2>Output</h2>
    <p>{ @html output }</p>
</main>

<style>
    main {
        text-align: center;
        padding: 0;
        margin: 0;
    }

    h1 {
        font-size: 50px;
    }

    textarea {
        resize: none;
        width: calc(100vw - 40px);
        background-color: #202020;
        border: none;
        border-radius: 10px;
        padding: 10px;
        height: 20vh;
    }

    p {
        font-size: 20px;
        letter-spacing: 10px;
        word-wrap: break-word;
    }
</style>