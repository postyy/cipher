<script>
let input = ''
let output = ''

function encrypt() {
    let plaintext = input
    let ciphertext = ''

    for(let i = 0; i < plaintext.length; i++) {
        ciphertext += plaintext.charCodeAt(i) + ' '
    }

    output = ciphertext
}
</script>


<h1>Cipher</h1>

<label>
Text
<input type="text" bind:value={input}>
</label>

<button on:click={encrypt}>Encrypt</button>


<h2>Result</h2>
<p>{output}</p>