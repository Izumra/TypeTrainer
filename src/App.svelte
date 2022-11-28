<script>
  import { writable } from "svelte/store";
  let text='A Christian holiday signifying the birth of Jesus, Christmas is widely celebrated and enjoyed across the United States and the world. The holiday always falls on 25 December (regardless of the day of the week), and is typically accompanied by decorations, presents, and special meals. Specifically, the legend behind Christmas (and the one that most children are told) is that Santa Claus, a bearded, hefty, jolly, and red-jacket-wearing old man who lives in the North Pole, spends the year crafting presents with his elves, or small, festive, excited Santa-assistants. All the children who behave throughout the year are admitted to the Good List, and will presumably receive their desired gifts on Christmas, while those who don\'t behave are placed on the Naughty List, and will presumably (although the matter is determined by parents) receive a lump of coal. Santa Claus is said to fly around the Christmas sky in a sled powered by his magical reindeer, or cold-resistant, mythically powered, individually named animals, delivering presents to each child\'s house in the process. Santa is also expected to slide through chimneys to deliver these presents (homes not equipped with chimneys might "leave the front door cracked open"), and children sometimes arrange cookies or other treats on a plate for him to enjoy. Gifts are placed underneath a Christmas tree, or a pine tree that\'s decorated with ornaments and/or lights and is symbolic of the holiday. Additionally, smaller gifts may be placed inside a stocking, or a sock-shaped, holiday-specific piece of fabric that\'s generally hung on the mantle of a fireplace (homes without fireplaces might use the wall). A Christmas tree\'s ornaments, or hanging, typically spherical decorations, in addition to the mentioned lights, may be accompanied by a star, or a representation of the Star of Jerusalem that the Three Apostles followed while bringing Baby Jesus gifts and honoring him, in the Bible.'
  let checkText=text
  let setSymbols=0
  let enterText=''
  let body;
  let entertext
  let form=writable(17)
  function checkKey(e){
    if(e.key!='Shift'&&checkText.length!=0){
      if($form<entertext.offsetHeight){
        body.scrollTo(0,entertext.offsetHeight-14)
        $form=entertext.offsetHeight
      }
      enterText+=e.key
      checkText=checkText.slice(setSymbols+1,checkText.length)
      console.log(enterText)
    }
  }
</script>
<svelte:window on:keypress={checkKey}/>
<div class="wrap">
  <header>
    <div class="logo">
      Type trainer
    </div>
  </header>
  <!-- поиграться с настройкой высоты  -->
  <div bind:this={body} class="textBox">
    <string bind:this={entertext}>
      {#each Array.from(enterText) as symbol,i}
        {#if symbol==text[i]}
          <string class='trueText'>{symbol}</string>
        {:else}
          <string class='errorText'>{text[i]}</string>
        {/if}
      {/each}
    </string>
    {#each Array.from(checkText) as symbol,i}
      <string class='defaultText'>{symbol}</string>
    {/each}
  </div>
</div>

<style>
  .wrap{
    width: 1450px;
  }
  header{
    display: flex;
    justify-content: center;
    width: inherit;
  }
  .logo{
    font-size: 102px;
    font-family: 'Rubik Glitch', cursive;
    color:azure;
  }
  .defaultText{
    color: rgb(163, 162, 162);
    font-size: 32px;
  }
  .textBox{
    height:112px;
    overflow-y: auto;
    margin-top: 60px;
    
  }
  .textBox::-webkit-scrollbar{
    width:0
  }
  .errorText{
    color: rgb(249, 148, 148);
    font-size: 32px;
  }
  .trueText{
    color: azure;
    font-size: 32px;
  }
</style>
