<script>
  const shift = 3;

  let input = "";
  let output = "";

  function encrypt() {
    let plaintext = input;
    let ciphertext = "";

    for (let i = 0; i < plaintext.length; i++) {
      //ciphertext += plaintext.charCodeAt(i) + "|";
      let charCode = plaintext.charCodeAt(i);
      charCode += shift;
      ciphertext += charCode + "|";
    }

    output = ciphertext;
  }

  function decrypt() {
    let ciphertext = input;
    let plaintext = "";
    let charCode = "";

    for (let i = 0; i < ciphertext.length; i++) {
      if (ciphertext[i] !== "|") {
        charCode += ciphertext[i];
      } else {
        charCode -= shift;
        plaintext += String.fromCharCode(charCode);
        charCode = "";
      }
    }

    output = plaintext;
  }

  function analyse() {
    let ciphertext = input;
    let charCode = "";
    let codes = [];
    let analysis = "";

    for (let i = 0; i < ciphertext.length; i++) {
      if (ciphertext[i] !== "|") {
        charCode += ciphertext[i];
      } else {
        codes = [...codes, charCode];
        charCode = "";
      }
    }
    if (codes.length) {
      codes.sort();
      let currentCode = codes[0];
      let count = 0;

      for (let i = 0; i < codes.length; i++) {
        if (codes[i] === currentCode) {
          count += 1;
        } else {
          analysis += currentCode + " appears " + count + " times. <br>";
          currentCode = codes[i];
          count = 1;
        }
      }
      analysis += currentCode + " appears " + count + " times. <br>";
    }

    output = analysis;
  }
</script>

<section class="section content">
  <h1>Cipher</h1>

  <label style="width: 40%" class="label">
    Text:
    <input class="input" type="text" bind:value={input} />
  </label>

  <button class="button is-success" on:click={encrypt}>Encrypt</button>
  <button class="button is-success" on:click={decrypt}>Decrypt</button>
  <button class="button is-danger" on:click={analyse}>Analyse</button>

  <h2>Result:</h2>
  <p>{@html output}</p>
</section>
